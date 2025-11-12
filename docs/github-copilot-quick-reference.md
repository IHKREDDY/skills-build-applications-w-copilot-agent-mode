# GitHub Copilot Standards Quick Reference

## 📋 Cheat Sheet

### Prompt Files vs Instruction Files

| Aspect | Prompt Files | Instruction Files |
|--------|--------------|-------------------|
| **Purpose** | Define tasks (WHAT) | Define standards (HOW) |
| **Location** | `.github/prompts/` | `.github/instructions/` |
| **Extension** | `.prompt.md` | `.instructions.md` |
| **Usage** | `/prompt-name` in Copilot Chat | Auto-applied by context |
| **When to use** | Repeatable tasks | Coding standards |
| **Scope** | Single execution | Persistent guidance |

---

## 📝 Prompt File Quick Reference

### Naming Pattern
```
<action>-<object>.prompt.md
```

### Required Front Matter
```yaml
---
mode: 'agent'
model: GPT-4.1
description: 'Brief description'
---
```

### Basic Structure
```markdown
# Environment Setup
- Prerequisites
- Existing resources

# Task Name
1. Step 1
2. Step 2
3. Step 3

# Verification
- Success criteria
- Expected outputs
```

### Key Principles
- ✅ Focus on WHAT to accomplish
- ✅ Clear sequential steps
- ✅ Include verification
- ❌ Don't specify HOW (leave to instructions)
- ❌ Don't include implementation details

---

## 📐 Instruction File Quick Reference

### Naming Pattern
```
<component>_<technology>.instructions.md
```

### Required Front Matter
```yaml
---
applyTo: "path/pattern/**"
---
```

### Basic Structure
```markdown
# Component Guidelines

## Topic 1
- Rule 1
- Rule 2

### Code Example
```language
code here
```

## Topic 2
Requirements and patterns
```

### Key Principles
- ✅ Focus on HOW to implement
- ✅ Use directive language (must/should/never)
- ✅ Provide code examples
- ❌ Don't include task workflows
- ❌ Don't be vague

### Common applyTo Patterns
```yaml
applyTo: "**"                        # Global (all files)
applyTo: "backend/**"                # Backend only
applyTo: "frontend/**"               # Frontend only
applyTo: "backend/api/**"            # Specific subdirectory
```

---

## 🎯 Decision Tree: Which Should I Create?

```
Do I have a repeatable task to automate?
│
├─ YES → Create a PROMPT FILE
│         Examples: Creating a component, setting up a service,
│                  running a workflow, initializing a database
│
└─ NO → Do I need to enforce coding standards?
         │
         ├─ YES → Create an INSTRUCTION FILE
         │         Examples: Configuration patterns, API design rules,
         │                  code style, framework conventions
         │
         └─ NO → Do I need both?
                  │
                  └─ YES → Create BOTH!
                            Prompt defines the task
                            Instructions define the standards

```

---

## 💡 Common Use Cases

### Use Case 1: Setting Up New Component

**Create both:**
- **Prompt:** `create-api-endpoint.prompt.md` - Steps to create endpoint
- **Instruction:** `api_backend.instructions.md` - How endpoints should be structured

### Use Case 2: Enforcing Standards

**Create instruction only:**
- **Instruction:** `frontend_styling.instructions.md` - CSS/styling rules

### Use Case 3: Automation Task

**Create prompt only:**
- **Prompt:** `deploy-application.prompt.md` - Deployment steps

---

## 📖 Example Files in This Repository

### Prompt Files (`.github/prompts/`)
- `create-django-project.prompt.md` - Create Django project
- `init-populate-octofit_db.prompt.md` - Initialize database
- `update-octofit-tracker-app.prompt.md` - Update app files

### Instruction Files (`.github/instructions/`)
- `octofit_tracker_setup_project.instructions.md` - Global setup rules
- `octofit_tracker_django_backend.instructions.md` - Backend standards
- `octofit_tracker_react_frontend.instructions.md` - Frontend standards

---

## 🚀 Quick Start

### To Use a Prompt
1. Open Copilot Chat in VS Code
2. Select "Agent" mode
3. Type: `/prompt-name`
4. Press Enter

### To Create a Prompt
1. Create file in `.github/prompts/`
2. Name: `<action>-<object>.prompt.md`
3. Add front matter with mode and model
4. Write task steps
5. Add verification steps

### To Create Instructions
1. Create file in `.github/instructions/`
2. Name: `<component>_<tech>.instructions.md`
3. Add front matter with applyTo pattern
4. Write prescriptive guidelines
5. Include code examples

---

## 🔍 Testing Your Files

### Test a Prompt
```
1. Save the prompt file
2. Open Copilot Chat
3. Switch to Agent mode
4. Run: /your-prompt-name
5. Verify it executes correctly
```

### Test an Instruction
```
1. Save the instruction file
2. Open a file matching applyTo pattern
3. Ask Copilot to generate code
4. Verify it follows your instructions
```

---

## ⚠️ Common Mistakes

### Prompt Files
- ❌ Including implementation details (use instructions instead)
- ❌ No verification steps
- ❌ Vague task descriptions
- ❌ Missing front matter
- ✅ Focus on task goals and steps

### Instruction Files
- ❌ Including task workflows (use prompts instead)
- ❌ No code examples
- ❌ Wrong applyTo path pattern
- ❌ Vague requirements
- ✅ Focus on patterns and standards

---

## 📚 Full Documentation

For complete details, see:
- [GitHub Copilot Customization Guide](./github-copilot-customization-guide.md)
- [Prompt File Standards](./github-copilot-prompt-standards.md)
- [Instruction File Standards](./github-copilot-instruction-standards.md)

---

## 🔗 Quick Links

### Official Documentation
- [VS Code: Prompt Files](https://code.visualstudio.com/docs/copilot/customization/overview#_prompt-files)
- [VS Code: Custom Instructions](https://code.visualstudio.com/docs/copilot/customization/overview#_custom-instructions)
- [Copilot Agent Mode](https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode)

### In This Repository
- Prompt examples: `.github/prompts/`
- Instruction examples: `.github/instructions/`
- Exercise steps: `.github/steps/`

---

**Print this for quick reference!** 📄
