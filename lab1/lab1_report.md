University: [ITMO University](https://itmo.ru)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Введение в веб технологии](https://itmo-ict-faculty.github.io)  
Year: 2025/2026  
Group: K66666  
Author: По  
Lab: Lab1  
Date of create: 16.03.2026  
Date of finished: -
# Лабораторная работа №1
## Основы работы с Docker

### Цель работы
Изучить основы работы с Docker: запуск контейнеров, работу с образами и томами.

## 1. Проверка установки Docker

Команда:

docker –version


## 2. Запуск тестового контейнера

Команда:

docker run hello-world

Docker скачал образ hello-world и запустил тестовый контейнер.


## 3. Работа с образами

Просмотр образов:

docker images

Просмотр запущенных контейнеров:

docker ps

Просмотр всех контейнеров:

docker ps -a


## 4. Работа с контейнером Ubuntu

Запуск контейнера:

docker run -it ubuntu bash

Установка пакета curl:

apt update
apt install curl

Проверка:

curl –version


## 5. Запуск веб-сервера nginx

Запуск контейнера:

docker run -d -p 8080:80 –name web-server nginx:alpine

После запуска сервер стал доступен по адресу:

http://localhost:8080

---

## 6. Управление контейнерами

Просмотр контейнеров:

docker ps

Остановка контейнера:

docker stop web-server

Запуск контейнера:

docker start web-server

Удаление контейнера:

docker rm web-server


## 7. Работа с томами

Создание тома:

docker volume create my-volume

Создание файла в томе:

echo “Hello from volume” > /data/test.txt

Проверка сохранения данных в томе.
