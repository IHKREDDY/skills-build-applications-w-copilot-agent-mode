# GitHub Copilot Prompt File Standards

## Overview

Prompt files are reusable, standalone prompts that you can run directly in GitHub Copilot Chat. They allow you to define common and repeatable development tasks in a Markdown file format. This document outlines the standards and best practices for creating prompt files in this repository.

## File Location

All prompt files should be stored in:
```
.github/prompts/
```

## File Naming Convention

Prompt files should follow this naming pattern:
```
<task-description>.prompt.md
```

**Examples:**
- `create-django-project.prompt.md`
- `init-populate-octofit_db.prompt.md`
- `update-octofit-tracker-app.prompt.md`

## File Structure

### Required Front Matter

Every prompt file must start with YAML front matter containing metadata:

```yaml
---
mode: 'agent'
model: GPT-4.1
description: '<Brief description of what this prompt does>'
---
```

**Front Matter Fields:**

- **mode**: Specifies the execution mode
  - `'agent'` - For autonomous agent mode execution
  - Required for all prompt files in this repository

- **model**: Specifies the AI model to use
  - `GPT-4.1` - Standard model for complex tasks
  - Required field

- **description**: Brief, clear description of the prompt's purpose
  - Should be concise (one sentence)
  - Describes what the prompt accomplishes
  - Required field

### Prompt Content Structure

After the front matter, organize your prompt content using these guidelines:

#### 1. Environment Setup (if applicable)
```markdown
# Environment Setup
- List existing resources to use
- Specify what NOT to create
- Define activation commands
- Identify required tools
```

#### 2. Main Task Description
```markdown
# <Task Name>
1. Step-by-step instructions
2. Each step should be clear and actionable
3. Use numbered lists for sequential tasks
4. Use bullet points for requirements or notes
```

#### 3. Configuration Details (if applicable)
```markdown
## Configuration
- Specific settings to apply
- Files to modify
- Variables to set
```

#### 4. Verification Steps
```markdown
# Verification
- How to verify the task completed successfully
- Expected outcomes
- Commands to run for validation
```

## Best Practices

### 1. Focus on WHAT, Not HOW
- Prompts should describe **what** needs to be accomplished
- The **how** (implementation details) should be in instruction files
- Let Copilot agent mode determine the specific commands

**Good Example:**
```markdown
Create a Django project in the octofit-tracker/backend directory
```

**Bad Example:**
```markdown
Run: cd octofit-tracker/backend && django-admin startproject myapp
```

### 2. Be Specific About Context
- Reference existing resources explicitly
- Specify directory paths
- Mention prerequisite states

**Example:**
```markdown
# Environment Setup
- Use the existing Python virtual environment in `octofit-tracker/backend/venv`
- Do not create a new Python virtual environment
- The Django project is in `octofit-tracker/backend/octofit_tracker`
```

### 3. Use Clear Sequential Steps
- Number steps that must be done in order
- Use sub-steps (a, b, c) for related actions
- Be explicit about dependencies

**Example:**
```markdown
1. Ensure the MongoDB service is running
2. Configure Django in `settings.py` to connect to the `octofit_db` database
3. Run `makemigrations` and `migrate` in the Python virtual environment
```

### 4. Provide Clear Success Criteria
- Include verification steps
- Specify expected outputs
- Define what "done" looks like

**Example:**
```markdown
# Verification
- After population, verify with `mongosh` that the `octofit_db` database contains the correct collections and test data
- Confirm Django REST API endpoints are available for all collections
```

### 5. Include Notes and Warnings
- Use blockquotes for important information
- Highlight critical steps
- Warn about common pitfalls

**Example:**
```markdown
> [!NOTE]
> - Wait a moment for Copilot to respond and press the Continue button
> - Keep files created and updated by Copilot agent mode until it is finished

> [!IMPORTANT]
> - Don't start the Python Django app automatically
```

## Integration with Instruction Files

Prompt files work in conjunction with instruction files:

- **Prompt Files** (`*.prompt.md`): Define WHAT tasks to accomplish
- **Instruction Files** (`*.instructions.md`): Define HOW tasks should be implemented

When creating prompt files, reference related instruction files:
```markdown
Follow the instructions in the Django backend guidelines for configuration details
```

## Usage in Copilot Chat

To use a prompt file in GitHub Copilot Chat:

1. Open Copilot Chat in VS Code
2. Select "Agent" mode from the dropdown
3. Type `/` followed by the prompt file name (without `.prompt.md`)

**Example:**
```
/create-django-project
```

## Example Template

Here's a complete template for creating new prompt files:

```markdown
---
mode: 'agent'
model: GPT-4.1
description: '<One sentence describing what this prompt does>'
---

# Environment Setup (if applicable)
- List existing resources
- Specify constraints
- Define prerequisites

# <Main Task Name>
1. First step with clear action
2. Second step with clear action
3. Third step with clear action
   a. Sub-step if needed
   b. Another sub-step

# Configuration (if applicable)
- Setting 1
- Setting 2
- Setting 3

# Verification
- How to verify success
- Expected outcomes
- Validation commands
```

## Common Patterns

### Pattern 1: Project Setup Prompts
Used for initializing projects or major components.

**Characteristics:**
- References existing virtual environments or tools
- Creates directory structures
- Installs dependencies
- Basic configuration

### Pattern 2: Database/Backend Prompts
Used for setting up databases and backend services.

**Characteristics:**
- Ensures services are running
- Configures connections
- Creates schemas/models
- Populates test data
- Includes verification steps

### Pattern 3: Component Update Prompts
Used for modifying existing components.

**Characteristics:**
- Lists specific files to update
- Describes changes needed
- Maintains existing functionality
- Focuses on incremental changes

## Testing Prompt Files

Before committing a new prompt file:

1. Test it in GitHub Copilot Chat agent mode
2. Verify it produces the expected results
3. Check that it doesn't conflict with existing instructions
4. Ensure all referenced files and paths exist
5. Validate the front matter is properly formatted

## Maintenance

- Review prompt files regularly for accuracy
- Update when underlying tools or structures change
- Remove or archive obsolete prompts
- Keep descriptions current

## Additional Resources

- [VS Code Docs: Prompt Files](https://code.visualstudio.com/docs/copilot/customization/overview#_prompt-files)
- [GitHub Copilot Documentation](https://docs.github.com/en/copilot)
- Repository instruction files in `.github/instructions/`
