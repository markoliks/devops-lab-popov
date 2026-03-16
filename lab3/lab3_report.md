University: ITMO University (https://itmo.ru/)
Faculty: FICT (https://fict.itmo.ru/)
Course: Введение в веб технологии (https://itmo.ru/)
Year: 2025/2026
Group: U4215
Author: Mark Popov
Lab: Lab3
Date of create: 17.03.2026
Date of finished: -

⸻

Лабораторная работа №3

Мониторинг с использованием Prometheus и Grafana

⸻

Цель работы

Изучить основы мониторинга контейнеризированных приложений с использованием Prometheus и Grafana, научиться собирать и визуализировать метрики.

⸻

Ход работы

1. Создание сети Docker

Создана сеть для взаимодействия контейнеров:

docker network create monitoring


⸻

2. Запуск Node Exporter

Контейнер для сбора метрик системы:

docker run -d --name node-exporter --restart unless-stopped -p 9100:9100 prom/node-exporter

Подключение к сети:

docker network connect monitoring node-exporter


⸻

3. Настройка Prometheus

Создан файл prometheus.yml:

global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']

  - job_name: 'node-exporter'
    static_configs:
      - targets: ['node-exporter:9100']


⸻

4. Запуск Prometheus

Запуск контейнера с конфигурацией:

MSYS_NO_PATHCONV=1 docker run -d \
  --name prometheus \
  --network monitoring \
  -p 9090:9090 \
  -v /c/Users/marko/devops-lab-popov/lab3/prometheus:/etc/prometheus \
  -v prometheus-data:/prometheus \
  prom/prometheus \
  --config.file=/etc/prometheus/prometheus.yml

Проверка:

http://localhost:9090/targets

Все сервисы находятся в состоянии UP.

⸻

5. Запуск Grafana

docker run -d \
  --name grafana \
  --network monitoring \
  -p 3000:3000 \
  -v grafana-data:/var/lib/grafana \
  -e "GF_SECURITY_ADMIN_PASSWORD=admin" \
  grafana/grafana


⸻

6. Подключение Prometheus в Grafana

Добавлен источник данных:
 • Тип: Prometheus
 • URL:

http://prometheus:9090

Подключение успешно (Save & Test).

<img width="1259" height="994" alt="image" src="https://github.com/user-attachments/assets/c8d893bd-c624-483b-a287-02be401643a4" />


7. Создание Dashboard

Создан dashboard и добавлена визуализация.

Используемый запрос:

node_cpu_seconds_total

Дополнительный (для наглядности):

rate(node_cpu_seconds_total[1m])

Построен график загрузки CPU.

<img width="708" height="746" alt="image" src="https://github.com/user-attachments/assets/f44790bb-1e10-4064-83f6-0ca2dd7d72a4" />
<img width="711" height="390" alt="image" src="https://github.com/user-attachments/assets/1cb4a39c-6acb-4b3e-a46c-262362e976a5" />


Результаты
 • Развернут стек мониторинга (Prometheus + Grafana)
 • Настроен сбор метрик через Node Exporter
 • Проверена работоспособность сервисов
 • Создан dashboard для визуализации

<img width="1225" height="961" alt="image" src="https://github.com/user-attachments/assets/dc6c6562-d447-4779-8315-81291433cb35" />


Вывод

В ходе лабораторной работы были освоены:
 • работа с Docker-контейнерами
 • настройка сетей Docker
 • конфигурация Prometheus
 • подключение источников данных в Grafana
 • построение графиков и мониторинга системы

Система мониторинга успешно развернута и функционирует корректно.
