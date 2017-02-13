# Navigation
    C-v	Move forward one screenful
	M-v	Move backward one screenful
	C-l	Clear screen and redisplay all the text,
		 moving the text around the cursor
		 to the center of the screen.
		 (That's CONTROL-L, not CONTROL-1.)


	C-f	Move forward a character
	C-b	Move backward a character

	M-f	Move forward a word
	M-b	Move backward a word

	C-n	Move to next line
	C-p	Move to previous line

	C-a	Move to beginning of line
	C-e	Move to end of line

	M-a	Move back to beginning of sentence
	M-e	Move forward to end of sentence

For instance, C-u 8 C-f moves forward eight characters.

if emacs stops responding to your commands, you can stop it safely by
typing c-g.

	<DEL>        Delete the character just before the cursor
	C-d   	     Delete the next character after the cursor

	M-<DEL>      Kill the word immediately before the cursor
	M-d	     Kill the next word after the cursor

	C-k	     Kill from the cursor position to end of line
	M-k	     Kill to the end of the current sentence

	As you do this, Emacs highlights the text between the cursor and the
position where you typed C-<SPC>.  Finally, type C-w.  This kills all
the text between the two positions.

The command for yanking is C-y.  It reinserts the last killed text,
at the current cursor position.

	C-x C-f		Find file
	C-x C-s		Save file
	C-x s		Save some buffers
	C-x C-b		List buffers
	C-x b		Switch buffer
	C-x C-c		Quit Emacs
	C-x 1		Delete all but one window
	C-x u		Und

* Ido mode*
http://stackoverflow.com/questions/23741014/how-to-stop-auto-complete-from-overwriting-a-file-that-is-similarly-named
- Once you've typed the filename you want, hit C-j instead of RET. This makes ido-mode use the filename exactly as you typed it.
