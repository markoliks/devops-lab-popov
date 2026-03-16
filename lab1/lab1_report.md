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
<img width="1898" height="1022" alt="image" src="https://github.com/user-attachments/assets/857b1e7f-41e7-442b-824e-9adb029cd68d" />


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

<img width="1875" height="1010" alt="image" src="https://github.com/user-attachments/assets/c08484e0-da64-4a9b-936d-ab3ebea186d5" />

## 5. Запуск веб-сервера nginx

Запуск контейнера:

docker run -d -p 8080:80 –name web-server nginx:alpine

После запуска сервер стал доступен по адресу:

http://localhost:8080

<img width="1891" height="1011" alt="image" src="https://github.com/user-attachments/assets/a16210f7-bc1a-4dfc-a4c3-46ba9dff0f96" />


## 6. Управление контейнерами

Просмотр контейнеров:

docker ps

Остановка контейнера:

docker stop web-server

Запуск контейнера:

docker start web-server

Удаление контейнера:

docker rm web-server

<img width="1899" height="1004" alt="image" src="https://github.com/user-attachments/assets/54e5099b-762c-4a09-98ee-3ce1a058c8c7" />

## 7. Работа с томами

Создание тома:

docker volume create my-volume

Создание файла в томе:

echo “Hello from volume” > /data/test.txt

Проверка сохранения данных в томе.
