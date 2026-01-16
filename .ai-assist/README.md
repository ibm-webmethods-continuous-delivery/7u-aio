# AI Assistance for Meta-Repository Template

## Overview

This is a **template repository** designed to help you manage multiple child repositories with AI assistance. The `.ai-assist/` folder contains configuration files and generated content from AI assistants working with your codebase.

**Key Principles:**
- AI agents work as **attended assistants**, helping you with tasks in real-time
- This structure is **IDE and agent-agnostic** - adapt it to your preferred tools
- **You control the workflow** - customize these files to match your needs

## What is a Meta-Repository?

A meta-repository is a parent repository that contains multiple child repositories, each potentially with different:
- Technology stacks (Go, Python, Java, etc.)
- Purposes (services, libraries, infrastructure)
- Development workflows
- AI assistance requirements

Some child repositories may not use AI assistance at all - that's perfectly fine.

## Repository Structure

```
./                                       # Your meta-repository root
├── .ai-assist/
│   ├── README.md                        # This file - human-readable guide
│   ├── RULES.md                         # AI agent instructions
│   ├── domains/                         # Optional: Domain-specific AI rules
│   │   ├── docker-builder.md            # Rules for Docker projects
│   │   ├── terraform.md                 # Rules for Terraform projects
│   │   └── golang-dev.md                # Rules for Go development
│   └── sessions/                        # AI-generated session logs
│       └── YYYY/MM/DD/
│           └── 01_SessionName/          # Timestamped session folders
│
└── <child-repos>/                       # Your managed repositories
    ├── .ai-assist/                      # Optional: Repo-specific AI config
    └── .sbx/                            # Optional: Development sandboxes
```

## Getting Started

### 1. Customize for Your Needs

This is a **template** - adapt it to your workflow:

1. **Edit `RULES.md`**: Modify AI agent behavior rules to match your standards
2. **Add domain rules**: Create files in `domains/` for specific technology stacks
3. **Update this README**: Document your specific meta-repository purpose and structure

### 2. Working with AI Assistants

When working with AI assistants in this repository:

- **Sessions are tracked**: Each AI conversation creates a session folder with logs
- **Rules are hierarchical**: Global rules apply everywhere, domain rules apply to specific contexts
- **You stay in control**: AI agents ask for permission before making significant changes

### 3. Child Repository Integration

Each child repository can optionally have:

```
<child-repo>/
├── .ai-assist/
│   ├── README.md                        # Repo-specific AI guidance
│   └── RULES.md                         # Repo-specific AI rules
└── .sbx/                                # Development sandboxes (optional)
    └── <sandbox-name>/
        ├── docker-compose.yml
        └── README.md
```

## Best Practices

### Security
- **Never commit secrets**: Use `.env.example` files, not `.env` files
- **Review AI changes**: Always review modifications before committing
- **Sensitive repos**: Some child repositories may not be suitable for AI assistance

### Organization
- **Use meaningful session names**: Help future you understand what was done
- **Document decisions**: Session summaries capture context for later reference
- **Keep rules updated**: Periodically review and update AI rules as your workflow evolves

### Sandboxes and DevContainers
- Repositories **may** have sandboxes in `.sbx/` directory
- Repositories **may** have devcontainers in `.devcontainer/` directory
- These are optional - use what fits your workflow

## File Purposes

| File | Audience | Purpose |
|------|----------|---------|
| `README.md` (this file) | **Humans** | Understand repository intent and usage |
| `RULES.md` | **AI Agents** | Instructions for AI behavior and constraints |
| `domains/*.md` | **AI Agents** | Context-specific rules for different technologies |
| `sessions/` | **Both** | Historical record of AI-assisted work |

## Adapting This Template

To make this template your own:

1. **Replace example paths** with your actual repository structure
2. **Add your domain-specific rules** in the `domains/` folder
3. **Update the meta-repository context** in `RULES.md` (Rule 6)
4. **Document your specific workflows** in this README
5. **Remove or modify** sections that don't apply to your use case

## Questions?

This template is designed to be flexible. If something doesn't fit your workflow, change it! The goal is to make AI assistance work **for you**, not to impose a rigid structure.
