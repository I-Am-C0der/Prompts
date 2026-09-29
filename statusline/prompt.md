/statusline Create an ultra-polished, information-dense single-line Claude Code statusline optimized for a modern dark terminal. Use truecolor 24-bit ANSI RGB throughout, with a clean developer-HUD aesthetic and dim gray RGB(70,70,70) pipe separators. Keep it strictly single-line and dynamically adapt to terminal width: show the full information set on wide terminals and gracefully omit lower-priority fields on narrow terminals rather than wrapping.

Prioritize information density, readability, and real utility over decoration. Use only information actually provided by Claude Code's statusline JSON payload or safely derivable from the current repository/session. Never fabricate, estimate, or infer unavailable metrics.

Layout, in this exact priority order:

1. 📁 Repository/project name — bold yellow.

2. 🌿 Git branch — bold cyan, with the branch name inside parentheses.

3. Git working-tree state — derive from the current repository using Git commands and show compact indicators for staged, modified, untracked, ahead, and behind state. Preferred format: `✚3 ~2 ?1 ↑2 ↓1`. Show `✓` when the working tree is clean. Use green for staged/addition indicators, yellow for modified, red for conflicts/problems, and cyan for ahead/behind. Keep Git operations lightweight because the statusline may refresh frequently.

4. Context usage — dynamic 20-block progress bar. Use Claude Code's native context usage percentage when available; do not independently recalculate the percentage from token counts when a native percentage is provided. Color the filled blocks with a smooth 24-bit RGB gradient from green RGB(0,200,80), through yellow RGB(220,200,0), to red RGB(220,40,20), according to overall context usage. Use RGB(60,60,60) for empty blocks.

5. Dynamic context-status emoji based on usage:
   - 🟢 below 20%
   - ⚡ 20–69%
   - 🔥 70–89%
   - 🚨 90%+

6. Exact context percentage using the same severity color as the bar.

7. Context token usage when available — compact format such as `108k/200k`, using dim gray for the numeric token count. Prefer Claude Code's native context values.

8. Session code-change statistics — show total lines added in green and total lines removed in red, e.g. `+842 -317`. Do not call this "velocity"; these are cumulative session change statistics.

9. Current session cost — show the native Claude Code session cost in yellow, e.g. `💰 $3.42`. Treat it as an estimated session cost and do not represent it as a billing-period balance.

10. Claude usage/rate-limit information when natively available — show the relevant 5-hour and 7-day usage percentages compactly, with reset time when useful. Example: `5h 38% ↻2h14m │ 7d 17% ↻3d8h`. Omit these fields when unavailable. Do not infer or fabricate a monthly dollar allowance, subscription balance, or remaining credits from session cost.

11. 🤖 Model name — magenta, showing a concise human-readable model name rather than an unnecessarily long model ID.

12. 🧠 Reasoning/thinking effort when available — purple, e.g. `HIGH`, `XHIGH`, or `MAX`.

13. ⏱ Session duration when available — dim cyan, formatted compactly as `14m`, `1h42m`, etc.

14. ↻ Turn/request count only if reliably available — dim white. Omit it if Claude Code does not expose a reliable native value rather than attempting to reconstruct it.

15. API latency only when useful and available — show compactly, such as `API 1.2s`. Keep this lower priority than all fields above and omit it on narrow terminals.

Use concise symbols and abbreviations so the line remains readable. Do not duplicate information. Do not use excessive emoji. Make the context bar the primary visual element.

Preferred wide-terminal appearance:

📁 hermes │ 🌿 (feature/agent-core) ✚3 ~2 ?1 ↑1↓0 │ ⚡ ███████████░░░░░░░░ 54% 108k/200k │ +842 -317 │ 💰 $3.42 │ 5h 38% ↻2h14m │ 7d 17% ↻3d8h │ 🤖 Sonnet 4.6 │ 🧠 HIGH │ ⏱42m

Color rules:
- repository: bold RGB(255,210,60)
- branch: bold RGB(0,210,255)
- Git healthy/staged/addition indicators: RGB(0,220,100)
- modified indicators: RGB(255,190,0)
- conflicts/problems: RGB(255,60,50)
- ahead/behind: RGB(0,200,255)
- context filled blocks: smooth truecolor green → yellow → red gradient based on usage
- empty context blocks: RGB(60,60,60)
- context percentage: same color as current context severity
- context token counts: dim RGB(150,150,150)
- +lines: RGB(0,220,100)
- -lines: RGB(255,70,70)
- session cost: RGB(255,210,60)
- rate-limit usage: use the same green → yellow → red severity scheme
- model: RGB(220,80,255)
- reasoning level: RGB(180,100,255)
- session duration/API latency/secondary metrics: dim RGB(150,150,150)
- separators: dim RGB(70,70,70)

For narrow terminals, progressively remove information in this order:
1. API latency
2. turn/request count
3. session duration
4. reasoning level
5. detailed rate-limit reset times
6. Git ahead/behind counts
7. changed-file counts
8. context token count
9. detailed Git statistics

Never remove repository name, branch, context bar, context percentage, session cost, or model unless absolutely necessary.

For very narrow terminals, preserve the core HUD:
`📁 repo │ 🌿 (branch) │ ⚡ ███████████░░░░░░░░ 54% │ 💰 $3.42 │ 🤖 Sonnet`

Do not wrap to a second line under any circumstances.

Important implementation rules:
- Use native Claude Code statusline JSON fields whenever available.
- Use `cost.total_cost_usd` for session cost.
- Use native context-window percentage and size fields for context display.
- Use native lines-added/removed fields for session change statistics.
- Use native model and effort fields when available.
- Use native duration data when available rather than maintaining a separate timer.
- Use native rate-limit fields when available.
- Derive Git branch/worktree state from Git only when necessary.
- Avoid expensive shell commands or repository-wide scans on every statusline refresh.
- Gracefully omit any unavailable field.
- Never fabricate monthly budget, subscription balance, token counts, turn counts, or other unavailable metrics.
- Do not attempt to reconstruct unavailable metrics from unrelated fields.
- Keep the final implementation fast enough that statusline rendering itself is effectively unnoticeable.

Make the final result visually balanced, compact, highly readable, and suitable for continuous use during long Claude Code sessions.
