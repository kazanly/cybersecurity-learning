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

## Git
- git add . -> git commit -m "text" -> git push
- (корзина -> заказ -> курьер)
- git pull - забрать изменения с GitHub перед работой
- git log --all --name-only --format="" | sort | uniq - все файлы за всю историю
- git log -p --all | grep "слово" - поиск по всей истории

## Search
- grep слово файл - найти строку в файле
- grep -rilE "a|b" . - искать слова во всех файлах, показать имена файлов
- find / -user X -size 33c 2>/dev/null - найти файлы по признакам
- mdls файл - метаданные файла (Mac)

## Danger
- rm -rf папка - удалить навсегда. Сначала ls с тем же путём!

## Files and archives
- cp откуда куда - скопировать файл
- mv старое новое - переименовать или переместить
- file имя - тип файла (определяет по первым байтам, не по имени)
- gzip -d имя.gz - распаковать gzip
- bzip2 -d имя.bz2 - распаковать bzip2
- tar -xf имя - достать файлы из архива tar (потом ls)
- xxd -r файл > новый - hexdump обратно в файл
- Цикл: file -> инструмент -> ls -> повторить

## Encoding
- base64 -d файл - раскодировать base64 (это не шифрование)
- tr 'a-z' 'A-Z' - заменить символы
- Опции: -d (одна буква, один минус), --decode (слово, два минуса)

## HTTP
- curl -I адрес - только заголовки ответа
- curl -v адрес - весь разговор: > запрос, < ответ
- curl -d "данные" адрес - отправить форму (POST)
- Коды: 2xx ок, 3xx иди дальше, 4xx моя ошибка, 5xx ошибка сервера

## Keys and TLS
- scp -P порт пользователь@сервер:файл . - скопировать файл с сервера сюда
- ssh -i ключ пользователь@сервер -p порт - войти по ключу
- chmod 600 файл - только владелец читает и пишет (r=4, w=2, x=1)
- openssl s_client -connect адрес:порт - TLS-клиент
- curl -sv -o /dev/null https://... - посмотреть сертификат
- Перед командой смотри на начало строки: Mac или сервер?

## Git route (маршрут каждый раз)
1. cd ~/cybersecurity-learning   - сходи в папку
2. git pull                      - забери свежее
3. nano journal/ДАТА.md          - открой и запиши
4. git add .                     - корзина
5. git commit -m "Глагол + что"  - заказ
6. git push                      - курьер

## Processes
- ps -o pid,ppid,comm - процессы этого окна: номер, родитель, имя
- ps -p НОМЕР -o pid,ppid,comm - конкретный процесс по номеру
- Идти вверх по PPID до 1 = найти, кто всё запустил
- ssh пользователь@сервер -p порт КОМАНДА - выполнить одну команду без входа
- s вместо x в ls -la = setuid (запуск с правами владельца)
- find / -perm -4000 2>/dev/null - найти все setuid-файлы

## Ports
- http 80 (бабушка, всё вслух), https 443 (замок), ssh 22 (ш-ш)
