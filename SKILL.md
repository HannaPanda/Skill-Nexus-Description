---
name: nexus-description
description: >-
  Schreibt und überarbeitet Nexus-Mods-Beschreibungen (Mod-Seite, Description-Tab,
  BBCode-Text) nach festen Regeln: Player-facing Produktseite statt README, keine
  internen Implementierungsdetails. Diese Skill immer benutzen, sobald eine
  Nexus-Beschreibung, eine Mod-Seiten-Beschreibung, ein Description-Update, ein
  Beta-Hinweis, ein Nexus-Changelog-Text oder der BBCode für eine Mod-Seite
  erstellt, gekürzt oder überarbeitet werden soll - auch wenn nur "Beschreibung
  für den Mod", "Nexus-Text", "mod page description" oder "Description" gesagt
  wird, und auch dann, wenn der Text nur aus einem README, einem Changelog oder
  einem Commit-Verlauf abgeleitet werden soll. Gilt für jedes Spiel (7 Days to
  Die, RimWorld, DayZ, ...).
---

# Nexus Mod Description Writing Rules

A Nexus Mods description is a player-facing product page, not a README, development log, QA report, technical specification, or justification document.

Writing happens in two stages. **Stage 1** drafts the page against the rules below. **Stage 2** is a mandatory editorial cleanup pass (see the end of this document) that runs even when the draft already looks compliant — the recurring failure mode is not a bad first draft, it is technical and defensive material creeping back in through changelogs, compatibility notes and legal disclaimers.

## Information filter

Before writing, silently classify every available fact:

* **Player benefit:** What the mod does, how it feels, why someone would use it.
* **Required knowledge:** Installation, compatibility, requirements, known limitations, safe uninstallation.
* **Legal information:** Credits, licences, source code and AI disclosure.
* **Internal detail:** Implementation, code architecture, patches, logs, testing procedures, technical reasoning and development history.

Only the first three categories may appear in the Nexus description.
Internal details must be omitted unless they directly change something the player must do.

## Never include

Do not include:

* Testing diaries or descriptions of how testing was performed.
* Statements about logs being checked.
* Harmony patch implementation details.
* Class names, method names, asset loading internals or networking implementation.
* Explanations of why a technical limitation exists.
* Defensive wording intended to prove that development was careful.
* Long justifications for balance values or unlock levels.
* Comparisons containing unnecessary exact damage calculations.
* Repeated compatibility information.
* Repeated feature descriptions using different wording.
* Roadmap details presented as features missing from the current release.
* Statements such as "here is exactly what this means", "I would rather list that", or similar self-conscious narration.
* Information that belongs in the GitHub README, changelog or issue tracker.
* Filler written merely to make a section feel complete.

## Technical-detail test

For every technical sentence, ask:
**Does this change what the player needs to install, configure, avoid, expect or do?**
If the answer is no, remove the sentence.
Explain the effect, not the implementation.

Bad:
> The drones carry the thrower's entity ID through a custom Harmony component, allowing XP attribution.

Good:
> Drone kills grant normal XP and count as your kills.

Bad:
> Version 3.0.1 was launched and the Harmony patch logs were checked for exceptions.

Good:
> Tested on 3.1. Compatibility with earlier 3.x versions is not guaranteed.

## Explain actions, not causes

When technical behaviour affects installation, multiplayer setup or removal, state the action the player must take. Never explain the engine internals behind it.

Bad:
> Saves containing a custom entity class cannot resolve it once the assembly is removed.

Good:
> Before uninstalling, wait until all active pods and drones have disappeared.

Bad:
> The server cannot distribute asset bundles to clients.

Good:
> Every player and the server must have the mod installed.

## Technical specification rules

Exact specifications belong on the page only when they help the user succeed. Do not list every supported bit depth, sample rate, channel count, format variant or internal limit when one plain instruction covers normal usage.

Bad:
> Supports 8, 16 and 24-bit PCM, 32-bit float, 1–8 channels and 4–192 kHz.

Good:
> Use a normal uncompressed WAV file up to 25 MB.

A conversion command, a file path or a config snippet may be included when it is a practical solution the player would otherwise have to look up.

## Never invent numbers

Every concrete value on the page must come from the supplied source data, the code, or something that was actually tested. This includes distances, ranges, percentages, ratios, damage figures, drop chances, durations, stack sizes and supported versions.

Do not fill a gap with a figure that merely looks plausible. If a number is not available, describe the effect qualitatively instead.

Bad (invented endpoints for a slider whose only known value is the default):
> Force - 25 to 300%. Roughly 10 m at the default, about 6 m at the bottom and 75 m at the top.

Good:
> Force - 25 to 300%. Controls how strongly the dash launches you; roughly 10 m at the default.

Also check that the numbers on the page agree with each other. A stated ratio, a stated before/after pair and a suggested compensating setting must be consistent. If the page says a value is "about a quarter as strong" while also telling the player to set the slider to 250% to restore the old behaviour, one of the two is wrong: recompute from the source rather than keeping both.

Do not attribute an effect to the wrong game property. Stability, explosion resistance, block hardness and damage gating are separate mechanics; describe each as what it actually does, and never present one as the reason for another.

When a number cannot be verified and cannot be dropped without losing something the player needs, say what is known and leave the rest out.

## Compatibility wording

Compatibility sections must be brief and factual. Name the versions, say what is unverified, stop.

Preferred:
> **Tested on V 3.1.** Other 3.x versions have not been tested.

Avoid legalistic or defensive language:

* "not known-broken"
* "logs were checked"
* "patches apply"
* "no exceptions were found"
* "verified properly"
* "every release has to re-earn this list"
* any explanation of why a version was or was not tested

Never imply compatibility merely because the mod loaded once, and never present a clean load as evidence of quality.

**The one permitted exception:** when a version was actually launched but not played through, saying so answers a real compatibility question and may stay. Distinguish the three states precisely and claim no more than each earns:

* Fully tested: **"Tested on V 3.1."**
* Launched during development, not fully tested: **"V 3.0.0 and V 3.0.1 loaded successfully during development but were not fully tested with this release."**
* Never run: **"Other 3.x versions have not been tested."**

This exception covers one short clause about a specific named version. It does not license a description of what was checked, how it was checked, or what the log showed.

## Roadmap wording

Do not describe planned features as a list of things the current release is missing.

Bad:
> The chem launcher, turret, gun drone and hive are not in this file yet.

Good:
> The Cluster Seeker is the first Agent Armory gadget. More modules are planned.

Omit roadmap information entirely when it does not help the player understand the current release.

## Changelog rules

The Nexus changelog is not the full technical changelog. It describes only player-visible change:

* what was added
* what changed in gameplay
* what was fixed
* what the user must do differently

Do not include formulas, internal calculations, method or class changes, configuration-loading details, implementation explanations, detailed accounts of how a bug was fixed, or defensive assurances such as "nothing breaks" or "no errors occur".

Rewrite every internal change into its visible result.

Bad:
> Only the part of the existing velocity already pointing in the dash direction is counted, and only at 25 percent.

Good:
> Improved sprint momentum handling for sideways and backward dashes.

Bad:
> Settings are read on every dash.

Good:
> Setting changes apply immediately.

Link the full technical history on GitHub instead of reproducing it.

## Repetition rules

Each fact should normally appear once. A short introduction may summarise the main feature, but every later section must add new information rather than restate the same feature in different words.

Before final output, check for repeated mentions of:

* the number of projectiles, drones or charges
* damage and radius
* supported versions
* multiplayer installation requirements
* EAC requirements
* AI usage
* voice cloning restrictions
* licences
* removal safety
* planned features

Keep the clearest occurrence and delete the rest.

## Legal and AI disclosure rules

Legal information must be accurate but concise. Do not repeat the same restriction across the feature section, the AI disclosure and the credits — state it once, in the place a player is most likely to read it.

Do not expand a disclosure into a defensive explanation about hosting, training, generation pipelines or hypothetical reuse unless it is legally required or directly relevant to the user.

Credits may identify the creator, the asset, the source, the licence and any redistribution restriction. Nothing more is needed unless the licence explicitly requires it.

## Avoid defensive prose

Remove any sentence whose main purpose is to prove that the author was careful, honest or technically competent:

* "Here is exactly what that means."
* "I would rather tell you than let you find out."
* "This was tested properly."
* "Nothing breaks and nothing errors."
* "Other versions are untested, not known-broken."
* "The whole thing has to re-earn compatibility from scratch."

State the useful fact directly instead.

## Section naming

Prefer ordinary player-facing headings:

* Features
* How It Works
* Unlocking and Crafting
* Requirements
* Installation
* Known Limitations
* Uninstallation
* Changelog
* Credits

Avoid self-conscious headings such as "Honest Notes", "Here Is Exactly What Beta Means" or "What It Is Good At and What It Is Not". A more descriptive heading is fine when it fits the mod, as long as it does not sound defensive or theatrical.

## Tone

Write clearly, directly and confidently.
The text should sound like it was written by a mod author explaining the mod to another player.
Use concrete descriptions instead of marketing language. Avoid exaggerated hype, artificial punchlines, corporate wording and overdramatic claims.
Do not explain obvious statements. Do not defend every design decision.

## Punctuation and sentence rhythm

**Never use em dashes or en dashes (— –) anywhere in the output.** They are the single clearest tell that a text was machine-written, and the author does not want them on the page. Use a comma, a colon, a full stop or brackets instead, and recast the sentence if none of those fit. A plain hyphen surrounded by spaces is acceptable in list items where a label is separated from its explanation, but prose should not lean on it either.

Also avoid the other habits that make a text read as generated:

* The "not just X, it's Y" and "this isn't a Y, it's a Z" construction.
* Three-part parallel lists used for rhythm rather than because there are three things.
* A short dramatic sentence fragment placed after a long sentence for effect.
* Opening a paragraph by restating the heading.
* Sentences whose only job is to announce what the next sentence will say.

Vary sentence length naturally. A page where nearly every sentence has the same shape reads as generated even when every individual sentence is fine.

## Recommended structure

Use only sections that contain useful information:

1. Short hook
2. What the mod adds
3. Main gameplay features
4. How to unlock or craft it
5. Beta or known limitations
6. Requirements and installation
7. Safe removal, only when relevant
8. Credits, licence and AI disclosure
9. Changelog

Merge sections when they are short.

## Length

The main description should normally remain below 900 words, excluding credits, licence information and changelog.
Each section should answer one clear player question. Prefer short paragraphs and a few meaningful bullet points.
Do not add a section merely because Nexus descriptions commonly contain one.

## Preserve useful complexity

Do not shorten a description merely to make it short. Detailed explanation is appropriate wherever the player genuinely needs it, for example:

* several input modes
* controller bindings
* perk ranks
* configuration options
* multiplayer setup
* save-removal precautions

A feature-rich mod earns a longer page. Remove implementation detail, not necessary user guidance.

## Beta wording

A beta notice should state only:

* What is already complete.
* What may still change.
* What kind of feedback is useful.

Do not describe the test process.

Example:
> The Cluster Seeker is feature-complete. Balance, compatibility and terrain behaviour may still change during the beta. Feedback about damage, crafting cost and unlock timing is especially useful.

## Source priority

When writing a Nexus description, use explicitly supplied player-facing facts as the source of truth.
Do not mine the repository for additional implementation details merely because they are available.
When uncertain whether a fact belongs in the description, omit it.

## Stage 2: mandatory cleanup pass

After the draft is finished, run a separate editorial pass over it. **This pass is required even when the draft already follows the information filter** — it is where the recurring leaks are caught. Read the whole page again looking specifically for:

* technical implementation details
* development notes
* QA narration
* repeated compatibility warnings
* repeated legal disclaimers
* repeated feature explanations
* balance justifications
* roadmap details presented as missing features
* changelog entries that explain internal mechanics instead of player-visible changes
* numbers that were not in the source data, and numbers that contradict each other
* em dashes and en dashes

Changelogs, compatibility sections and legal disclaimers are the three places where this material survives a first draft most often. Check them explicitly, even if the body of the page is clean.

Search the finished text for `—` and `–` and remove every occurrence before returning it.

## Stage 3: final compression pass

After the cleanup pass, run one more pass whose only job is to make the page shorter. **Aim to remove at least 15% of the draft without losing a single player action, requirement, limitation or gameplay feature.**

During this pass:

* Remove information already stated elsewhere on the page.
* Never leave a section that holds only one sentence or one bullet. Merge it into the nearest relevant section and drop the heading.
* Remove defensive words such as "real", "properly", "exactly", "honest" and "as you would expect" unless they carry necessary information.
* State requirements without explaining their implementation. Write "EasyAntiCheat must be disabled", not why the DLL requires it.
* Keep only the latest one or two releases in the Nexus changelog when the full changelog is linked.
* Shorten configuration explanations once the options and their effects are clear.
* Remove sentences that justify why a piece of information was included.
* Prefer one direct sentence over a paragraph followed by a quote that repeats it.

Then check:

1. Is any feature explained more than once?
2. Does every section contain enough useful information to justify its heading?
3. Is any sentence defending a design decision instead of describing its effect?
4. Could a player understand the mod without the technical explanation?
5. Does the page become easier to scan if this paragraph is removed?

Compression removes redundancy and self-justification, never user guidance. If a cut would leave the player unable to install, configure, unlock or safely remove something, put it back.

## Final validation questions

Before returning a Nexus description, silently check every paragraph:

1. Does this tell the player what the mod does, how to use it, what to expect or what they must do?
2. Is this fact already stated elsewhere?
3. Is this describing implementation rather than behaviour?
4. Is this defending a decision that could simply be stated?
5. Does this belong in the GitHub README or full changelog instead?
6. Can this be said more directly without losing useful information?
7. Does every number here come from the source data, and do the numbers agree with each other?
8. Are there any em dashes left?

If a paragraph fails question 1, remove it unless it is required legal or credit information.

## Output format

Deliver the description as Nexus BBCode (`[b]`, `[size=5]`, `[list][*]`, `[url=]`, `[spoiler]`) unless something else was asked for. The BBCode goes straight into the Nexus rich-text editor - no BBCode mode required, so there is no need to warn about that.
