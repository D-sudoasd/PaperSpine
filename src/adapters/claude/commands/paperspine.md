---
allowed-tools: Bash(powershell:*), Bash(powershell.exe:*), Bash(pwsh:*), Bash(cmd:*), Bash(bash:*), Bash(sh:*), Bash(chmod:*)
description: Start PaperSpine with resumable, host-compatible intake
---

Start the PaperSpine workflow for the current project.

If `paper_rewriting_output/paper_spine_config.json` is missing or incomplete,
route through the `paper-spine` skill, inspect the existing progress, and use a
host-permitted intake path. A valid existing configuration may be reused. The
bundled intake UI is optional: launch it once when the installed launcher is
available, otherwise use the concise numbered/text fallback for the missing
fields. Do not ask the user to hand-write JSON. If the configuration remains
missing after the permitted intake attempt, leave the intake gate pending and
report what is still needed; do not infer approval from a timeout or an
unfinished UI window. Motivation, contribution, and other author gates remain
explicit decisions.

## Platform-specific launcher

### Windows

```powershell
$config = Join-Path (Get-Location) "paper_rewriting_output\paper_spine_config.json"
$launcher = Join-Path $env:USERPROFILE ".claude\skills\paper-spine\scripts\launch_paperspine_ui.ps1"
if (-not (Test-Path -LiteralPath $launcher)) {
  throw "PaperSpine UI launcher not found at $launcher. Reinstall or resync PaperSpine."
}
if (-not (Test-Path -LiteralPath $config)) {
  powershell.exe -NoProfile -ExecutionPolicy Bypass -File $launcher -OutputDir "paper_rewriting_output"
}
if (-not (Test-Path -LiteralPath $config)) {
  throw "PaperSpine intake is pending. Complete the permitted UI or use the numbered/text fallback, then rerun /paperspine."
}
Get-Content -LiteralPath $config -Raw
```

### macOS / Linux

```bash
CONFIG="paper_rewriting_output/paper_spine_config.json"
LAUNCHER="$HOME/.claude/skills/paper-spine/scripts/launch_paperspine_ui.sh"

if [ ! -f "$LAUNCHER" ]; then
  echo "PaperSpine UI launcher not found at $LAUNCHER. Reinstall or resync PaperSpine." >&2
  exit 1
fi

if [ ! -f "$CONFIG" ]; then
  chmod +x "$LAUNCHER"
  bash "$LAUNCHER" "paper_rewriting_output"
fi

if [ ! -f "$CONFIG" ]; then
  echo "PaperSpine intake is pending. Complete the permitted UI or use the numbered/text fallback, then rerun /paperspine." >&2
  exit 1
fi

cat "$CONFIG"
```

## After config is ready

When the config already exists, read it directly and continue through the
`paper-spine` orchestrator workflow without relaunching intake unless required
fields are missing.
