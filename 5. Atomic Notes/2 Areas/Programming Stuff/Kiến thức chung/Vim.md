2025-07-26 16:38
Status: #baby
Tags: [[computer science]] [[productivity]]
## Main
## 🧱 Modes

|Key|Mode|
|---|---|
|`Esc`|Normal mode|
|`i`|Insert before cursor|
|`I`|Insert at line start|
|`a`|Append after cursor|
|`A`|Append at line end|
|`v`|Visual mode|
|`V`|Visual line mode|
|`:`|Command-line mode|
|`R`|Replace mode|

---

## 🚀 File Operations

|Command|Description|
|---|---|
|`:e file`|Open file|
|`:w`|Save file|
|`:w file`|Save as new file|
|`:q`|Quit|
|`:q!`|Quit without saving|
|`:wq` / `ZZ`|Save and quit|
|`:x`|Save and quit (if changed)|

---

## ⌨️ Insert Mode

|Key|Description|
|---|---|
|`i`|Insert before cursor|
|`a`|Append after cursor|
|`o`|Open line below|
|`O`|Open line above|
|`Esc`|Exit to normal mode|

---

## 🧭 Movement

|Key|Moves cursor|
|---|---|
|`h`|Left|
|`l`|Right|
|`j`|Down|
|`k`|Up|
|`0`|Beginning of line|
|`^`|First non-blank on line|
|`$`|End of line|
|`w`|Next word|
|`b`|Previous word|
|`gg`|Top of file|
|`G`|Bottom of file|
|`:n`|Go to line n|

---

## ✂️ Editing

|Command|Description|
|---|---|
|`x`|Delete character|
|`dd`|Delete line|
|`dw`|Delete word|
|`d$`|Delete to end of line|
|`yy`|Yank (copy) line|
|`p`|Paste after cursor|
|`P`|Paste before cursor|
|`u`|Undo|
|`Ctrl+r`|Redo|
|`r<char>`|Replace one character|
|`cc`|Change (delete and insert line)|

---

## 🔍 Searching

| Command         | Description                    |
| --------------- | ------------------------------ |
| `/word`         | Search forward for "word"      |
| `?word`         | Search backward for "word"     |
| `n` / `N`       | Repeat search forward/backward |
| `:%s/old/new/g` | Replace all                    |
| `:noh`          | Remove search highlight        |

---

## 📋 Visual Mode

|Command|Description|
|---|---|
|`v`|Start character selection|
|`V`|Start line selection|
|`Ctrl+v`|Start block (column) selection|
|`y`|Yank selection|
|`d`|Delete selection|
|`>` / `<`|Indent / un-indent block|

---

## 🔄 Macros and Registers

|Command|Description|
|---|---|
|`q<letter>`|Start recording macro|
|`<commands>`|Execute desired commands|
|`q`|Stop recording|
|`@<letter>`|Play macro|
|`@@`|Repeat last macro|

---

## 🔌 Window Splits

|Command|Description|
|---|---|
|`:split`|Horizontal split|
|`:vsplit`|Vertical split|
|`Ctrl+w`|Start window command|
|`Ctrl+w h`|Move to left window|
|`Ctrl+w l`|Move to right window|
|`Ctrl+w q`|Close current split|

---

## 🧩 Buffers & Tabs

| Command      | Description                |
| ------------ | -------------------------- |
| `:ls`        | List open buffers          |
| `:b1`, `:b2` | Switch to buffer 1, 2, ... |
| `:tabnew`    | Open new tab               |
| `gt`, `gT`   | Next / previous tab        |
| `:tabclose`  | Close current tab          |


## References