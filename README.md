# dnt rules

Rules for [dnt](https://github.com/v0v3s/dungeons-n-terminals), the D&D 5e
companion: what a feature does to a character sheet (its uses, the Armor
Class it gives, the speed it adds…), so the sheet does the maths.

dnt has many rules built in. This repository collects the rest, for anyone
to use and add to:

| Folder | Rules for |
|---|---|
| [`srd/`](srd) | the SRD 5.2.1, which dnt has built in |
| [`homebrew/`](homebrew) | homebrew (only the rules: import the homebrew itself into dnt) |

## Using them

dnt reads this library itself: tick a folder, a file or single rules and
import them, and they become your rules (your rules for a feature replace
dnt's own; where you have rules of your own, it asks before overwriting).

- **The app:** *Data › Rules library*.
- **The terminal app:** `L` on **4 Campaigns**, or from the shell:
  `dnt rules` lists the library, `dnt rules import srd` (a folder, a file
  such as `srd/classes`, or a rule's id) imports.

By hand: a file of rules is a list of `[[feature]]` blocks, one per
feature; copy it into dnt's rules folder, `library/overlays/` in its data
folder (`~/.local/share/dnt` on Linux, `%APPDATA%\dnt` on Windows), or
paste a block into a feature's *rules* in the app.

## Writing rules

```toml
[[feature]]
id = "classFeature:Roving|Ranger|SRD52|6"   # what dnt calls the feature
[[feature.effect]]
target = "speed"
add = "10"
when = "not armor.heavy"
```

A feature has `[[feature.effect]]`s (on `ac`, `speed`, `hp.max`,
`skill.<skill>`, `str`…`cha`, `attack.bonus`, …: `add`, `set`, `max`,
`min` or `mul`, maybe `when`), `[[feature.resource]]`s (uses that come
back on a rest) and `[[feature.toggle]]`s. See
[Homebrew and rules](https://github.com/v0v3s/dungeons-n-terminals/wiki/Homebrew-and-rules)
and the [format](https://github.com/v0v3s/dungeons-n-terminals/blob/main/schemas/overlay.schema.json).
In dnt, a feature's *rules* show its `id` and check what you write as you
type.

## Adding yours

Pull requests are welcome:

- one file per book or homebrew, in `srd/` or `homebrew/`;
- rules only: no text of the book or homebrew they are for (a short
  comment on what a rule does is fine), and the homebrew's author named
  at the top of its file;
- the check passes (CI runs it on every pull request):

  ```sh
  cargo run -p dnt-rules --example check_overlays -- data/srd srd/*.toml
  cargo run -p dnt-rules --example check_overlays -- --parse-only data/srd homebrew/*.toml
  ```

  from a checkout of dnt (paths to this repository's files).

By contributing, you license your rules under this repository's licence.

## Licence

[CC BY 4.0](LICENSE). Credit "dnt rules" with a link to this repository.

This work includes material from the System Reference Document 5.2.1
("SRD 5.2.1") by Wizards of the Coast LLC, available at
https://www.dndbeyond.com/srd. The SRD 5.2.1 is licensed under the
Creative Commons Attribution 4.0 International License, available at
https://creativecommons.org/licenses/by/4.0/legalcode.

The rules in `homebrew/` describe the workings of homebrew by its
authors, who are named in each file; the homebrew itself is theirs and is
not included.
