:::writing{variant=“standard” id=“lab03”}

Лабораторная работа №3

Мониторинг с использованием Prometheus и Grafana

Цель работы

Изучить основы мониторинга контейнеризированных приложений с использованием Prometheus и Grafana, научиться собирать метрики и визуализировать их.

⸻

Ход работы

1. Создание сети Docker

Для взаимодействия контейнеров была создана сеть:

docker network create monitoring


⸻

2. Запуск Node Exporter

Node Exporter используется для сбора метрик системы:

docker run -d --name node-exporter --restart unless-stopped -p 9100:9100 prom/node-exporter

Контейнер был подключён к сети:

docker network connect monitoring node-exporter


⸻

3. Настройка Prometheus

Создан конфигурационный файл prometheus.yml:

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

Контейнер Prometheus был запущен с подключением конфигурации:

MSYS_NO_PATHCONV=1 docker run -d \
  --name prometheus \
  --network monitoring \
  -p 9090:9090 \
  -v /c/Users/marko/devops-lab-popov/lab3/prometheus:/etc/prometheus \
  -v prometheus-data:/prometheus \
  prom/prometheus \
  --config.file=/etc/prometheus/prometheus.yml

После запуска проверено состояние таргетов:

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

В Grafana добавлен источник данных:
 • Тип: Prometheus
 • URL:

http://prometheus:9090

Проверка соединения выполнена успешно (Save & Test).

⸻

7. Создание Dashboard

Создан новый Dashboard и добавлена визуализация.

Использован запрос:

node_cpu_seconds_total

Дополнительно использован улучшенный запрос:

rate(node_cpu_seconds_total[1m])

На графике отображаются метрики загрузки CPU.

⸻

Результаты

В ходе лабораторной работы:
 • Развернут стек мониторинга (Prometheus + Grafana)
 • Настроен сбор метрик с помощью Node Exporter
 • Проверена доступность сервисов
 • Построена визуализация метрик CPU
