# HOW TO USE VIM

### vim mode

- normal/command mode
- insert mode, type 'i'.
- leave insert mode, press Escape.
- command line mode, type ':'

### Delete

```
s   //delete and use 'insert mode'
S   //delete current line and use 'insert mode'

x   //delete(cut) current cursor
X   //delete(cut) front cursor (link press delete)

dh  //deltete front cursor
dj  //deltete current line and upper line
dk  //delete current line and lower line
dl  //delete current cursor

dd  //delete current line
d3w //delete 3 word
3dd //delete 3 line

D   //delete current cursor position to end of line
d$  //delete current cursor position to end of line
d0, d^  //delete current cursor positon to start of line
```
