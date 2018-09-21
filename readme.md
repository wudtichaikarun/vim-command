# HOW TO USE VIM

## vim mode

- normal/command mode
- insert mode, type 'i'.
- leave insert mode, press Escape.
- command line mode, type ':'

## help

```
vimtutor  //open vim document
//open help document about command ex. :help dd,previous document ⌃o,forword ⌃i
⇧⌘Space //open Emoji & Symbols
```

## plugin NERDTree

```
⌃ww   //swith display
⌃t    //open NERDTree(like tab to see all file in folder)
```

## Iterm2

```
⌘→, ⌘← //next tab, previous tab
```

## Delete

```
s   //delete and use 'insert mode'
S   //delete current line and use 'insert mode'

x   //delete(cut) current cursor
X   //delete(cut) front cursor (like press delete)

dh  //deltete front cursor
dj  //deltete current line and upper line
dk  //delete current line and lower line
dl  //delete current cursor

dd  //delete current line
d3w //delete 3 word
3dd //delete 3 line

D   //delete the characters under the cursor until the 'end' of the line
d$  //delete the characters under the cursor until the 'end' of the line
d0, d^  //delete the characters under the cursor until the 'start of the line
```

## Deleteing, Yanking and Putting

**Standard vs Vim**

- cut = delete
- copy = yank
- paste = put

```
2yw //yank 2 word
yw  //yank word
yy  //yank all line

p //put after cursor
P //put before cursor
```

**Register type**

`:reg` look at the registers

- Unnamed register = ""

  - "" holds text from d, c, s, x, and y operations

- Numbered registers = "0 "1 ... "9 <i>**"automatic add"**</i>

  - "0 holds last text yanked(y)
  - "1 holds last text deleted(d) or changed(c)
  - Numbered registers shift with each d or c

- Named <i>**"manual add"**</i>

  - `"a` or another characters like b, c, d ... z
  - `"ayy` append current line to the "a register
  - `"ayiw` append word to the "a register
  - `"ap` put text from register "a

example.

```
before => Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do
1. "byy //append current line to "b register
2. "bp  // put text from the register "b
after => Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do
         Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do
```

**Repeating with Registers**

- [count][register]operator or [register][count]operator

example.

```
before => Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed

1. "ayy // register current line to register "a
2. 2"ap // [count][register]operator put 2 line from register a

after => Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed
         Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed
         Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed
```

**Black hole register**

`"_` use to delete text without affecting the normal registers.

```
1."_dd //delete current line
2.p //put Unnamed register
```

## Undo, redo

```
u   //undo
^r  //redoes
```

## Write
