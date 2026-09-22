# claude-skills

Personal [Claude Code](https://code.claude.com) skills, published as a plugin marketplace.

## spec-workflow

Two skills that split feature work into "decide what to build" and "decide how to build it",
each in its own session.

| Command | What it does |
| --- | --- |
| `/spec-new <feature name>` | Interviews you — scope, behaviour, data and interfaces, edge cases, errors, non-goals — then writes a specification to `docs/specs/NNN-<slug>.md` (or wherever the project keeps its specs). WHAT and WHY only, always in English, ending in acceptance criteria with an end-to-end verification step. |
| `/spec-plan <number, slug or path>` | Reads that specification, reads the code it touches, and produces an implementation plan for it. |

Both are invoked explicitly only — Claude never loads them on its own.

## Install

```
/plugin marketplace add brueggern/claude-skills
/plugin install spec-workflow@claude-skills
```

## Local development

Clone the repo and symlink the skills into `~/.claude/skills/` instead of installing the
plugin — then editing a `SKILL.md` takes effect immediately, and the skill is versioned by
this repo:

```sh
git clone git@github.com:brueggern/claude-skills.git ~/.agents/claude-skills
ln -s ../../.agents/claude-skills/plugins/spec-workflow/skills/spec-new  ~/.claude/skills/spec-new
ln -s ../../.agents/claude-skills/plugins/spec-workflow/skills/spec-plan ~/.claude/skills/spec-plan
```

Do one or the other, not both — symlinking *and* installing the plugin registers each command
twice.

## License

MIT
