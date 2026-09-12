---
description: Start PaperSpine — research, then rewrite or build a paper or report end to end
argument-hint: "[optional: target/scene, e.g. 'IEEE conference paper from ./materials']"
---

Start the PaperSpine workflow for the current project using the **`$paper-spine`
orchestrator** skill. Route through `$paper-spine`; do not call the worker
sub-skills directly unless the orchestrator tells you to.

If `paper_rewriting_output/paper_spine_config.json` is missing or incomplete,
inspect the existing configuration, progress, and launcher availability first.
Resolve the launcher by its absolute installed path — Codex runs from the project
folder, where `scripts/` does not exist. Use only parameters supported by the
current host; do not request elevation or require the launcher to precede
inspection. If the UI is unavailable, use the numbered/chat intake fallback for
the missing fields and leave configuration-dependent stages at the intake gate.
Read-only preparation that does not depend on missing configuration may continue.
Never treat a launcher timeout as approval, and do not infer a user's motivation
or contribution choice. Reuse a valid existing approval only when its source and
target scope still match.

### Windows

```powershell
$paperSpineConfig = Join-Path (Get-Location) "paper_rewriting_output\paper_spine_config.json"
$paperSpineLauncher = @(
  "$env:USERPROFILE\.codex\skills\paper-spine\scripts\launch_paperspine_ui.ps1",
  "$env:USERPROFILE\.claude\skills\paper-spine\scripts\launch_paperspine_ui.ps1",
  "$env:USERPROFILE\AppData\Local\hermes\skills\academic-writing\paper-spine\scripts\launch_paperspine_ui.ps1"
) | Where-Object { Test-Path -LiteralPath $_ } | Select-Object -First 1
$paperSpineLaunchState = 'INTAKE_FALLBACK_REQUIRED'
if (-not (Test-Path -LiteralPath $paperSpineConfig) -and $paperSpineLauncher) {
  try {
    powershell.exe -NoProfile -ExecutionPolicy Bypass -File $paperSpineLauncher -OutputDir "paper_rewriting_output"
    if ($LASTEXITCODE -eq 0) { $paperSpineLaunchState = 'UI_PENDING' }
  } catch {
    Write-Output "UI launch failed: $($_.Exception.Message)"
  }
}
if (Test-Path -LiteralPath $paperSpineConfig) {
  Get-Content -LiteralPath $paperSpineConfig -Raw
} else {
  Write-Output $paperSpineLaunchState
}
```

### macOS / Linux

```bash
paper_spine_config="paper_rewriting_output/paper_spine_config.json"
paper_spine_launcher="$HOME/.codex/skills/paper-spine/scripts/launch_paperspine_ui.sh"
[ -f "$paper_spine_launcher" ] || paper_spine_launcher="$HOME/.claude/skills/paper-spine/scripts/launch_paperspine_ui.sh"
paper_spine_launch_state="INTAKE_FALLBACK_REQUIRED"
if [ ! -f "$paper_spine_config" ] && [ -f "$paper_spine_launcher" ]; then
  if bash "$paper_spine_launcher" "paper_rewriting_output"; then
    paper_spine_launch_state="UI_PENDING"
  fi
fi
if [ -f "$paper_spine_config" ]; then
  cat "$paper_spine_config"
else
  printf '%s\n' "$paper_spine_launch_state"
fi
```

### Handle the observed intake state

- Config content returned: read it and run the existing intake validation before
  any configuration-dependent stage. File existence alone is not validation.
- `UI_PENDING`: the launcher returned while the user-facing intake is still
  pending. Do not relaunch the window or require the user to rerun `/paperspine`.
  Continue independent read-only preparation, then recheck the existing config
  with a bounded wait when appropriate. A missing config or elapsed wait never
  means the user approved a motivation or completed intake.
- `INTAKE_FALLBACK_REQUIRED`: perform the numbered/chat intake fallback in
  `references/intake.md` now, reusing known answers and asking only for missing
  required decisions. Keep dependent stages at the intake gate. Do not replace
  this fallback with an instruction to reinstall or restart the task.

### After config is ready

When the config already exists, read it and continue through the `$paper-spine`
orchestrator workflow (research → confirm motivation → rationale matrix →
rewrite/build → LaTeX/PDF/Word → audit) without relaunching intake unless
required fields are missing. If `$1` was provided, treat it as the target/scene hint.
