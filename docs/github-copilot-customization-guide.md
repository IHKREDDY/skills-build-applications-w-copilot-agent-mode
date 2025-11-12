# GitHub Copilot Customization Standards Guide

## Overview

This guide provides comprehensive standards for customizing GitHub Copilot in this repository using prompt files and instruction files. These customization mechanisms enable consistent, repeatable, and efficient development workflows.

## Table of Contents

1. [Quick Reference](#quick-reference)
2. [Understanding the Customization System](#understanding-the-customization-system)
3. [When to Use What](#when-to-use-what)
4. [File Structure Overview](#file-structure-overview)
5. [Best Practices](#best-practices)
6. [Examples](#examples)
7. [Additional Resources](#additional-resources)

## Quick Reference

| Feature | Prompt Files | Instruction Files |
|---------|--------------|-------------------|
| **Purpose** | Define WHAT tasks to accomplish | Define HOW tasks should be implemented |
| **Location** | `.github/prompts/` | `.github/instructions/` |
| **Extension** | `.prompt.md` | `.instructions.md` |
| **Usage** | Run directly in Copilot Chat with `/prompt-name` | Applied automatically based on context |
| **Scope** | Single task execution | Ongoing guidance for code areas |
| **Content Focus** | Task steps and verification | Patterns, standards, and constraints |

## Understanding the Customization System

### Prompt Files

**Purpose:** Reusable, standalone prompts for common development tasks

**Key Characteristics:**
- Task-oriented and action-focused
- Executed on-demand in Copilot Chat
- Include task-specific context and steps
- Define clear success criteria
- Work in agent mode for autonomous execution

**Example Use Cases:**
- Creating a Django project
- Initializing a database
- Setting up a new component
- Running a specific workflow

### Instruction Files

**Purpose:** Persistent guidelines that inform how Copilot works in specific contexts

**Key Characteristics:**
- Context-aware and path-specific
- Applied automatically when working in matching files
- Define standards, patterns, and conventions
- Provide implementation guidance
- Include code examples and best practices

**Example Use Cases:**
- Backend framework conventions
- Frontend component patterns
- Configuration standards
- API design guidelines

## When to Use What

### Use Prompt Files When:

✅ You have a **repeatable task** that needs to be executed multiple times
✅ The task has **clear, defined steps** that can be automated
✅ You want to ensure **consistent execution** of complex workflows
✅ The task requires **specific sequencing** of operations
✅ You need to **share standardized procedures** with the team

**Example:**
```markdown
Task: "Set up a new Django app with database connection"
Solution: Create a prompt file with step-by-step instructions
```

### Use Instruction Files When:

✅ You need to enforce **coding standards** and patterns
✅ You want to provide **ongoing guidance** for specific code areas
✅ You need to define **HOW things should be implemented**
✅ You want to ensure **consistency** across a codebase
✅ You need **context-specific rules** for different parts of the project

**Example:**
```markdown
Requirement: "All Django settings files must include Codespace URL handling"
Solution: Create an instruction file with the required pattern
```

### Use Both Together When:

🎯 You have a **task (prompt)** that should follow **specific patterns (instructions)**

**Example:**
```markdown
Prompt: "Create a new REST API endpoint"
    ↓
Instructions: "API endpoints must follow these URL patterns and include these authentication checks"
```

## File Structure Overview

### Repository Layout

```
.github/
├── prompts/                    # Prompt files for repeatable tasks
│   ├── create-django-project.prompt.md
│   ├── init-populate-octofit_db.prompt.md
│   └── update-octofit-tracker-app.prompt.md
│
└── instructions/               # Instruction files for persistent guidance
    ├── octofit_tracker_setup_project.instructions.md    # Global rules
    ├── octofit_tracker_django_backend.instructions.md   # Backend-specific
    └── octofit_tracker_react_frontend.instructions.md   # Frontend-specific
```

### Prompt File Anatomy

```markdown
---
mode: 'agent'                   # Execution mode
model: GPT-4.1                  # AI model to use
description: 'What this does'   # Brief description
---

# Environment Setup                # Context and prerequisites
- Existing resources
- Prerequisites

# Main Task                         # Core task definition
1. Step 1
2. Step 2
3. Step 3

# Verification                      # Success criteria
- How to verify
- Expected outcomes
```

### Instruction File Anatomy

```markdown
---
applyTo: "path/pattern/**"      # Which files this applies to
---

# Component Guidelines              # Title and context

## Specific Topic                   # Organized by topic
- Rule 1
- Rule 2

### Code Example                    # Concrete implementation
```language
code here
```

## Another Topic                    # Multiple topics
Requirements and patterns
```

## Best Practices

### 1. Separation of Concerns

**Do:**
- Prompts describe WHAT (the task goal)
- Instructions describe HOW (the implementation)
- Keep them focused and single-purpose

**Don't:**
- Mix task execution with coding standards
- Put implementation details in prompts
- Put task workflows in instructions

### 2. Naming Conventions

**Prompt Files:**
```
<action>-<object>.prompt.md

Examples:
- create-django-project.prompt.md
- setup-database.prompt.md
- deploy-application.prompt.md
```

**Instruction Files:**
```
<component>_<technology>.instructions.md

Examples:
- api_django_backend.instructions.md
- ui_react_frontend.instructions.md
- database_mongodb.instructions.md
```

### 3. Scope Appropriately

**Prompts:**
- One task per file
- Clear beginning and end
- Verifiable completion

**Instructions:**
- One area or component per file
- Related rules grouped together
- Applied by path pattern

### 4. Provide Examples

**Always include:**
- ✅ Code examples
- ✅ Command examples
- ✅ Configuration examples
- ✅ Expected outputs

### 5. Use Clear Language

**Prompts:**
- Use action verbs (Create, Setup, Initialize)
- Number sequential steps
- Be specific about resources

**Instructions:**
- Use directive language (Must, Should, Never)
- State requirements clearly
- Provide rationale when helpful

### 6. Keep It Maintainable

**Regular maintenance:**
- Review quarterly or when tools change
- Update examples to match current code
- Remove obsolete files
- Document changes in commits

## Examples

### Example 1: Project Setup

**Scenario:** Need to set up a new Python Django backend

**Prompt File:** `create-backend-app.prompt.md`
```markdown
---
mode: 'agent'
model: GPT-4.1
description: 'Create a new Django backend application'
---

# Environment Setup
- Use Python virtual environment in `backend/venv`
- Django and dependencies are pre-installed

# Task: Create Django App
1. Create Django app in `backend/` directory
2. Configure settings for development
3. Create initial database migrations
4. Verify app starts successfully

# Verification
- App directory structure created
- `manage.py` runs without errors
- Development server starts on port 8000
```

**Instruction File:** `backend_django.instructions.md`
```markdown
---
applyTo: "backend/**"
---
# Django Backend Guidelines

## Settings Configuration

Always include Codespace URL handling:

```python
import os
ALLOWED_HOSTS = ['localhost', '127.0.0.1']
if os.environ.get('CODESPACE_NAME'):
    ALLOWED_HOSTS.append(f"{os.environ.get('CODESPACE_NAME')}-8000.app.github.dev")
```

## Database Configuration

Always use Django ORM, not direct database scripts.
```

**How They Work Together:**
1. Developer runs: `/create-backend-app` in Copilot Chat
2. Copilot executes the prompt's task steps
3. While generating code, Copilot applies the backend instructions
4. Result: Django app created with correct URL handling pattern

### Example 2: API Endpoint Development

**Scenario:** Need to add new REST API endpoints

**Prompt File:** `add-rest-endpoint.prompt.md`
```markdown
---
mode: 'agent'
model: GPT-4.1
description: 'Add a new REST API endpoint to Django backend'
---

# Task: Add REST API Endpoint
1. Create model in `models.py`
2. Create serializer in `serializers.py`
3. Create view in `views.py`
4. Add route in `urls.py`
5. Test endpoint with curl

# Verification
- Endpoint returns 200 status
- Data serialization works correctly
- CRUD operations function properly
```

**Instruction File:** `backend_api.instructions.md`
```markdown
---
applyTo: "backend/**/api/**"
---
# API Development Guidelines

## Serializers

Must convert ObjectId fields to strings:

```python
class MySerializer(serializers.ModelSerializer):
    id = serializers.CharField(read_only=True)
```

## URL Patterns

Must use codespace-aware base URLs:

```python
import os
codespace_name = os.environ.get('CODESPACE_NAME')
base_url = f"https://{codespace_name}-8000.app.github.dev" if codespace_name else "http://localhost:8000"
```

## Testing

Use curl to test endpoints:
```bash
curl -X GET http://localhost:8000/api/endpoint/
```
```

### Example 3: Frontend Component Creation

**Scenario:** Need to create React components

**Prompt File:** `create-react-component.prompt.md`
```markdown
---
mode: 'agent'
model: GPT-4.1
description: 'Create a new React component with routing'
---

# Task: Create React Component
1. Create component file in `src/components/`
2. Add routing in `App.js`
3. Add navigation link
4. Test component renders

# Verification
- Component renders without errors
- Route works correctly
- Navigation link is functional
```

**Instruction File:** `frontend_react.instructions.md`
```markdown
---
applyTo: "frontend/**"
---
# React Frontend Guidelines

## Component Structure

Components should use functional components with hooks.

## Styling

Use Bootstrap CSS classes:
- Import at top of `index.js`: `import 'bootstrap/dist/css/bootstrap.min.css';`
- Use Bootstrap classes in components

## Routing

Use react-router-dom for navigation:

```javascript
import { BrowserRouter, Routes, Route } from 'react-router-dom';
```

## Images

Use images from `docs/` directory:
```javascript
import logo from '../docs/octofitapp-small.png';
```
```

## Workflow Integration

### Standard Development Workflow

1. **Start**: Open GitHub Copilot Chat in VS Code
2. **Select Mode**: Choose "Agent" from dropdown
3. **Run Prompt**: Type `/prompt-name` to execute a prompt file
4. **Auto-Apply Instructions**: Instructions automatically apply during code generation
5. **Review**: Check generated code follows standards
6. **Iterate**: Refine with additional prompts if needed

### Team Collaboration Workflow

1. **Create Standards**: Document patterns in instruction files
2. **Create Procedures**: Document tasks in prompt files
3. **Share Knowledge**: Commit files to repository
4. **Enable Team**: Everyone uses same prompts and standards
5. **Maintain Together**: Update files as project evolves

## Tips for Success

### ✅ Do's

- Keep prompts focused on one task
- Keep instructions focused on one area/technology
- Provide concrete code examples
- Use clear, directive language
- Test before committing
- Update regularly
- Document the "why" when helpful

### ❌ Don'ts

- Mix task steps with coding patterns
- Create overly broad instructions
- Use vague or ambiguous language
- Forget to include verification steps
- Let files become outdated
- Create duplicate or conflicting rules
- Over-constrain Copilot's flexibility

## Troubleshooting

### Prompt Not Working

**Check:**
- ✓ Front matter YAML is valid
- ✓ File is in `.github/prompts/` directory
- ✓ File name ends with `.prompt.md`
- ✓ Mode is set to `'agent'`
- ✓ Steps are clear and actionable

### Instructions Not Applied

**Check:**
- ✓ Front matter YAML is valid
- ✓ File is in `.github/instructions/` directory
- ✓ File name ends with `.instructions.md`
- ✓ `applyTo` path matches target files
- ✓ No conflicting instructions in other files

### Copilot Behavior Unexpected

**Try:**
- ✓ Review both prompts and instructions for conflicts
- ✓ Make instructions more specific with examples
- ✓ Add verification steps to prompts
- ✓ Test in isolation (disable other customizations)
- ✓ Check Copilot logs for errors

## Additional Resources

### Detailed Documentation

- [Prompt File Standards](./github-copilot-prompt-standards.md) - Complete guide to prompt files
- [Instruction File Standards](./github-copilot-instruction-standards.md) - Complete guide to instruction files

### Official Documentation

- [VS Code: Prompt Files](https://code.visualstudio.com/docs/copilot/customization/overview#_prompt-files)
- [VS Code: Custom Instructions](https://code.visualstudio.com/docs/copilot/customization/overview#_custom-instructions)
- [GitHub Copilot Documentation](https://docs.github.com/en/copilot)
- [Copilot Agent Mode](https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode)

### Repository Resources

- Existing prompt files: `.github/prompts/`
- Existing instruction files: `.github/instructions/`
- Example implementations in `octofit-tracker/` directory

---

**Version:** 1.0  
**Last Updated:** November 2025  
**Maintained By:** Development Team
