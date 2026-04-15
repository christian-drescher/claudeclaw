---
name: create-skill
description: Create new skills. Use when users ask to create a skill, add a skill, make a new command, build a skill, add a slash command, create a plugin skill, or define a new automation. Trigger phrases include "create a skill", "new skill", "add a skill", "make a command", "build a skill", "I want a skill that", "add slash command", "create automation".
---

# Create Skill

Create new skills. Use `$ARGUMENTS` to determine what the user wants.

## Skill File Format

A skill is a `SKILL.md` file inside a `skills/<skill-name>/` directory. It uses YAML frontmatter:

```markdown
---
name: my-skill
description: Short description of when to trigger this skill. Include trigger phrases so the agent knows when to activate it.
---

# Skill Title

Instructions for what the agent should do when this skill is triggered.
```

### Key rules for SKILL.md:
- **name**: lowercase, kebab-case (e.g. `my-skill`)
- **description**: must include trigger phrases and keywords so the agent knows when to use it
- The body contains the full instructions the agent will follow when the skill is invoked

## Scope

Skills must be created at workspace level:
- Location: `<workspace-root>/skills/<skill-name>/SKILL.md`
- No special permissions needed

## Steps

1. Ask the user conversationally what the skill should do, and what name they want. Suggest ideas based on context.

2. Based on their answers, generate the `SKILL.md` content:
   - Write a clear, descriptive `name` in kebab-case
   - Write a `description` with plenty of trigger phrases so the agent knows when to activate it
   - Write detailed body instructions for what the agent should do

3. Create the skill:
   - **Workspace level**: Write to `skills/<skill-name>/SKILL.md` relative to workspace root

4. Confirm creation and show the user:
   - The skill name and path
   - How to invoke it: `/<plugin-name>:<skill-name>` or just by asking naturally (the agent auto-triggers based on description)
   - Remind them the skill is available immediately — no restart needed
