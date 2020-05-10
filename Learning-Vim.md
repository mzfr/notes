# Learning Vim

I have just started using Vim for writing small scripts while doing CTFs so this will have things that I am learning with time.

* duplicate a line: `:t.`
* Copy paste are simple:
    - `Shift+CTRL+C` - copy
    - `Shift+CTRL+V` - paste
* quit
    - `:qa!`

* visual mode:
    - `v` to get into visual mode - this is just for characters
    - `V` - this is for line mode
    - `Ctrl+v` - Visual block mode
    - Use arrow keys to select the text.
        - Shift+$ - to completely select the word.
    - Y - yank(copy)
    - d - delete
    - p - paste
    - u - undo

* :s/,/\r/g
    - Break on comma

* :set number
    - Show line number

## To Select and comment multiple lines

* Select the first caracter of your block

* press Ctrl+V ( this is rectangular visual selection mode)

* type `j` for each line more you want to be commented

* type `Shift-i` (like I for "insert at start")

* type // (or # or " or ...)

* You will see the modification appearing only on the first line

* IMPORTANT LAST STEP: type Esc key, and there you see the added character appear on all lines

