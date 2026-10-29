# Cthangover: Murakami — a story line of the main game

This mod adds one story line to Cthangover: something prowls the town, and following it leads to a meeting with Murakami. It brings the scenarios of that meeting, Murakami as a character with her portrait and set of expressions, a quest in the journal, and battles. It is part of the Cthangover game and needs the base story (`cthangover_game`) to run.

This page describes how the line is attached to the game and how it starts; what happens later is left for the player.

## How it starts

When Marao comes to the town entrance, a growl comes from the darkness and the player chooses whether to go back home or check the alley:

![The town entrance at night: the text "[A muffled growl came from the darkness]" with the answers Return home and Check the alley.](assets/growl.jpg)

Checking the alley starts the quest **Meeting Murakami**, and its first entry appears in the journal:

![The journal with the active quest Meeting Murakami and its entry "I met a wild wolf in the city; it was trying to get into a locked house."](assets/journal.jpg)

## How it is attached to the base story

The mod changes no file of the base game. It adds scenarios to existing scenes, and the game picks the one to play by its priority and condition:

```scenario
scene: town_entry
priority: 10
condition: MeetingMurakamiQuest.notHasTag("wolf_battle")
```

- The opening scenario belongs to the scene `town_entry` with priority 10, so it is chosen over the town's ordinary scenarios while its condition holds.
- Each next step of the line is another scenario of `town_entry` with a higher priority (20, 30) whose condition looks at the tags of the quest `MeetingMurakamiQuest`. The last step plays in the house (`home_vestibule`).
- Battles start with `battle.init` on the platform's battle system; the outcome is written back as a quest tag, so the next scenario knows what happened.
- When the line is finished, its conditions no longer hold and the town plays its ordinary scenarios again.

What the mod ships:

- `scenarios/murakami/meeting/` — the four scenarios of the meeting;
- `quests/quests.json` — the quest with three journal entries;
- `characters/player/murakami.json` — Murakami as a character, with her picture;
- `avatars/murakami/` — her expressions for dialogs;
- the backgrounds of the meeting in `backgrounds/town/meetingmurakami/`;
- texts in seven languages in `locale/`.

## Turning it off

The line can be left out of the game's collection: the town then plays only its own scenarios, and the quest never appears.

## Known problems

- Two of Marao's expressions used by these scenarios, `marao/what` and `marao/relax`, do not exist in the game, so those lines show no portrait. The Validator reports them as `REF_NOT_FOUND`.
