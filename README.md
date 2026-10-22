# Peace Intel console parts: clarifying questions, research updates, the field's active state

**For:** Nathanael Miksis and his coding agent
**From:** Matt Gillespie, 21 October 2026 (handoff Rev 60)

Four fixes to production's console. Production's clarifying-question card and research
updates overuse the accent, round their corners past 4px and set every line in the serif.
Both are now restyled on the brand system. Production's input field also does not match the
handoff when it is active.

**The CSS to swap in:** `console-parts.css`. It holds just the Rev 60 blocks (H1.19 and H1.20), extracted from `components.css`, ready to replace the hand-built versions at the end of production's `console.css`. The package zip and folder you had were Rev 58, which is why `components.css` there had none of this.

**Start here:** `console-parts.html` (the page this site opens to). Every state is drawn on it,
and each specimen's markup is the markup to build. Read the page's source.

| File | What it is |
|---|---|
| `console-parts.html` | The three parts, every state, plus a live demo |
| `console-parts.css` | Only the Rev 60 CSS, to paste into production. An extract: `components.css` wins if they differ |
| `components.css` | The whole catalog, Rev 60. Search for `H1.19` (`.clarify`, `.cq-*`) and `H1.20` (`.ru`) |
| `CONSOLE.md` | The console's behaviour. Section 2 covers all three; section 8 lists them as H1.19 to H1.21 |
| `AGENTS.md` | The rules. The quick reference has a row for each part |
| `console.html` + `prototypes.js` | The console prototype. Click into the composer to see the right active state. `prototypes.js` is a mock to read, not to port |
| `tokens.css`, `explorations.css`, `system.js`, `reference.css` | The rest of the system, so the pages render. `reference.css` is page furniture only and is not part of the system |

If this README and the CSS disagree, the CSS wins.

## What to change in production

1. **Clarifying questions (H1.19).** Keep production's questions and its logic, and replace
   the card's markup and styles with `.clarify`:
   - neutral mono count and the 2px ink step line;
   - the question as the card's only serif line;
   - the options in a tray, and the chosen one rises as a tile;
   - the lead term in bold where production writes "Lead term — gloss";
   - *Write my own answer* last, opening a field. Drop "Something else (please specify)";
   - *Skip questions* as `.btn.ghost`, *Next* / *Start research* as `.btn.tint`, *Back* as `.act`.

   Answered, the card goes and the answers post as the user's message. Skipped, one `.cq-done` line.
2. **Research updates (H1.20).** Remove the warm boxes, the orange left rules and the orange
   toggle edge.
   - While working, the newest update is the pending answer's text.
   - Earlier updates fold above it in `details.ru`.
   - When the answer lands, all of them fold into that one line at the answer's head, closed.
3. **The field's active state (H1.21).** Production does not match the handoff.
   - The composer: no shadow at rest. On focus its edge goes to `--ink-35` and it lifts to
     `--elev-3`. The textarea inside draws nothing of its own.
   - Every other field: on focus, edge `--ink-35` and `--elev-1`, no outline.
   - No field takes an accent ring or an accent edge.

4. **A match found by search in a chat (H1.22, Rev 61).** No box round the message. Every place
   the words occur in it takes a grey wash, `--hl-find` (ink at 12%, a new token), through the
   CSS Custom Highlight API (`::highlight(find)`), and the first is scrolled to the middle of the
   screen. Not the orange `--hl`: that marks the passage a citation points to. Click a search
   result from This chat in `console.html` to see it; `markFind` in `prototypes.js` is the mock.

Also fixed at the base, for anyone who copied it: `.reflect` and `.cb-file` wrote
`border: 1px solid var(--edge)`. `--edge` is already a whole border, so that line is invalid
and drew nothing. Write `border: var(--edge)`.
