# Superpowers for Hermes Agent

Superpowers can be installed as a Hermes Agent plugin. The plugin registers the bundled skills under the `superpowers:` namespace and injects the `using-superpowers` bootstrap through Hermes' `pre_llm_call` plugin hook.

## Install

```bash
hermes plugins install https://github.com/obra/superpowers
```

Restart Hermes after installing so the plugin is loaded.

## Local development

From a checkout of this repository, install via a local Git URL:

```bash
hermes plugins install file:///path/to/superpowers
```

Then start a clean Hermes session and run the acceptance test prompt:

```text
Let's make a react todo list
```

A working installation loads the Superpowers bootstrap automatically and invokes `superpowers:brainstorming` before writing code.

## How it works

- `plugin.yaml` declares a Hermes plugin with a `pre_llm_call` hook.
- `__init__.py` registers every bundled `skills/*/SKILL.md` with Hermes as a read-only plugin skill.
- The hook injects the `using-superpowers` bootstrap and `skills/using-superpowers/references/hermes-tools.md` into each LLM turn.
- The tool mapping tells Hermes to load skills with plugin-qualified names such as `skill_view(name="superpowers:brainstorming")`.

The plugin does not copy files into `~/.hermes/skills/` and does not edit user config. Everything is delivered through Hermes' plugin install mechanism.
