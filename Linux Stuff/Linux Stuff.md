## CMD

- xdg-open . (open file explorer) 
- xdg-open file (open file) 
- ctrl + a ⇒ move cursor to start 
- ctrl + e ⇒ move cursor to end
- ctrl + RIGHT/LEFT ⇒ move one word to left or right 
- ctrl + u ⇒ cut from end to begining 
- ctrl + k ⇒ cut form begining to end 
- ctrl + y ⇒ paste from clipboard 
- ctrl + w ⇒ cut one word 
- alt + U ⇒ upper case
- alt + L ⇒ Lower case
- alt + C ⇒ capitalize

## Find

- find -iname ⇒ case insensitive
- find -type d (directory) | f (file) 
- find -mmin -(time in min)(less than) | +(time in min)(more than) 
- find -mtime (days) find . -size +5M (returns all files of size more than 5Mb)
- find -perm 777 (find based on permissions)
- find . -type f -name "*.jpg" -maxdepth 1 
- find (folder or .) -exec {} + 
- find /path/to/parent -type f -exec grep 'XXX' /dev/null {} + (find 'XXX' in /path/to/parent)

## Grep

- grep -win "\<text/pattern\>" \<file name\> (match exact word (w) case insensitive (i) and line number (n))
- grep -A \<no of lines after match\> | -B \<no of lines before match\> | -C \<no of lines before and after match\>