# Vim / Neovim Cheat Sheet — Practical Guide

> **For:** Linux / WSL / C++ / Rust / Python / Backend development  
> **Goal:** Master the Vim editing model and the commands you'll actually use.

---

# 0. The Vim Mental Model

Vim is built around **modes**.

```text
NORMAL  → navigate, manipulate, commands
INSERT  → type text
VISUAL  → select text
COMMAND → : commands
```

The most important key:

```text
Esc
```

When confused, press:

```text
Esc
```

That returns you to **Normal mode**.

---

# 1. The Commands You Must Know First

| Action | Command |
|---|---|
| Enter insert mode | `i` |
| Insert at end of line | `A` |
| Insert at beginning of line | `I` |
| Append after cursor | `a` |
| Append at end of line | `A` |
| New line below | `o` |
| New line above | `O` |
| Return to Normal mode | `Esc` |
| Save | `:w` |
| Quit | `:q` |
| Save + quit | `:wq` |
| Quit without saving | `:q!` |
| Save + quit | `ZZ` |

**Memorize these first.**

---

# 2. Navigation

## Basic Movement

| Action | Command |
|---|---|
| Left | `h` |
| Down | `j` |
| Up | `k` |
| Right | `l` |

Think:

```text
      k
      ↑
h ←       → l
      ↓
      j
```

## Word Movement

| Action | Command |
|---|---|
| Next word | `w` |
| Previous word | `b` |
| End of word | `e` |
| Beginning of word | `0` / `^` |
| End of line | `$` |

### Important distinction

```text
w    next word
e    end of word
b    backward word
```

---

# 3. File Navigation

| Action | Command |
|---|---|
| Top of file | `gg` |
| Bottom of file | `G` |
| Go to line | `:123` |
| Go to line | `123G` |
| Current line info | `Ctrl-g` |
| Half page down | `Ctrl-d` |
| Half page up | `Ctrl-u` |
| Full page down | `Ctrl-f` |
| Full page up | `Ctrl-b` |
| Center screen | `zz` |
| Top of screen | `zt` |
| Bottom of screen | `zb` |

---

# 4. Insert Mode

| Action | Command |
|---|---|
| Insert before cursor | `i` |
| Insert at line beginning | `I` |
| Append after cursor | `a` |
| Append at line end | `A` |
| New line below | `o` |
| New line above | `O` |

Typical workflow:

```text
Esc
↓
Normal mode
↓
i
↓
Insert text
↓
Esc
↓
Normal mode
```

---

# 5. Delete

| Action | Command |
|---|---|
| Delete character | `x` |
| Delete character before cursor | `X` |
| Delete line | `dd` |
| Delete to next word | `dw` |
| Delete inside word | `diw` |
| Delete to end of line | `D` |
| Delete inside quotes | `di"` |
| Delete inside parentheses | `di(` |
| Delete inside brackets | `di[` |

---

# 6. Change

`c` means **change**.

| Action | Command |
|---|---|
| Change word | `cw` |
| Change inside word | `ciw` |
| Change line | `cc` |
| Change to end of line | `C` |
| Change inside quotes | `ci"` |
| Change inside parentheses | `ci(` |
| Change inside brackets | `ci[` |
| Change around quotes | `ca"` |
| Change around parentheses | `ca(` |

This is one of Vim's biggest strengths.

---

# 7. The Vim Grammar

Many Vim commands follow:

```text
[count] [operator] [motion/text-object]
```

Examples:

```text
dw
```

```text
diw
```

```text
ci"
```

```text
3dd
```

```text
d$
```

Think:

```text
d + motion
c + motion
y + motion
```

This composability is the heart of Vim.

---

# 8. Operators

| Operator | Meaning |
|---|---|
| `d` | Delete |
| `c` | Change |
| `y` | Yank/copy |
| `>` | Indent |
| `<` | Unindent |
| `=` | Auto-indent |
| `g~` | Toggle case |

Examples:

```text
dw
cw
yw
d$
y$
```

---

# 9. Yank / Copy / Paste

| Action | Command |
|---|---|
| Yank line | `yy` |
| Yank word | `yw` |
| Yank to end of line | `y$` |
| Yank selected text | `y` |
| Paste after cursor | `p` |
| Paste before cursor | `P` |
| Duplicate line | `yyp` |

Example:

```text
yy
p
```

copies the current line below itself.

---

# 10. Undo / Redo

| Action | Command |
|---|---|
| Undo | `u` |
| Redo | `Ctrl-r` |
| Repeat last change | `.` |

### The `.` command

This is extremely important.

If you perform:

```text
ciw
```

and replace a word, then:

```text
.
```

repeats that change.

Think:

> **`.` = repeat my last change**

---

# 11. Visual Mode

Visual mode is Vim's selection system.

| Mode | Command |
|---|---|
| Character selection | `v` |
| Line selection | `V` |
| Block selection | `Ctrl-v` |

Then use normal movement.

Example:

```text
v
w
w
y
```

Select two words and yank them.

---

# 12. Visual Editing

After selecting text:

```text
d
```

delete.

```text
y
```

copy.

```text
c
```

change.

```text
>
```

indent.

```text
<
```

unindent.

---

# 13. Indentation

| Action | Command |
|---|---|
| Indent line | `>>` |
| Unindent line | `<<` |
| Auto-indent line | `==` |
| Indent selection | `>` |
| Unindent selection | `<` |

For multiple lines:

```text
3>>
```

---

# 14. Search

| Action | Command |
|---|---|
| Search forward | `/pattern` |
| Search backward | `?pattern` |
| Next match | `n` |
| Previous match | `N` |
| Search word under cursor | `*` |
| Search previous occurrence | `#` |

Example:

```text
/function_name
```

Press:

```text
n
```

to move through matches.

---

# 15. Replace

Current line:

```text
:s/old/new/
```

Whole file:

```text
:%s/old/new/g
```

Whole file with confirmation:

```text
:%s/old/new/gc
```

Useful flags:

```text
g = all matches on each line
c = confirm
```

---

# 16. Marks

Marks let you remember locations.

Set a mark:

```text
ma
```

Jump to mark:

```text
'a
```

Backtick version:

```text
`a
```

The difference:

```text
'a   → line
`a   → exact position
```

---

# 17. Jumping Around Code

| Action | Command |
|---|---|
| Matching bracket | `%` |
| Previous jump | `Ctrl-o` |
| Next jump | `Ctrl-i` |
| Definition / tag | `Ctrl-]` |
| Jump back | `Ctrl-t` |
| Top of file | `gg` |
| Bottom | `G` |

`%` is especially useful for:

```cpp
if (condition) {
    ...
}
```

Place cursor on `{` and press `%`.

---

# 18. Search + Replace Workflow

A practical workflow:

```text
/old_name
```

Find the text.

Then:

```text
:%s/old_name/new_name/gc
```

Confirm replacements one by one.

---

# 19. Buffers

A **buffer** is an open editing area.

Useful commands:

| Action | Command |
|---|---|
| List buffers | `:buffers` |
| Open file | `:e file.cpp` |
| Next buffer | `:bnext` |
| Previous buffer | `:bprev` |
| Switch buffer | `:buffer name` |
| Delete buffer | `:bd` |

In Neovim, fuzzy finders such as Telescope may make this easier.

---

# 20. Windows / Splits

| Action | Command |
|---|---|
| Horizontal split | `:split` / `Ctrl-w s` |
| Vertical split | `:vsplit` / `Ctrl-w v` |
| Move left | `Ctrl-w h` |
| Move down | `Ctrl-w j` |
| Move up | `Ctrl-w k` |
| Move right | `Ctrl-w l` |
| Next window | `Ctrl-w w` |
| Close window | `Ctrl-w q` |
| Equalize windows | `Ctrl-w =` |

In Neovim, you can use your configured keybindings instead.

---

# 21. Tabs

Vim tabs are better thought of as **collections of windows**, not browser-style files.

| Action | Command |
|---|---|
| New tab | `:tabnew` |
| Next tab | `gt` |
| Previous tab | `gT` |
| First tab | `1gt` |
| Last tab | `:tablast` |
| Close tab | `:tabclose` |

---

# 22. Macros

Record a macro into register `q`:

```text
qq
```

Perform your commands.

Stop recording:

```text
q
```

Replay:

```text
@q
```

Repeat:

```text
@@
```

Repeat macro multiple times:

```text
10@q
```

Macros are extremely powerful for repetitive transformations.

---

# 23. Registers

Vim has registers for storing text and commands.

View registers:

```text
:registers
```

Unnamed register:

```text
""
```

Named register:

```text
"ayy
```

Yank line into register `a`.

Paste:

```text
"ap
```

---

# 24. Command Mode

Press:

```text
:
```

Then execute commands.

Important examples:

```text
:w
:q
:wq
:q!
:e file.cpp
:buffers
:split
:vsplit
:terminal
:set number
:set relativenumber
```

---

# 25. External Shell Commands

Run a shell command from Vim:

```text
:!ls
```

Compile:

```text
:!g++ main.cpp -o main
```

Run:

```text
:!./main
```

In Neovim, you will often use terminals, plugins, or task runners instead.

---

# 26. Terminal

Vim/Neovim can open terminals.

Neovim:

```text
:terminal
```

You can also configure terminal toggles.

For your WSL workflow, this is useful for:

```text
cargo
cmake
make
git
python
docker
```

---

# 27. C/C++ Workflow

With a modern Neovim setup such as NvChad:

```text
1. Open project
2. Navigate files
3. Edit
4. LSP diagnostics
5. Jump to definition
6. Search references
7. Build
8. Test
9. Git
```

Useful core Vim commands:

```text
gd
```

Go to definition if provided by your LSP configuration.

```text
gr
```

Find references if configured.

```text
K
```

Show documentation/hover information if configured.

These are **LSP mappings**, not universal Vim commands.

---

# 28. Rust Workflow

For Rust projects:

```text
:terminal
```

Then:

```bash
cargo check
cargo test
cargo build
cargo run
```

With `rust-analyzer` configured, you can use LSP features such as:

```text
gd
gr
K
```

depending on your NvChad configuration.

---

# 29. Python Workflow

Typical terminal commands:

```bash
python main.py
pytest
ruff check .
```

Neovim + LSP can provide:

- completion
- diagnostics
- definitions
- references
- documentation
- formatting

Again, these capabilities come from your **Neovim configuration/plugins**, not core Vim.

---

# 30. Git

From Vim:

```text
:!git status
```

or use your terminal.

Modern Neovim workflows often use plugins for:

- Git signs
- staging
- diffs
- commits
- history
- merge conflicts

If you use NvChad, learn its configured Git workflow separately.

---

# 31. File Explorer

Classic Vim:

```text
:Explore
```

Neovim can use:

- built-in netrw
- Telescope
- nvim-tree
- oil.nvim
- other file managers

Your NvChad setup determines what you already have.

---

# 32. Vim Help — Extremely Important

Vim has a fantastic built-in help system.

```text
:help
```

Specific topic:

```text
:help motion
```

```text
:help text-objects
```

```text
:help registers
```

```text
:help macros
```

```text
:help usr_01
```

Search help:

```text
:helpgrep keyword
```

If you don't know how something works:

```text
:help something
```

---

# 33. Text Objects — The Secret Weapon

Text objects are one of Vim's most powerful concepts.

Common ones:

```text
iw   inner word
aw   a word
i"   inside quotes
a"   around quotes
i'   inside single quotes
a'   around single quotes
i(   inside parentheses
a(   around parentheses
i[   inside brackets
a[   around brackets
i{   inside braces
a{   around braces
it   inside HTML/XML tag
```

Combine them with operators.

Examples:

```text
diw
ciw
yiw

di"
ci"
yi"

di(
ci(
yi(
```

This is the part of Vim you should really master.

---

# 34. Counts

Most commands can accept a count.

Examples:

```text
3j
```

Move down 3 lines.

```text
5dd
```

Delete 5 lines.

```text
3w
```

Move 3 words.

```text
10@q
```

Run macro 10 times.

This makes commands composable.

---

# 35. `f` and `t` Navigation

Very useful for code.

```text
fa
```

Jump forward to next `a`.

```text
ta
```

Jump forward until before `a`.

Backward:

```text
Fa
Ta
```

Repeat:

```text
;
```

Reverse:

```text
,
```

Example:

```cpp
std::cout << "hello";
```

You can quickly navigate to punctuation/characters without moving character-by-character.

---

# 36. `g` Commands Worth Knowing

| Command | Action |
|---|---|
| `gg` | Top of file |
| `g_` | Last non-whitespace character |
| `ge` | End of previous word |
| `gd` | Go to definition (often LSP) |
| `gr` | Find references (often LSP) |
| `gf` | Open file under cursor |
| `gi` | Go to last insert position |
| `g;` | Previous change location |
| `g,` | Next change location |

Some of these are built-in Vim features; LSP ones depend on your configuration.

---

# 37. Change History

Useful navigation:

```text
u
```

Undo.

```text
Ctrl-r
```

Redo.

```text
g;
```

Jump to previous change.

```text
g,
```

Jump to next change.

---

# 38. The Dot Command

Remember:

```text
.
```

It repeats the last change.

Example:

```text
ciw
```

replace a word.

Then move somewhere else:

```text
.
```

Same edit happens again.

This is one of the most valuable Vim habits.

---

# 39. Vim's Core Grammar

Think like this:

```text
operator + motion
```

Examples:

```text
d + w   → dw
c + w   → cw
y + w   → yw
```

Or:

```text
operator + text object
```

Examples:

```text
d + iw  → diw
c + i"  → ci"
y + i(  → yi(
```

And:

```text
count + command
```

Examples:

```text
3dd
5j
10@q
```

This is why Vim becomes powerful with practice.

---

# 40. Vim vs Neovim

If you're using **NvChad**, you're actually using:

```text
Neovim
+
NvChad configuration
+
plugins
+
Lua configuration
```

Core Vim knowledge still applies.

But features such as:

```text
LSP
completion
Telescope
file explorer
Git integration
formatting
debugging
```

are generally provided by Neovim's ecosystem/configuration.

Don't confuse:

```text
Vim command
```

with:

```text
NvChad keybinding
```

---

# 41. The 30 Commands I Recommend Memorizing

If you only memorize these, you'll already be dangerous:

```text
Esc          Normal mode
i            Insert
a            Append
o            New line below
O            New line above

h j k l      Navigation
w            Word forward
b            Word backward
e            Word end
0            Line start
$            Line end
gg           File start
G            File end

dd           Delete line
dw           Delete word
diw          Delete inside word
ciw          Change inside word
yy           Yank line
p            Paste
u            Undo
Ctrl-r       Redo
.            Repeat

v            Visual
V            Visual line
Ctrl-v       Visual block

/            Search
n            Next match
N            Previous match
%            Matching bracket

:w           Save
:q           Quit
:wq          Save + quit
:q!          Quit without saving

Motions + operators + text objects
```

---

# 42. The 80/20 Learning Path

## Level 1 — Survival

Master:

```text
Esc
i
a
o
:w
:q
:wq
:q!
```

## Level 2 — Navigation

Master:

```text
h j k l
w b e
0 $
gg G
Ctrl-d Ctrl-u
```

## Level 3 — Editing

Master:

```text
dd
dw
d$
cc
cw
ciw
yy
p
u
Ctrl-r
.
```

## Level 4 — Text Objects

Master:

```text
iw
aw
i"
a"
i(
a(
i[
a[
i{
a{
```

Then combine:

```text
diw
ciw
yiw
di"
ci"
di(
ci(
```

## Level 5 — Advanced Editing

Learn:

```text
Visual mode
macros
registers
marks
search/replace
counts
f/t motions
jump history
```

## Level 6 — Neovim

Then learn:

```text
LSP
Telescope
Treesitter
Git
DAP
formatters
linters
terminal workflow
Lua configuration
```

Because you're already using **NvChad**, you're probably somewhere around Level 5–6.

---

# 43. Emergency Commands

Something weird?

```text
Esc
```

Still weird?

```text
Esc
Esc
```

Need to cancel a command:

```text
Esc
```

Need to quit without saving:

```text
:q!
```

Need to understand something:

```text
:help command
```

---

# 44. The Vim Philosophy

Don't think:

> "I need to memorize hundreds of commands."

Think:

> **"I need to learn a small set of operators, motions, and text objects that I can compose."**

The core model:

```text
                 Vim
                  │
       ┌──────────┼──────────┐
       ↓          ↓          ↓
   Operators    Motions   Text Objects
       │          │          │
       └──────────┼──────────┘
                  ↓
            Composable edits
```

Examples:

```text
d + w
c + i + w
y + i + "
3 + d + d
```

That's the real Vim skill.

---

# 45. Your Practice Challenge

Open a real C++/Rust/Python file in NvChad and practice:

```text
1. Move without arrow keys
2. Jump word-by-word
3. Search for a function
4. Change a variable using ciw
5. Delete text inside parentheses
6. Copy a line
7. Duplicate a line
8. Change text inside quotes
9. Jump between brackets with %
10. Use . to repeat an edit
11. Use a macro for repetitive changes
12. Split the window
13. Switch buffers
14. Search and replace
15. Jump through changes
```

Do this until the commands stop feeling like commands.

The goal is:

```text
Think about the edit
        ↓
Execute the edit
```

rather than:

```text
Think about which key to press
        ↓
Execute the key
```

---

# Quick Reference

```text
MODES
Esc           Normal
i             Insert
v             Visual
V             Visual line
Ctrl-v        Visual block
:             Command-line

MOVEMENT
h j k l       Left/down/up/right
w             Word forward
b             Word backward
e             Word end
0             Line start
$             Line end
gg            File start
G             File end
Ctrl-d        Half page down
Ctrl-u        Half page up
%             Matching bracket
f<char>       Find character
t<char>       Till character
;             Repeat f/t
,             Reverse f/t

EDITING
i             Insert
a             Append
o             New line below
O             New line above
dd            Delete line
dw            Delete word
diw           Delete inside word
ciw           Change inside word
yy            Yank line
p             Paste
u             Undo
Ctrl-r        Redo
.             Repeat change

TEXT OBJECTS
iw            Inner word
aw            A word
i" / a"       Quotes
i' / a'       Single quotes
i( / a(       Parentheses
i[ / a[       Brackets
i{ / a{       Braces
it / at       Tag

SEARCH
/pattern      Search forward
?pattern      Search backward
n             Next
N             Previous
*             Word under cursor
#             Previous word match
:%s/a/b/g     Replace all

VISUAL
v             Character
V             Line
Ctrl-v        Block
y             Yank
d             Delete
c             Change
>             Indent
<             Unindent

FILES
:w            Save
:q            Quit
:wq           Save + quit
:q!           Force quit
:e file       Open file
:buffers      List buffers

WINDOWS
Ctrl-w s      Horizontal split
Ctrl-w v      Vertical split
Ctrl-w h/j/k/l Move window
Ctrl-w o      Keep current window
Ctrl-w q      Close window

BUFFERS
:bnext        Next
:bprev        Previous
:bd           Delete buffer

TABS
gt            Next tab
gT            Previous tab
:tabnew       New tab

MACROS
qq            Record into q
q             Stop recording
@q            Play macro
@@            Repeat macro

HELP
:help         Help
:help motion
:help text-objects
:help macros
:helpgrep     Search help
```

---

## The One Sentence to Remember

> **Vim is not about memorizing shortcuts; it's about composing operators + motions + text objects into precise edits.**
