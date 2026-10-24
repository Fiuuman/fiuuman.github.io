---
title: ghost0 - breachlab.org
published: true
---

# [](#intro) Ввод
Очень долгое время меня не было и хотелось бы снова вернутся в эту кашу со своими руками и головой. Не знаю что меня все время тянет к этому но вот я решился познать что-то новое и начать с базы а закончить уже чем-то большим. Чтож давайте начнем.
# [](#challenge-description) Описание челенджа
> The previous analyst left in a hurry.
>
> His terminal is still open. His files — still here.
>
>Find what he left behind.

# [](#approach) Мысли перед прохождением
Мысли только о том как мне оформить эти врайтапы, я думаю тут прямо не так сильно много будет кнтента и как бы будет не очень заполнять маленькими контентами сайт свой. Может мне стоит его улучшить и использовать более другую версию перенеся все свои старые записки? Ладно я буду думать и в будущем возможно сделаю это.

## [](#step1) Шаг 1: Понимание базовых концепций
Что там вообще нужно сделать? Нам пишут о том что прошлый аналитик оставил открытым терминал и какие-то файлы, нам же нужно прочитать эти файлы. Ну на самом деле, я уже немного опытный игрок linux/unix систем и как бы честно говоря я не знаю что тут писать и сразу очевидно напрашивается понимание как работает навигация в linux. Что нам нужно? Правильно, команда ```ls ```. Что это такое?
Команда ```ls``` — это электронный «фонарик» для осмотра папок в Linux.
По умолчанию эта команда скрывает файлы и папки название которых начинается с точки (```.```). Потому мы воспользуемся флагами встроенную в эту команду.

```-l``` - отображает подробную информацию: права доступа, владельца, размер и дату изменения. Это помогает быстро зацепиться за файлы, которые редактировались последними

```-a``` - позволяет увидеть абсолютно все скрытые объекты. Скрытые объекты это как раз таки те, которые начинаются с точки(```.```)

## [](#step2) Шаг 2: Понимание задачи
Ну объяснять как подключаться к серверу я не буду, просто введем сразу нашу команду:
```bash
ghost0@breachlab:~$ ls -la
total 84
drwx------ 1 ghost0 ghost0 4096 Oct 22 17:17 .
drwxr-xr-x 1 root   root   4096 Jun 22 13:41 ..
-rw-r--r-- 1 ghost0 ghost0  220 Jan  6  2022 .bash_logout
-rw-r--r-- 1 ghost0 ghost0 3771 Jan  6  2022 .bashrc
drwx------ 2 ghost0 ghost0 4096 Sep 15 14:05 .cache
drwxrwxr-x 4 ghost0 ghost0 4096 Jun 26 03:51 .local
-rw-r--r-- 1 ghost0 ghost0  807 Jan  6  2022 .profile
drwx------ 2 ghost0 ghost0 4096 Sep 14 16:25 .ssh
drwxrwxr-x 3 ghost0 ghost0 4096 Oct 22 17:55 .terminfo
drwxr-x--- 4 ghost0 ghost0 4096 Aug  9 13:31 .vscode-server
drwxrwxr-x 3 ghost0 ghost0 4096 Jul 27 07:23 .warp
-rw-r----- 1 ghost0 ghost0  312 Apr 17  2026 README
drwxrwxr-x 3 ghost0 ghost0 4096 Oct 17 09:56 shodan-env
drwxr-x--- 1 ghost0 ghost0 4096 Jul 16 03:51 workspace

```
Наша задача найти что-то непримечательное и среди того что нам выдало, мы видим папку ```workspace/```.
## [](#step3) Шаг 3: Атака
Переходим в нашу папку ```workspace/```.
```bash
ghost0@breachlab:~$ cd workspace/
ghost0@breachlab:~/workspace$ ls -la
total 32
drwxr-x--- 1 ghost0 ghost0 4096 Jul 16 03:51 .
drwx------ 1 ghost0 ghost0 4096 Oct 22 17:17 ..
drwxr-x--x 1 ghost0 ghost0 4096 Oct 20 10:52 archive
-rw-r----- 1 ghost0 ghost0  238 Jun 22 13:41 notes.txt
```
Видим папку ```archive/``` и файл ```notes.txt```. Для разнообразия давайте прочитаем файл с помощью команды ```cat```.
```bash
ghost0@breachlab:~/workspace$ cat notes.txt 
OPERATIONAL NOTES — KAEL
========================
Target: internal network segment 10.4.x.x
Method: passive recon, no active scanning
Status: ongoing

Credentials filed separately in archive/.
Do not store passwords in plaintext notes.
```
Ну как мы видим он напишет что наше решение находится в папке ```archive/```.
```bash
ghost0@breachlab:~/workspace$ cd archive/
ghost0@breachlab:~/workspace/archive$ ls -la 
total 24
drwxr-x--x 1 ghost0 ghost0 4096 Oct 20 10:52 .
drwxr-x--- 1 ghost0 ghost0 4096 Jul 16 03:51 ..
-rw-r----- 1 ghost0 ghost0   15 Jun 22 13:41 credentials
```

## [](#step4) Шаг 4: Решение
Видим файл, который нам нужен и снова читаем его с помощью команды ```cat```
```bash
ghost0@breachlab:~/workspace/archive$ cat credentials 
{flag}
```
Получаем наш флаг и пароль к следующей комнате. Поздравляю!