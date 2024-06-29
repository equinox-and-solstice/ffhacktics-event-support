# Overview

This is an unofficial extension for hacking Final Fantasy Tactics, specifically event scripting. It builds on the content provided by the [FFHacktics community](https://ffhacktics.com/) and as such refers to all such content in the function data (including linking to the [wiki](https://ffhacktics.com/wiki/Main_Page)).

[![License: CC BY-NC 4.0](https://img.shields.io/badge/License-CC%20BY--NC%204.0-lightgrey.svg)](http://creativecommons.org/licenses/by-nc/4.0/)
Share it and don't sell it...

Enjoy and happy hacking 😁

**Features and tutorials**

As long as your open event file's extension is `.evt` (such as `event.evt`):

- Named function hover, code completion, and signature help support
  - **Tutorial**: [crash course video](https://www.youtube.com/watch?v=btLANdB91fg); includes extension installation
  - Function info displaying [![Requires Event Instruction Upgrade - click for Wiki page](./icon/EIU_icon.png)](https://ffhacktics.com/wiki/Event_Instruction_Upgrade) indicates the function requires the Event Instruction Upgrade; click the icon where shown to link to the wiki page for details, including where to download
- Code snippets (see below)
- Syntax highlighting (see below for formatting scopes) and language support

---

## Snippets

Snippets create quick blocks of text for common code sections, and allow you to `[Tab]` through and set different pieces as available.

The following table details the current collection of snippets, and the codes to use them. Type the code (and optionally press `[Ctrl]` + `[.]`), and select from the dropdown to spark snippet insertion.

| Snippet Title              | Code       | Description                                 |
|----------------------------|:----------:|---------------------------------------------|
| Regions                    | `creg`     | Creates region opening and closing tags.    |
| Create Message             | `msg`      | Supplies a flexible message setup.          |
| Unit Setup                 | `setup`    | Loads units into the event map.             |
| Camera Setup               | `csetup`   | Supplies a default collection of camera calls for initial setup. |
| Say Message                | `smsg`     | Sets a unit to speak.                       |
| Exchange Messages          | `emsg`     | Sets 2 units to speak.                      |
| Dialogue (longer Exchange) | `dmsg`     | Sets 2 units to talk back and forth.        |
| Unit Move                  | `move`     | Sets a unit walking a certain distance away on the event map. |
| Unit Enter                 | `enter`    | Brings a unit into the event map.           |
| Unit Exit                  | `exit`     | Sends a unit out of the event map.          |
| End Battle                 | `endbat`   | Optionally revives unit x01, and turns the player team to face them. |
| Clear Map                  | `clearmap` | Removes all units from view.                |
| Fade Out                   | `fadeout`  | Fades the event map to black.               |
| Zoom Out                   | `zoomout`  | Raises the camera 500 units after a battle. |

---

## Syntax Highlighting

This extension provides enhanced syntax highlighting for `.evt` files, specific to the event functions as defined by the FFHacktics community. Below are the scopes you can style in your editor to customize the appearance of FFHackticsEvent code.

### Scope Overview

This section mainly contains tables of file scopes, which identify different parts of the code. This table describes how the file scope tables work. _For this overview table only_, read each column downward, not each row across:

| Scope | Description | "Foreground?" values |
| --- | --- | --- |
| `scope.name.evt.example` | Targets certain elements for styling, specifically those of the `scope.name.evt.example` scope. | **Yes**: you can set the rule's `settings`' `foreground` property and see results. 
| | An **example** of such a scope is for code comments, `comment.line.double-slash.evt`. | **Maybe**: VS Code may override this. |
| | **Note**: if you specify a setting for `scope.name.evt`, it will also work for things like `scope.name.evt.example`, `scope.name.evt.example.end`, etc. When you specify settings for these latter / child scopes, it overrides the former / parent scope __for that content only__. | **No**: VS Code probably overrides this. |
| | **That is**, specifying `comment.line.double-slash.evt.message` settings will override `comment.line.double-slash.evt`, but _only for comment parts like `Message x01`_. The rest of the comment style (the `//`, any other text) retains the style you set for `comment.line.double-slash.evt`. | **_In any case_**: you can still set the `fontStyle` property. |

### How do I use this?

The short answer is that in your `settings.json` file, you set formatting for a given scope (or multiple). See the following example for formatting both event script comments and number prefixes to dark gray. The table shows the scope information, and the code shows how to set it up in your JSON:

  | Scope | Description | Foreground? |
  | --- | --- | --- |
  | `punctuation.definition.comment.evt` | The two slashes (`//`) that define the start of a comment. | Yes |
  | `constant.numeric.prefix.evt` | Any number prefixes (`x` and `r`). | Yes |

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

### Text and Comments (`//`)
  
  | Scope | Description | Foreground? |
  | --- | --- | --- |
  | `source.evt` | Usually ends up just as message text. Actually governs all file text, but the other scopes and styles override most of it (including VS Code theme / default styles). | Yes |
  | `punctuation.definition.comment.evt` | The two slashes (`//`) that define the start of a comment. | Yes |
  | `comment.line.double-slash.evt` | General comments. | Yes |
  | `comment.line.double-slash.evt.message` | The _`Message x01`_ part of comments including text like `//Message x01`. | Yes |

### Numeric Constants

#### Common Numeric Constant Scopes

  | Scope | Description | Foreground? |
  | --- | --- | --- |
  | `constant.numeric.prefix.evt` | Any number prefixes (`x` and `r`). | Yes |
  | `constant.numeric.evt` | Any numbers in any types of bytes and words (the _`00`_ part of `x00`...) | Yes |
  | `entity.name.variable.parameter.evt` | Any parameter values (`x00`, `+12345`, `r01000000`...) | No |
  | `entity.name.variable.parameter.evt.hex` | Any hexadecimal values (`x00`, `x0010`...) | No |
  | `entity.name.variable.parameter.evt.decimal` | Any base 10 decimal values (`060`, `-04096`...) | No |

#### Hexadecimal Values

  | Scope | Description | Foreground? |
  | --- | --- | --- |
  | `constant.numeric.prefix.evt.hex` | Prefix for hexadecimal numbers (`x`). | Yes |
  | `constant.numeric.evt.hex.byte` | Hexadecimal numbers in a byte (the _`00`_ part of `x00`). | Yes |
  | `constant.numeric.evt.hex.word` | Hexadecimal numbers in a word (the _`0000`_ part of `x0000`). | Yes |
  | `entity.name.variable.parameter.evt.hex.byte` | Hexadecimal byte values (`x00` to `xFF`). | No |
  | `entity.name.variable.parameter.evt.hex.word` | Hexadecimal word values (`x0000` to `xFFFFFFFF`). | No |
  
#### Decimal Values

  | Scope | Description | Foreground? |
  | --- | --- | --- |
  | `keyword.operator.arithmetic.evt` | Prefix for signed decimal values (the _`+`_ or _`-`_ in values like `+000`). | Yes |
  | `constant.numeric.evt.decimal.byte` | Decimal numbers in a byte (the _`999`_ part of `-999`). | Yes |
  | `constant.numeric.evt.decimal.word` | Decimal numbers in a word (the _`00000`_ part of `+00000`). | Yes |
  | `entity.name.variable.parameter.evt.decimal.byte` | Decimal byte values, including signs (`-999` to `000` to `+999` etc). | No |
  | `entity.name.variable.parameter.evt.decimal.word` | Decimal word values (`-9999999999` to `00000` to `+9999999999` etc). | No |

### Function Calls

#### Common Function Call Scopes

  | Scope | Description | Foreground? |
  | --- | --- | --- |
  | `meta.function-call.evt` | General function call styling. | No |
  | `punctuation.definition.parameters.evt` | Any parentheses `(` & `)` for function calls. | Yes |
  | `punctuation.definition.function.evt` | Any braces `{` & `}` for tags and numbered functions. | Yes |
  | `punctuation.separator.parameter.evt` | Any commas `,` or colons `:` separating parameters or specifiers. | Yes |

#### Named Functions

##### Common Named Function Scopes

  | Scope | Description | Foreground? |
  | --- | --- | --- |
  | `meta.function-call.evt.named` | Named functions including any passed parameters, such as `WaitAddUnit()` and `CameraSpeedCurve(xAA)`. | No |
  | `entity.name.function.evt.named` | Function names, such as _`CameraSpeedCurve`_ in `CameraSpeedCurve(xAA)`. | Yes |
  | `punctuation.definition.parameters.evt.named` | Any parentheses `(` & `)` for function parameters. | Yes |

##### Specific Named Function Scopes

  | Scope | Description | Foreground? |
  | --- | --- | --- |
  | `punctuation.separator.parameter.evt.named` | Separating commas `,` between parameters. | Yes |
  | `punctuation.definition.parameters.evt.named.begin` | Opening parenthesis `(` for function parameters. | Yes |
  | `punctuation.definition.parameters.evt.named.end` | Closing parenthesis `)` for function parameters. | Yes |

#### Numbered Functions (including r-type values):

##### Common Numbered Function Scopes

  | Scope | Description | Foreground? |
  | --- | --- | --- |
  | `meta.function-call.evt.numbered` | Numbered functions including any passed parameters, such as `{7C}()` and `{75}(r010000000000)`. | No |
  | `entity.name.function.evt.numbered` | Function numbers, such as _`75`_ in `{75}(r010000000000)`. | Yes |
  | `punctuation.definition.function.evt.numbered` | Any braces `{` & `}` for function numbers. | Yes |
  | `punctuation.definition.parameters.evt.numbered` | Any parentheses `(` & `)` for function parameters. | Yes |

##### Specific Numbered Function Scopes

  | Scope | Description | Foreground? |
  | --- | --- | --- |
  | `entity.name.variable.parameter.evt.r-type` | Full 'r'-type parameter values, such as `r010000000000`. | No |
  | `constant.numeric.evt.r-type` | Numbers in 'r'-type constants (the _`010000000000`_ in `r010000000000`). | Yes |
  | `constant.numeric.prefix.evt.r-type` | Prefix for 'r'-type numeric constants (the _`r`_ in `r010000000000`). | Yes |
  | `punctuation.definition.function.evt.numbered.begin` | Opening brace `{` for function numbers. | Yes |
  | `punctuation.definition.function.evt.numbered.end` | Closing brace `}` for function numbers. | Yes |
  | `punctuation.definition.parameters.evt.numbered.begin` | Opening parenthesis `(` for function parameters. | Yes |
  | `punctuation.definition.parameters.evt.numbered.end` | Closing parenthesis `)` for function parameters. | Yes |

#### Tagged Functions

  | Scope | Description | Foreground? |
  | --- | --- | --- |
  | `meta.function-call.evt.tag` | Tag-type functions including any specifiers, such as `{br}` and `{font:08}`. | No |
  | `entity.name.function.evt.tag` | Tag names, such as _`font`_ in `{font:08}`. | Yes |
  | `constant.numeric.evt.hex.byte.tag` | Specifier hexadecimal byte values, such as _`08`_ in `{font:08}`. | Yes |
  | `punctuation.definition.function.evt.tag` | Any braces `{` & `}` for tag functions. | Yes |
  | `punctuation.definition.function.evt.tag.begin` | Opening brace `{` for tag functions. | Yes |
  | `punctuation.definition.function.evt.tag.end` | Closing brace `}` for tag functions. | Yes |
  | `punctuation.separator.parameter.evt.tag` | The colon `:` separating the tag name and specifier. | Yes |

Use these scope identifiers to configure your theme or customize the appearance of the FFHackticsEvent syntax in your editor.
  