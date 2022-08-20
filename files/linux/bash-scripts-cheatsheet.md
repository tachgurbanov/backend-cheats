# Шпаргалка по Bash скриптам

Скрипты Bash имеют расширение `.sh`:
```sh
touch script.sh
```

Хорошей практикой считается указывать путь до вашего терминала вначале каждого скрипта:
```sh
#! /bin/bash
```
> Этот прием называется **shebang**, подробнее можно почитать [тут](https://ru.wikipedia.org/wiki/%D0%A8%D0%B5%D0%B1%D0%B0%D0%BD%D0%B3_(Unix))

Список доступных терминалов в вашей системе можно посмотреть с помощью этой команды:
```sh
cat /etc/shells
```

## Hello world

```sh
#! /bin/bash
echo "Hello world"
```

Запуск скрипта:
```
bash script.sh
```

Скрипт можно сделать исполняемым файлом и запускать без команды `bash`:
```
chmod +x script.sh
```
```
./script.sh
```

## Комментарии

Однострочные комментарии:
```sh
# Это просто коммент
# И это тоже
echo "Hello from bash" # эта команда выводит строку в консоль
```

Мультистрочные комментарии:
```sh
: 'Мультистрочные комментарии очень удобны
для подробного описания ваших скриптов.
Успользуйте их с умом!'
```

## Переменные

```sh
MY_STRING="bash is cool"
echo $MY_STRING # Вывод значения переменной
```
> Имя переменной не должно начинаться с цифры

## Пользовательский ввод

Команда `read` читает пользовательский ввод и записывает его в указанную переменную:
```sh
echo "Введите ваше имя:"
read NAME
echo "Привет $NAME!"
```
> Если переменная не указана, то команда `read` по умолчанию сохранит все данные в переменную `REPLY`


Можно записывать несколько переменных. Для этого при вводе их нужно разделять пробелом:
```sh
read V1 V2 V3
echo "1 переменная: $V1"
echo "2 переменная: $V2"
echo "3 переменная: $V3"
```
```
> user:~$ bash script.sh
> hello world some other text
> 1 переменная: hello
> 2 переменная: world
> 3 переменная: some other text
```

Флаг `-a` позволяет создать массив в который будут записываться строки пользовательского ввода разделенные пробелом:
```sh
read -a NAMES
echo "Массив имён: ${NAMES[0]}, ${NAMES[1]}, ${NAMES[2]}"
```
```
> user:~$ bash script.sh
> Alex Mike John
> Массив имён: Alex, Mike, John
```

Флаг `-p` позволяет не переносить пользовательский ввод на следующую строку
Флаг `-s` позволяет скрыть вводимые символы (как это происходит при вводе пароля)
```sh
read -p "Введите ваш логин: " LOGIN
read -sp "Введите ваш пароль: " PASSWD
```
```
> user:~$ bash script.sh
> Введите ваш логин: bash_hacker
> Введите ваш пароль: 
```