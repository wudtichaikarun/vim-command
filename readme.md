# HOW TO USE VIM

## vim mode

- normal/command mode
- insert mode, type 'i'.
- leave insert mode, press Escape.
- command line mode, type ':'
- replacing mode type 'R'

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

## Inserting, Changing, Replacing, Joining

- inserting

```
i //insert before the cursor
I //insert at the beginning of the line

a //insert (append) after the cursor
A //insert (append) at the end of the line

o //append (open) a new line below the current line
O //append (open) a new line above the current line

ea //insert (append) at the end of the word
```

- changing mode press `c` `ciw` change in word

```
C, c$   //change(delete) from cursor to the end of line
c0, c^  //change(delete) from cursor to the start of line
cc      //change(delete) current line
3cc     //change(delete) 3 line
ciw     //change in word or just cw
```

- changing to uppercase

```
~  //swith character to uppercase/lowercase
g~w //change the word start from cursor to uppercase
g~iw //change the word to uppercase
g~$ //CHANGE THE LINE TO uppercase
g~~ //swith the character to uppercase/lowercase

yy U //change current line to uppercase
yiw U //change current word to uppercase

gUw  //change current word to uppercase
gUU  //change current line to uppercase

guw  //change current word to lowercase
guu  //change current line to lowercase
```

- replacing mode press `R`
- repeat(vertical) word, symbol
  - `[count]i[word]esc`
- repeat(horizontal) multiple line
  - `[count]o[word]esc`

example create a line of 20 asterisks(**\*....**).

```
// repeat(vertical)
20i*esc //********************

// repeat(horizontal)
5o#esc  #
        #
        #
        #
        #
4o192.168.1.1  // 192.168.1.1
                  192.168.1.1
                  192.168.1.1
                  192.168.1.1
```

- joining

```
J  //join line
gJ //join with out write space
3J //join 3 line together
```

## Search, Find and Replace

- find

  - f{char} find
  - F{char} find backward
  - ; repeat find in the same direction
  - , repeat find in the opposite direction
  - t{char} forward till search
  - T{char} reverse till search
  - `*` forward search for word
  - `#` reverse search for word
  - /pattern search for pattern
  - ?pattern search backward for pattern

```
fa //find forward a
Fa //find backword a

// f(find)
fspace  //move cursor to white space
2fspace //move cursor to 2 white spcae

// t is till(untill)
ti //move forward to one character befor i
Ti //move backword to one character after i

// t(till) and d(delete)
dta //delete until before a
```

- find from word or fomat **incsearch** turn on/off `:set is`/`:set nois` check on or off `:set is ?`

```
// symblo / is incsearch
/romantic //find and highlight word romantic press n or N for find next word
:noh      //no highlight
```

- find and replace

```
before => i and you
          you and me
1. /and enter //find word 'and'
2. ciw, cw //change in word
3. &       //use & instand of 'and'
4. n or N  //next word 'and'
3. .       //repeat comand befor
after => i & you
         you & me
```

- `d` delete current position untill `/xxx`

```
d/romantic //delete from current cursor position until word romantic
```

- replaces current line with new text `:s/old/new/` , `:s/old/new/[flages]` , `[range]s/old/new/[flage]`

[flages] ex. g for change all word

[range] `$ = last line`, `. = current line`, `.,$ = current line -> last line`, `% = all line (entire file)`

```
//:s/old/new/[flages]
:s/romantic/someText/   //replaces romantic with someText in current line
:s/romantic/someText/g  //replaces all romantic with someText in current line

// :[range]s/old/new/g
:.,$s/romantic/someText/g //replaces all romantic with someText start curret line -> last line
:%s/romantic/someText/g   //replaces all romantic with someText all line in the file
:1,$s/romantic/someText/g //same in top
```

**replace `/var/app/mail` with `/user/local/mail`**

```
//hard way
:s/\var\/app/\/user\/local/

//good way
:s#/var/app#/user/local#
```

**reposition to center `zz` reposition to top `z + enter`**

**open/close line number** `:set nu` / `:set nonu` swith on->off off->on `set nu!`

## Text Object and Macros

- Text Object

  - {operator}{a}{object} ex. `daw` Delete A Word (delete white space also)
  - {operator}{i}{object} ex. `diw` Delete Inner Word, `ciw` Change Inner Word

```
diw  // Delete Inner Word
daw  // Delete A Word and white space

dis  // Delete Inner Sentence
das  // Delete A Sentence and white space

dip  // Delete Inner Paragraph (have a blank line)
dap  // Delete A Paragraph (don't have a blank line)

da]  // Delete A [] and all content inside
ci]  // Change Inner []

<html>
yi>  // yank(copy) Inner <> :reg unname = html
ya>  // yank(copy) A <> :rag unname = <html>

<p> sometext </p>
cit  // Change Inner Tag result = <p></p>

a{ = a} = aB
i{ = a} = iB
```

- Macros
