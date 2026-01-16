# Rules for AI Assistants

Adapt the rules according to your style and run-books.

## A. Base Rules

1. Always read this rules file periodically to stay up to date with the latest rules and avoid the long chat memory loss.
2. AI agents MUST work in sessions. Each session is a conversation between the user and the AI assistant.
3. AI agents ARE NOT allowed to create files outside of the session folder by default, but may create and modify files at explicit user request.
4. AI agents are expected to create a session folder at the beginning of each session as a child of `.ai-assist/sessions`. The folder name MUST follow the format `YYYY/MM/DD/<Sequence>_<Mnemonic>` where sequence is a two-digit number (01, 02, etc.) and mnemonic is a meaningful short description. The Agent MUST verify the current running OS before creating the session folder. For example, `mkdir -p <folder>` creates a `-p` folder in Windows and we do not want that.
5. The user decides when a session finishes, it's not up to the AI assistant to decide. When the session ends, the AI assistant MUST produce a synthesis report and save it to the session folder. Also, this synthesis MUST have two forms: one markdown for human reading and one in a concise memory JSON format for eventual future AI use.

## B. Meta-Repository Context

6. Consider the current repository as a meta-container of many other repositories, which may have different purposes and technology stacks. Some of the children repositories may not admit AI assistance at all.

    By "meta-repository" we mean that it will have other repositories as children in the file system.

## C. Rule Hierarchy

7. **Hierarchy**: Rules are organized on a hierarchy and they SHOULD be loaded in a sparse mode according to the session purpose.

    ```
    ./                                              # root of this repository
    ├── .ai-assist/
    │   ├── README.md                               # Level 1: Global meta-repo README (this file)
    │   ├── RULES.md                                # Level 1: Global meta-repo rules
    │   └── <other content>
    ├── <child repo 1 path>
    │   ├── <specific ai rules>                     # Level 2: Child repo specific rules
    │   └── <child repo 1 content>
    │       └── <grand-child repo 1-1 path>
    │           ├── <specific ai rules>             # Level 3: Grand-child repo specific rules
    │           └── <grand-child repo 1-1 content>
    ├── <repo path N>
    │   ├── <specific ai rules>                     # Level 2: Child repo specific rules
    │   └── <child repo path 1>
    └── <repo files>
    ```

8. **Loading and priority**: AI assistants MUST load rules in this order. Earlier rules have higher precedence and cannot be overridden by later rules:

      1. **Global Rules** (this file): `.ai-assist/RULES.md` must be loaded for every session in the beginning at the session, at wrap up time and every time the prompting cycle surpasses 10 interactions. This ensures these rules are always present in the conversation context.

          ```
          ./                                       # root of this repository
          ├── .ai-assist/
          │   ├── RULES.md                         # Level 1: Global meta-repo rules
          │   └── <other content>
          └── <repo content>
          ```
      
      2. **Domain or family**: Rules that are loaded at user's request depending on the activity at hand:

          ```
          ./                                       # root of this repository
          ├── .ai-assist/
          │   ├── README.md                        # Level 1: Global meta-repo README (this file)
          │   ├── RULES.md                         # Level 1: Global meta-repo rules
          │   └── domains/                         # Level 2: Family or domain rules
          │       ├── docker-builder.md            # Rules for Docker image builders
          │       ├── terraform.md                 # Rules for Terraform sandboxes
          │       ├── wm-service-dev.md            # Rules for webMethods service development
          │       └── golang-dev.md                # Rules for Go development
          └── <repo files>
          ```

      3. **Repository Specific Rules**: 

          1. Each repository may have a different discipline for managing AI Assistance rules
          2. Repositories in `ibm-webmethods-continuous-delivery` SHOULD observe the same structure. that is

              ```
              ./                                       # root of child repository
              ├── .ai-assist/
              │   ├── README.md                        # Level 1: Global meta-repo README (this file)
              │   ├── RULES.md                         # Level 1: Global meta-repo rules
              │   └── specific/                        # Level 2: Repo specific rules
              │       └── any-topic.md
              └── <repo files>
              ```

      4. Repositories may be nested under each other. In this case, the rules of the parent repository take precedence over rules of the child repository (consistent with the principle that earlier-loaded rules have higher precedence).

## D. Session Management

9. **Context-Aware Sessions**:
   - Session folder name SHOULD include sandbox context if applicable
   - Format: `YYYY/MM/DD/<Sequence>_<Mnemonic>` where sequence is a two-digit number (01, 02, etc.)
   - Example: `2026/01/15/01_RulesReview`
   - Session summary MUST include sandbox context used

## F. File Operations

10. **Sandbox File Modifications**:
    - Modifications to sandbox configs require explicit permission
    - Changes to `docker-compose.yml`, `Dockerfile` need review
    - AI Agents MUST never read `.env` files. Read `EXAMPLE.env` instead.
    - Document all sandbox modifications in session summary

11. **Path Resolution**:
    - Always use relative paths from workspace root
    - For sandbox-internal paths, use container paths
    - Clearly distinguish between host paths and container paths
    - Example: Host `c:/r/repo/.sbx/name/` → Container `/workspace/.sbx/name/`

## E. Interaction

12. **Host Agent to Sandbox Content**:
    - According to the session, the agent MAY interact with the sandbox via docker exec commands
    - The agent MUST always remember or verify the current OS. Distinguish clearly, for example, that if we are in a Windows IDE, the terminals are PowerShell, while sandbox-related commands may be issued towards the available shell: busybox, nushell, etc.