# UX/UI workflow: a Claude skill

One skill that takes a product idea from requirements to finished UI in three phases: requirements, then UX, then UI.

The rule behind it: **the AI does the manual work, not the critical thinking.** It finds the questions, generates the options and writes everything up. You make every decision.

## The three phases

Each phase goes wide, then narrows down.

| Phase | What happens | Output |
|---|---|---|
| **1. Requirements:** the right problem | Claude interviews you in short rounds, with options and a recommended answer for each question. It runs a blind-spot round, a coverage check and an assumptions sign-off, then narrows everything into a problem statement you confirm. | `requirements.md` |
| **2. UX discovery:** the right solution | 3 genuinely different solution concepts, compared against your requirements. You pick one, and it's mapped into a journey, user flows, a screen inventory and a hero screen. No visuals yet. | `ux-brief.md`, `design-brief.md` |
| **3. UI:** the rule of three | On a Claude Design canvas: 3 directions for the hero screen, you pick one, then 3 variations of it, you pick the winner. Then a critique, a design system, and the rest of the screens. Each round is a row of 3 on the canvas, with your picks marked. | the canvas, a design system, `ui-progress.md` |

Claude stops at every decision point and waits for you, and it asks before moving on to the next phase.

## Install

### Claude Code

Clone this repo and copy the skill into your personal skills folder:

```bash
git clone https://github.com/AiTooltip/uxui-workflow.git
```

```bash
mkdir -p ~/.claude/skills && cp -R uxui-workflow/uxui-workflow ~/.claude/skills/
```

To use it in one project only, copy the `uxui-workflow` folder into that project's `.claude/skills/` folder instead.

### Claude (claude.ai and the desktop app)

1. Download [uxui-workflow.zip](https://github.com/AiTooltip/uxui-workflow/raw/main/uxui-workflow.zip).
2. In Claude, open **Settings**, find **Skills**, and upload the zip.

## Use it

Start a new conversation and either run `/uxui-workflow` (Claude Code) or describe what you want to build:

> I want to build an app for an independent climbing gym where members book sessions and classes.

### Stop and pick up later

The files are the save points. Each phase saves its output in your project folder, so you can stop after any phase and continue in a new conversation. The skill checks which files exist and picks up from there:

- no files → phase 1
- `requirements.md` → phase 2
- `design-brief.md` → phase 3
- `ui-progress.md` → back to the same canvas, at the round where you stopped

You can also jump to a phase directly, for example `/uxui-workflow ui` if you already have a design brief.

## What's in the skill

```
uxui-workflow/
├── SKILL.md                  ground rules, where to start, the stops between phases
└── phases/
    ├── 1-requirements.md
    ├── 2-ux-discovery.md
    └── 3-ui.md
```

Claude reads only the file for the phase it's in, so the UI instructions don't leak into the requirements interview.

## Notes

- **Phase 3 uses Claude Design canvases inside Claude.** If your account can't create them, the skill builds each option as an HTML file you can compare side by side.
- **A default design system changes round 1.** If you have one set as default, the canvas uses it, so the 3 directions share its colors and type and differ in layout, hierarchy and signature instead. Ask the skill to design without it if you want the full range.
