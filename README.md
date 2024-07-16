# Overview

This is an unofficial extension for hacking Final Fantasy Tactics, specifically event scripting. It builds on the content provided by the [FFHacktics community](https://ffhacktics.com/) and as such refers to all such content in the event instruction data (including linking to the [wiki](https://ffhacktics.com/wiki/Main_Page)).

[![License: CC BY-NC 4.0](https://img.shields.io/badge/License-CC%20BY--NC%204.0-lightgrey.svg)](http://creativecommons.org/licenses/by-nc/4.0/)
Share it and don't sell it...

Enjoy and happy hacking 😁

**Features and tutorials**

As long as your open event file's extension is `.evt` (such as `event.evt`):

- Named event instruction hover, code completion, and signature help support
  - **Tutorial**: [crash course video](https://www.youtube.com/watch?v=btLANdB91fg); includes extension installation
  - Event instruction info displaying [![Requires Event Instruction Upgrade - click for Wiki page](icon/EIU_icon.png)](https://ffhacktics.com/wiki/Event_Instruction_Upgrade) indicates the event instruction requires the Event Instruction Upgrade; click the icon where shown to link to the wiki page for details, including where to download
- Code snippets (see below)
- Syntax highlighting (see below for formatting scopes) and language support

---

## Snippets

Snippets create quick blocks of text for common code sections, and allow you to `[Tab]` through and set different pieces as available.

The following table details the current collection of snippets, and the codes to use them. Type the code (and optionally press `[Ctrl]` + `[.]`), and select from the dropdown to spark snippet insertion.

| Snippet Title              | Code       | Description                                 |
|----------------------------|:----------:|---------------------------------------------|
| Regions                    | `creg`     | Creates region opening and closing tags.    |
| #Const Block               | `cblock`   | Supplies the event-local #Const block.      |
| Constant Declaration       | `const`    | Supplies a constant skeleton for the #Const block. |
| Create Message             | `msg`      | Supplies a flexible message setup.          |
| Unit Setup                 | `setup`    | Loads units into the event map.             |
| Camera Setup               | `csetup`   | Supplies a default collection of camera calls for initial setup. |
| Say Message                | `smsg`     | Sets a unit to speak.                       |
| Exchange Messages          | `emsg`     | Sets 2 units to speak.                      |
| Dialog                     | `dmsg`     | Sets 2 units to speak, and optionally focuses on the first one to begin. Also `mdialog`. |
| Battle Banter              | `bmsg`     | Sets 2 units to talk back and forth in the middle of battle. Also `banter`. |
| Unit Move                  | `move`     | Sets a unit walking a certain distance away on the event map. |
| Unit Enter                 | `enter`    | Brings a unit into the event map.           |
| Unit Exit                  | `exit`     | Sends a unit out of the event map.          |
| End Battle                 | `endbat`   | Optionally revives unit x01, and turns the player team to face them. |
| Clear Map                  | `clearmap` | Removes all units from view.                |
| Fade Out                   | `fadeout`  | Fades the event map to black.               |
| Zoom Out                   | `zoomout`  | Raises the camera 500 units after a battle. |

---

## Syntax Highlighting

This extension provides enhanced syntax highlighting for `.evt` files, specific to the event functions as defined by the FFHacktics community. Below are the scopes you can style in your editor to customize the appearance of FFHackticsEvent code. With the way VS Code handles scopes usually, event instruction-type scopes have names including `function` instead.

### How do I use these?

The short answer is that in your `settings.json` file, you set formatting for a given scope (or multiple). You can copy the contents of [the default scopes and coloring](ffhacktics-event-all-scopes.jsonc), or you can copy over only some of them. Change them as much as you like to match your desired colors and text effects!

Though the defaults list each item individually for control, you can also combine multiple scopes for convenience. See the following example for formatting both event script comments and number prefixes as dark gray lettering and italics:

```json
"editor.tokenColorCustomizations": {
    "textMateRules": [
        {
            "scope": [
                "comment.line.double-slash.evt",
                "constant.numeric.prefix.evt"
            ],
            "settings": {
                "foreground": "#a9a9a9", // Dark Gray
                "fontStyle": "italic" // fontStyles work for pretty much everything
            }
        }
    ]
}
```

See the tutorial video for more details, as linked above in the overview. The different scopes follow in sections:
