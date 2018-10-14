# HOW TO USE VIM

## vscode vim

- tabs (splite, close, switch)

```
:sp // splite tab horizontal
:vsp // splite tab vertical

:q  // close tab
:⌃ h  // swith to left tab
:⌃ l  // swith to right tab

:⌥ ⌘ → // swith to right tab
:⌥ ⌘ ← // swith to left tab

4o  // insert  multiple line
```

## vim mode

- normal/command mode
- insert mode, type 'i'.
- leave insert mode, press Escape.
- command line mode, type ':'

  - Ctrl-d for see list of command
  - :e filename ex. :e ~/.vimrc // for edit other file

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

remember last word you type and key stroke ex. `I, i, a, A, dd, cc`

**macro best practices**

-> Normalize the cursor position. `0`

-> Perform edits and operations.

-> Position your cursor to enable easy replays. `j`

```
// create macro
// q{register}
1. qa     // start recodeing macro in register a
2. do what ever you want  // ex INOTE:
3. type q // end recode macro
:reg a    // for see what is register a store

// use macro
// @{register}
@a  // use macro => out put is result in 2. = NOTE: ..
@@  // repeat macro

// repat macro multiple line
//{count}@{register}
5@a  // use macro for 5 line

// append register in case forget or want to add more command to old macro register
// q{capital register}
qA   // start append
j    // append j(new line to register a)
q    // end recode macro
```

use macro change "" to ' all line

```
//"foo", "bar", "baz" -> 'foo', 'bar', 'baz'
qb  // start recoding macro use register b
0:s/"/'/g enter  // create macro
q   // end recode macro

//use macro
move to line you want to change "" to '"
@b

// multiple line
20@b // use macro register b to 20 line

// multiple line current line to the end of the file (cannot use in vscode)
// . = current positon
// $ = end of file
:.,$ normal @b
```

## visual

- v characterwise
- V linewise
- Ctrl-v blockwise // ex. I Ctrl-v lll jjj

Just some of command you can use in visual mode include.

```
ex. vap // select all paragraph
~ - Switch case
a - all
c - Change
d - Delete
y - Yank(copy)
o - oposite cursor location // ex. Vjjo
O - oposite cursor conner use with Ctrl-v(blockwise)
r - Replace
I - Insert
A - Append
J - Join
u - Make lowercase
U - Make uppercase
> - Shift right
< - Shift left

// append word multiline
// want to append end to all line
line1: one
line2: one two
line3: one two three
1. move cursor to begining line1
2. Ctrl-v // blockwise select
3. $   //select to end of line
4. jj  //select line2, 3
5. A   // insert multiple line
6. esc //
```

**V linewise mix other command**

```
// want to center text
########################################
line 1 sometext:
line 2 sometext: sometext
########################################

1. Vj  // select line 1, line 2
2. :   // enter command mode
3. center 40 and press enter //not work in vscode
// can use left right also
// gv reselect the area
########################################
            line 1 sometext:
       line 2 sometext: sometext
########################################
```

## Vim settings, preferences, and customizations

- rc = run commands
- system-wide vimrc and personal vimrc
- Unix/Linux/Mac: ~/.vimrc
- Windows: $HOME/\_vimrc
- Each line is executed as a command.

  - set ruler = :set ruler

```
:source .vimrc //read file .vimrc again after add new command

//.vimrc map use <F1-12> to auto add content
// map KEY KEYSTROKES
map <F2> ifunction foo(){<CR><Space><Space>console.log("I'm function foo");<CR>}<ESC>

//.vimrc custom own key map <leader> key :command  **not recommand**
map <leader> w :w!<CR> // type dont save and type enter
```

## Vim Buffers and Windows

- working with multiple windows

```
:sp   // splite window
:vs   // splite vertical window

// swith window
Ctrl-w w // go to next window
Ctrl-w h // go to windw to the left
Ctrl-w j // go to window below the curren
Ctrl-w k // go to windwo above
Ctrl-w l // go to window to the right

// adjust window size
Ctrl-w +  //decrease the height of a window
Ctrl-w -  //increase the height of a window
Ctrl-w >  //increase the width of a window
Ctrl-w <  //decrease the width of a window
Ctrl-w _  //maximize the width of a window
Ctrl-w =  //make all the windonw same or equal size

:h ctrl-w enter //document ctrl-w can do
```

## Vim surround

- wrap surround word with html tag

```
"Hello world" -> <p>Hello world</p>
cs"<p>

'Hello world' -> <p>Hello world</p>
cs'<p>

Hello world
<p>Hello world</p>
VS<p> or yss<p>

Hello world wrap the entire line
<p>Hello world wrap the entire line</p>
yss<p>

Hello world
<b>Hello</b> world
1. move cursor on Hello
2. ysiw<b>
```

- delete surround

```
"Hello world" -> Hello world
ds"

{Hello world}
Hello world
ds{
```

- wrap surrond text with ],}

```
Hello world -> [Hello world]
1. use v for select
2. type S]

Hello world -> [Hello] world
1. move cursor on Hello
2. type ysiw]
Note use [ instand of ] for add some space link this [ Hello ]
```

- wrap the entire line

```
{Hello} world
[{Hello} world]
yss]

{Hello} world
( {Hello} world )
yssb
```

- replace surround

```
(Hello world)
{Hello world}
cs(}
```
