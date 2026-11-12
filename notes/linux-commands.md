# Linux commands cheat sheet

## Navigation (навигация)
- pwd - show where I am (показать, где я)
- ls - show files in folder (показать файлы)
- ls -la - show all files, also hidden, with permissions (все файлы, скрытые, с правами)
- cd folder - go into folder (зайти в папку)
- cd .. - go one level up (на уровень выше)
- cd ~ - go home (домой)
- cd / - go to root (в корень)

## Paths (пути)
- . - this folder (эта папка)
- .. - parent folder (папка выше)
- ~ - my home folder (домашняя папка)
- / - root, start of full path (корень)

## Files (файлы)
- cat file - show file content (показать содержимое)
- cat ./file - file in this folder (файл в этой папке)
- "file name" or file\ name - name with spaces (имя с пробелами)
- - means stdin, keyboard input (минус = ввод с клавиатуры)

## Help (помощь)
- man command - manual, q to exit (справка, выход q)
- Tab - autocomplete names (автодополнение)
- Ctrl+C - stop command (остановить)

## New (день 6)
- ls -la - показать скрытые файлы (с точкой) и права
- file имя - показать тип файла (text или data)
- * - все файлы в папке (file ./inhere/*)
- lsof -i -P -n - сетевые соединения на моём Mac
