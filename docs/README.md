# Documentation

This directory contains documentation for the OctoFit Tracker application and GitHub Copilot customization standards.

## GitHub Copilot Standards Documentation

Comprehensive guides for customizing GitHub Copilot in this repository:

### 📘 [GitHub Copilot Customization Guide](./github-copilot-customization-guide.md)
**Start here!** Complete overview of the customization system with quick reference guide, examples, and best practices. This guide ties together both prompt files and instruction files.

**What you'll learn:**
- Understanding the customization system
- When to use prompt files vs instruction files
- Best practices for both
- Complete workflow examples
- Troubleshooting guide

### 📗 [Prompt File Standards](./github-copilot-prompt-standards.md)
Detailed standards for creating prompt files that define **WHAT** tasks to accomplish.

**What you'll learn:**
- Prompt file structure and format
- Front matter requirements
- Content organization patterns
- Best practices for task definition
- Integration with instruction files
- Complete template and examples

### 📙 [Instruction File Standards](./github-copilot-instruction-standards.md)
Detailed standards for creating instruction files that define **HOW** tasks should be implemented.

**What you'll learn:**
- Instruction file structure and format
- Path-based scoping with `applyTo`
- Writing prescriptive guidelines
- Providing code examples
- Common patterns and use cases
- Complete template and examples

## Quick Start

1. **New to Copilot customization?**  
   Start with [GitHub Copilot Customization Guide](./github-copilot-customization-guide.md)

2. **Want to create a new prompt file?**  
   See [Prompt File Standards](./github-copilot-prompt-standards.md)

3. **Want to create new coding standards?**  
   See [Instruction File Standards](./github-copilot-instruction-standards.md)

4. **Looking for examples?**  
   Check the existing files:
   - Prompts: `.github/prompts/`
   - Instructions: `.github/instructions/`

## Application Documentation

### 📖 [OctoFit Story](./octofit_story.md)
The story and background for the OctoFit Tracker fitness application.

### 🖼️ [Application Logo](./octofitapp-small.png)
OctoFit Tracker application logo image.

## Key Concepts

### Prompt Files
- **Location:** `.github/prompts/`
- **Purpose:** Define repeatable tasks
- **Usage:** Run with `/prompt-name` in Copilot Chat
- **Focus:** WHAT to accomplish

### Instruction Files
- **Location:** `.github/instructions/`
- **Purpose:** Define coding standards and patterns
- **Usage:** Applied automatically based on file context
- **Focus:** HOW to implement

### Working Together
```
Prompt File (WHAT)
    ↓
  Task Definition
    ↓
Copilot Agent Mode Execution
    ↓
Instruction File (HOW)
    ↓
  Implementation Standards
    ↓
  Code Generation
```

## File Organization

```
docs/
├── README.md                                      # This file
├── github-copilot-customization-guide.md         # Overview guide (start here)
├── github-copilot-prompt-standards.md            # Prompt file standards
├── github-copilot-instruction-standards.md       # Instruction file standards
├── octofit_story.md                              # Application story
└── octofitapp-small.png                          # Application logo
```

## Additional Resources

### In This Repository
- **Prompt Examples:** `.github/prompts/`
- **Instruction Examples:** `.github/instructions/`
- **Exercise Steps:** `.github/steps/`

### External Resources
- [VS Code Copilot Documentation](https://code.visualstudio.com/docs/copilot)
- [GitHub Copilot Documentation](https://docs.github.com/en/copilot)
- [Copilot Agent Mode](https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode)
- [Prompt Files Guide](https://code.visualstudio.com/docs/copilot/customization/overview#_prompt-files)
- [Custom Instructions Guide](https://code.visualstudio.com/docs/copilot/customization/overview#_custom-instructions)

## Contributing

When adding new documentation:

1. Follow the established format and style
2. Include practical examples
3. Keep language clear and directive
4. Update this README with links to new docs
5. Test any code examples before committing

## Questions?

If you have questions about these standards or need clarification:

1. Review the detailed guides linked above
2. Check existing prompt and instruction files for examples
3. See the exercise steps in `.github/steps/` for usage context
4. Open an issue with specific questions

---

**Last Updated:** November 2025
