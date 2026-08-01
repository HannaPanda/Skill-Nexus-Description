# Nexus Description Skill

A skill for [Claude Code](https://claude.com/claude-code) that writes and rewrites Nexus Mods
descriptions. It exists because mod pages written from a repository drift the same way every
time: Harmony internals, test diaries, balance justifications and the same legal disclaimer
repeated in three sections.

The rule the skill enforces is simple. A Nexus description is a player-facing product page, not
a README, a development log, a QA report or a justification document.

Game-agnostic. Nothing in it is specific to 7 Days to Die, RimWorld or any other title.

## What it does

Writing runs in three stages, and the last two are mandatory even when the draft already looks
clean:

1. **Draft** against an information filter. Player benefit, required knowledge and legal
   information may appear on the page. Implementation, testing procedure and development
   history may not.
2. **Cleanup pass** that re-reads the finished page hunting for the material that survives a
   first draft. Changelogs, compatibility sections and legal disclaimers are where it hides.
3. **Compression pass** targeting a 15% cut without losing a single player action, requirement,
   limitation or gameplay feature.

Along the way it covers the parts that are not about content:

- **Never invent numbers.** Distances, percentages, ratios and drop chances must come from the
  source data or an actual test. The skill also checks that the numbers on a page agree with
  each other, which is how a "quarter as strong" claim sitting next to a "set it to 250%"
  workaround gets caught.
- **Compatibility wording.** Name the versions, say what is unverified, stop. A version that
  only started up does not get called verified.
- **Punctuation and rhythm.** No em dashes, and none of the sentence habits that make a text
  read as machine-written.

Output is Nexus BBCode, ready to paste into the rich-text editor.

## Installation

Clone into your personal skills folder, using the directory name `nexus-description`:

```bash
git clone https://github.com/HannaPanda/Skill-Nexus-Description.git ~/.claude/skills/nexus-description
```

On Windows that path is `%USERPROFILE%\.claude\skills\nexus-description`.

For a single project instead, clone into `<project>/.claude/skills/nexus-description`.

## Usage

The skill triggers on its own whenever a task involves a mod page description, a description
update, a beta notice, a Nexus changelog or BBCode for a mod page. Trigger phrases are
recognised in English and German. You can also invoke it by name:

```
/nexus-description
```

Typical prompts:

- "Write a Nexus description for this mod from the README."
- "Shorten the mod page, it reads like a changelog."
- "Check my mod pages against the description rules."

## Related

Two companion skills, both specific to 7 Days to Die:

- [Skill-7D2D-Development](https://github.com/HannaPanda/Skill-7D2D-Development) writes and
  debugs the mods.
- [Skill-7D2D-Testbench](https://github.com/HannaPanda/Skill-7D2D-Testbench) tests them against
  several game versions.

## Licence

MIT, see [LICENSE](LICENSE). Use it, fork it, adapt the rules to your own house style.
