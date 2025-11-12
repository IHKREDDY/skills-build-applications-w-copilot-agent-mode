# GitHub Copilot Instruction File Standards

## Overview

Instruction files (also called custom instructions) provide context-specific guidelines that GitHub Copilot uses when generating code or executing tasks. Unlike prompt files that define WHAT to do, instruction files define HOW things should be done. This document outlines the standards and best practices for creating instruction files in this repository.

## File Location

All instruction files should be stored in:
```
.github/instructions/
```

## File Naming Convention

Instruction files should follow this naming pattern:
```
<component-or-area>_<technology>.instructions.md
```

**Examples:**
- `octofit_tracker_setup_project.instructions.md`
- `octofit_tracker_django_backend.instructions.md`
- `octofit_tracker_react_frontend.instructions.md`

## File Structure

### Required Front Matter

Every instruction file must start with YAML front matter containing metadata:

```yaml
---
applyTo: "<path-pattern>"
---
```

**Front Matter Fields:**

- **applyTo**: Defines which files or directories these instructions apply to
  - Use glob patterns to match multiple files/directories
  - `"**"` - Applies to all files in the repository
  - `"octofit-tracker/**"` - Applies to all files under octofit-tracker directory
  - `"octofit-tracker/backend/**"` - Applies only to backend files
  - Required field

**Examples:**
```yaml
---
applyTo: "**"
---
# Global instructions for entire project
```

```yaml
---
applyTo: "octofit-tracker/backend/**"
---
# Instructions specific to backend code
```

### Instruction Content Structure

After the front matter, organize your instructions using these guidelines:

#### 1. Title and Purpose
```markdown
# <Component Name> Guidelines

Brief description of what these instructions cover.
```

#### 2. High-Level Goals (if applicable)
```markdown
## Goals and Overview

Explain what the component/feature should accomplish:
- Goal 1
- Goal 2
- Goal 3
```

#### 3. Specific Rules and Guidelines

Organize by topic using level 2 headings (`##`):

```markdown
## Configuration Rules

Description of what should be configured and why.

### Subsection (if needed)

Specific details or examples.
```

#### 4. Code Examples

Provide concrete examples of correct implementations:

````markdown
## Example Configuration

Should always contain the following:

```python
import os
ALLOWED_HOSTS = ['localhost', '127.0.0.1']
if os.environ.get('CODESPACE_NAME'):
    ALLOWED_HOSTS.append(f"{os.environ.get('CODESPACE_NAME')}-8000.app.github.dev")
```
````

## Best Practices

### 1. Be Prescriptive, Not Descriptive
- State what MUST/SHOULD be done
- Use imperative language
- Provide specific requirements

**Good Example:**
```markdown
## Directory Structure

Never change directories when running commands. Instead, point to the directory when issuing commands.
```

**Bad Example:**
```markdown
## Directory Structure

It's better if you don't change directories.
```

### 2. Use Clear Directive Language

Use these terms consistently:
- **Must** / **Always** - Absolute requirements
- **Should** - Strong recommendations
- **Never** - Absolute prohibitions
- **Do not** - Strong prohibitions

**Examples:**
```markdown
- Always use `ps aux | grep mongod` for checking for mongod running
- Never change directories when agent mode is running commands
- Should always contain the following configuration
```

### 3. Provide Concrete Examples

Always include code examples for:
- Configuration patterns
- Required imports
- Expected structures
- Correct implementations

**Example:**
````markdown
## URL Configuration

Should always use the codespace environment variable for the URL:

```python
import os
codespace_name = os.environ.get('CODESPACE_NAME')
if codespace_name:
    base_url = f"https://{codespace_name}-8000.app.github.dev"
else:
    base_url = "http://localhost:8000"
```
````

### 4. Specify Tools and Commands

Be explicit about:
- Which tools to use
- Command syntax
- Command options
- Working directories

**Example:**
```markdown
## MongoDB Service

- always use `ps aux | grep mongod` for checking for mongod running
- mongodb-org is the official MongoDB package
- mongosh is the official client tool
- Always use Django's ORM, not direct MongoDB scripts to create the database structure and data
```

### 5. Define Project Structure

Clearly document:
- Directory hierarchies
- Required files
- File locations
- Naming conventions

**Example:**
```markdown
## Project Structure

The section defines the OctoFit Tracker App's structure:

```text
octofit-tracker/
├── backend/
│   ├── venv/
│   ├── octofit_tracker/
└── frontend/
```
```

### 6. Include Environment-Specific Guidance

Address different environments:
- Local development
- Codespaces
- CI/CD environments
- Production considerations

**Example:**
```markdown
## Forwarded Ports

- 8000: public
- 3000: public
- 27017: private

Do not propose any other ports to forward or to make public
```

### 7. Provide Installation Instructions

When relevant, include:
- Package lists
- Version specifications
- Installation commands
- Virtual environment setup

**Example:**
````markdown
## Required Packages

Create file octofit-tracker/backend/requirements.txt:

```text
Django==4.1.7
djangorestframework==3.14.0
django-cors-headers==4.5.0
```

Install with:

```bash
source octofit-tracker/backend/venv/bin/activate 
pip install -r octofit-tracker/backend/requirements.txt
```
````

## Scope Guidelines

### Global Instructions (`applyTo: "**"`)

Use for:
- Project-wide conventions
- Overall architecture rules
- Common patterns across all code
- General development practices

**Example topics:**
- Project goals and purpose
- Directory structure standards
- Environment setup
- Port configurations
- Tool preferences

### Component-Specific Instructions

Use for:
- Technology-specific guidelines (Django, React, etc.)
- Framework conventions
- Component-level patterns
- Implementation details

**Example topics:**
- Backend configuration patterns
- Frontend component structure
- API design rules
- Database interaction patterns

## Integration with Prompt Files

Instruction files complement prompt files:

- **Instruction Files** (`*.instructions.md`): Define HOW (implementation details, patterns, standards)
- **Prompt Files** (`*.prompt.md`): Define WHAT (tasks to accomplish)

**Relationship:**
```
Prompt: "Create a Django project"
    ↓
Instruction: "Django projects should always include these settings..."
```

## Example Template

Here's a complete template for creating new instruction files:

```markdown
---
applyTo: "<path-pattern>"
---
# <Component/Area> Guidelines

Brief description of what these instructions cover.

## Goals and Overview (optional)

High-level goals:
- Goal 1
- Goal 2

## <Topic 1>

Clear, prescriptive guidance about this topic.

### Specific Rule

- Always do X
- Never do Y
- Should include Z

## <Topic 2>

### Code Example

Should always contain the following:

```language
code example here
```

## <Topic 3>

Detailed requirements:

1. First requirement
2. Second requirement
3. Third requirement

## Tool Specifications (if applicable)

- Use tool X for purpose Y
- Command syntax: `command --option`
- Expected behavior
```

## Common Patterns

### Pattern 1: Project Setup Instructions
**Scope:** Global (`applyTo: "**"`)

**Content:**
- Project goals
- Directory structure
- Environment requirements
- Tool specifications
- Port configurations

### Pattern 2: Backend Framework Instructions
**Scope:** Backend-specific (`applyTo: "octofit-tracker/backend/**"`)

**Content:**
- Framework configuration
- Database patterns
- API structure
- Serialization rules
- URL patterns

### Pattern 3: Frontend Framework Instructions
**Scope:** Frontend-specific (`applyTo: "octofit-tracker/frontend/**"`)

**Content:**
- Component structure
- Styling guidelines
- Routing patterns
- State management
- Asset locations

## Writing Style Guidelines

### Use Action-Oriented Headers
```markdown
## Creating the Virtual Environment
## Configuring Django Settings
## Installing Dependencies
```

### Use Lists for Multiple Items
```markdown
Should always contain the following:
- Item 1
- Item 2
- Item 3
```

### Use Code Blocks for Technical Content
````markdown
```bash
command here
```

```python
code here
```

```text
configuration here
```
````

### Use Blockquotes for Notes
```markdown
> Note: This is an important consideration
```

## Testing Instruction Files

Before committing new instruction files:

1. Place file in `.github/instructions/` directory
2. Test with related prompt files
3. Verify Copilot follows the instructions correctly
4. Check for conflicts with other instruction files
5. Ensure path patterns in `applyTo` are correct
6. Validate YAML front matter syntax

## Maintenance

### Regular Reviews
- Update when tools/frameworks change versions
- Revise when patterns evolve
- Remove outdated practices
- Add new patterns as they emerge

### Version Control
- Document significant changes in commit messages
- Reference related PR or issue numbers
- Note which prompts are affected by changes

### Consistency Checks
- Ensure terminology is consistent across files
- Verify examples still work
- Confirm paths and commands are accurate
- Check that instructions don't contradict each other

## Troubleshooting Common Issues

### Copilot Not Following Instructions

**Possible causes:**
- `applyTo` pattern doesn't match target files
- Instructions are too vague
- Conflicting instructions in multiple files
- Missing code examples

**Solutions:**
- Make path patterns more specific
- Add concrete code examples
- Use stronger directive language (must/always/never)
- Check for instruction conflicts

### Instructions Too Restrictive

**Symptoms:**
- Copilot can't complete tasks
- Repeated errors or failures
- Excessive back-and-forth

**Solutions:**
- Provide alternative approaches
- Allow flexibility where appropriate
- Include troubleshooting guidance
- Add escape clauses for edge cases

## Additional Resources

- [VS Code Docs: Custom Instructions](https://code.visualstudio.com/docs/copilot/customization/overview#_custom-instructions)
- [GitHub Copilot Documentation](https://docs.github.com/en/copilot)
- Repository prompt files in `.github/prompts/`
- VS Code Copilot settings documentation
