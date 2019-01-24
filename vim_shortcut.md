# In the insert mode

Keyword completion

	Ctrl+N

# Replace
ce replace a word.
gR insert (replacing) mode. *CAPITAL R

%-globalflag

Delete the last characters

		:s/.\{1}$//
		
 Reverse lines (see :help 12.4)
 
 		:g/^/m0
 		
With confirmation: %s/test/test/c

:%s/old/new/g make replacement with old to new in all lines (g means all words in a line)

special character like /: s/test/\/test/
for \, use \\; e.g. s/test/\\test/

Last, First -> First Last (Tricky)
$$%s/\([^,]*\), \(.*\)/\2 \1/$$

## Copy
y$ : copy a line.

..and write (selected lines into new file):

w filename

## Global Copy (Clipboard)
$"*y copy to the clipboard $
$"*p paste to from the clipboard$


# Movement
e move to the end of the word.
w move to the beginning of the next word.
b move to the beginning of the previous word.


Ctrl+b jump to the previous page.
Ctrl+f jump to next page.
Ctrl+p jump to last line.
Crtl+n jump to next line.

## Yes, spell check!
setlocal spell


## Split the vim

split filename : open a new file on the right half of the screen
Ctrl-w h/j/k/l : move to the next window.
Ctrl-w [number] + : increase the size of the windows by [number] lines.
Ctrl-w =: make all windows even.
Ctrl-w [number] _ : change the size of the windows to [number] lines.

only: close all other windows.
wall: save all files.
qall: quit all files.

Note: Ctrl-+ or Ctrl--: change the font size of everything in the terminal. (Commands from the terminal itself.)

## Buffers (Multiple files)
buffers or ls: check the buffer list
buffer #: change to another buffer # (file).
sbuffer #: open new window for buffer #.
bdelete #: delter buffer #

## Play dead
Ctrl-s; to recover Ctrl-Q

## Record
(no enter)... start with setting up
		
		qa
		
		i things_to_be_recorded 
			// <then Move to the end of the lines> 
		a things_to_be_recorded_at_the_end
		
		q				 
		
Recall it by 

		@a
		
## New Technique:
