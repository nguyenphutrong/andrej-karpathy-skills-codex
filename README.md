# Andrej Karpathy Skills For Codex

This repository packages Karpathy-inspired coding guidelines as a Codex skill and a Codex plugin. It is designed for Codex CLI and the Codex app, with one canonical skill source under `.agents/skills/`.

This Codex-first port is based on the original repository [forrestchang/andrej-karpathy-skills](https://github.com/forrestchang/andrej-karpathy-skills).

The guidelines target four common failure modes in coding agents:
- hidden assumptions
- overengineering
- broad, unnecessary edits
- weak or missing verification criteria

## What This Repo Contains

- Repo-scoped skill at `.agents/skills/karpathy-guidelines/`
- Codex plugin manifest at `.codex-plugin/plugin.json`
- Repo marketplace at `.agents/plugins/marketplace.json`
- Worked examples in `EXAMPLES.md`

The skill name is `karpathy-guidelines`, so you can invoke it directly with `$karpathy-guidelines`.

## The Four Principles

### 1. Think Before Coding

Don't assume. Surface ambiguity, tradeoffs, and confusion before implementation.

### 2. Simplicity First

Prefer the minimum code that solves the actual request. Avoid speculative abstractions.

### 3. Surgical Changes

Touch only what the task requires. Avoid drive-by refactors and unrelated cleanup.

### 4. Goal-Driven Execution

Turn vague tasks into concrete, verifiable success criteria and loop until verified.

## Use As A Repo-Scoped Skill

Codex automatically scans `.agents/skills` from the current working directory up to the repo root.

1. Clone this repository.
2. Open Codex at the repository root.
3. Open the skill picker with `/skills` or type `$`.
4. Invoke `$karpathy-guidelines` explicitly, or let Codex match it implicitly from the task.

This is the simplest way to use the guidelines while working inside this repository.

## Install As A Local Codex Plugin

This repository also acts as its own plugin root. The local marketplace entry already lives at `.agents/plugins/marketplace.json`.

To test it in Codex:

1. Open Codex with this repository as the active repo.
2. Restart Codex so it reloads the repo marketplace.
3. Open the plugin directory.
4. Select the repo marketplace named `Andrej Karpathy Local Plugins`.
5. Install `andrej-karpathy-skills`.

After installation, the packaged skill should be available in Codex App alongside any repo-scoped discovery.

## Verify The Port

Static checks you can run locally:

```bash
python3 - <<'PY'
import json
from pathlib import Path

for path in [
    Path(".codex-plugin/plugin.json"),
    Path(".agents/plugins/marketplace.json"),
]:
    json.loads(path.read_text())
    print(f"ok: {path}")
PY
```

```bash
ruby -e 'require "yaml"; YAML.load_file(".agents/skills/karpathy-guidelines/agents/openai.yaml"); puts "ok: .agents/skills/karpathy-guidelines/agents/openai.yaml"'
```

Interactive smoke checks:

1. Confirm `$karpathy-guidelines` appears in `/skills` when Codex opens this repo.
2. Confirm the plugin appears in the repo marketplace and installs successfully.
3. Confirm the skill metadata shown in Codex App matches the plugin and skill descriptions.

## References

- [Codex skills docs](https://developers.openai.com/codex/skills.md)
- [Codex plugin build docs](https://developers.openai.com/codex/plugins/build.md)
- [Examples](./EXAMPLES.md)

## License

MIT
