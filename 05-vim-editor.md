# Vim Editor
**Notes by Sakshi Chavan**

---

Vim has **3 modes**. Get comfortable switching between them and you'll fly through files.

## 1. Command Mode (default on open)

Used for navigation, deleting, copying — no typing text here.

**Line ops**
```
dd       delete current line
2dd      delete 2 lines
10dd     delete 10 lines
yy       yank (copy) current line
2yy      yank 2 lines
p        paste
10p      paste 10 times
u        undo
Ctrl+r   redo
```

**Word ops**
```
dw       delete current word
7dw      delete next 7 words
```

**Jumping around**
```
gg       go to first line
20gg     go to line 20
G        go to last line
M        middle of screen
H        top of screen
L        bottom of screen
```

**Searching**
```
/word    search forward for "word"
n        next match
N        previous match
```

## 2. Insert Mode (for actually typing)

```
i    insert before cursor
I    insert at start of line
a    insert after cursor
A    insert at end of line
o    new line below, insert
O    new line above, insert
r    replace one character
R    replace multiple characters (overwrite mode)
```

Exit back to command mode: `Esc`

## 3. Ex Mode / Command-Line Mode

Enter with `:`

**Saving & quitting**
```
:q      quit
:q!     force quit (discard changes)
:w      save
:w!     force save
:wq     save & quit
:x      save & quit (same as :wq)
```

**Display**
```
:set nu       show line numbers
:set nonu     hide line numbers
:n            jump to line n
```

**Find & replace**
```
:%s/old/new/g
```
Example: `:%s/sshd/cbz/g` replaces every "sshd" with "cbz" in the file.

**Running shell commands from inside vim**
```
:!command
:!touch file1.txt
:!touch file{1..100}.txt
:!mkdir dir2
```

## My takeaways / best practices

- Save before you quit — always
- `u` / `Ctrl+r` are your safety net, use them
- `/search` beats scrolling every time
- Turn on line numbers when debugging or referencing specific lines
- `:!command` is a nice trick to avoid leaving vim for quick shell tasks

---
*Notes by Sakshi Chavan — for personal learning & LinkedIn sharing*
