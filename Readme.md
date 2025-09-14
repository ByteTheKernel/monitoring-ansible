# Monitoring Ansible Project

## 📖 Описание

Этот проект автоматизирует развёртывание системы мониторинга на одном
сервере с помощью **Ansible**.\
В составе: 
- **Node Exporter** для сбора метрик
- **Prometheus** для хранения метрик
- **Grafana** для визуализации

Проект разворачивается на локальной VM (localhost) и настраивает: 
- Имя хоста и таймзону
- Системный NTP
- Пользовательские сервисы (prometheus,
grafana, node_exporter)
- Рабочие директории в `/srv/`

------------------------------------------------------------------------

## 📂 Структура проекта

    monitoring-ansible/
    ├── group_vars/
    │   └── all.yml               # Глобальные переменные (hostname, timezone, пароли и т.д.)
    ├── roles/
    │   ├── common/               # Базовые настройки (hostname, timezone, ntp, пакеты)
    │   ├── node_exporter/        # Установка и настройка node_exporter
    │   ├── prometheus/           # Установка и настройка Prometheus
    │   └── grafana/              # Установка и настройка Grafana
    ├── site.yml                  # Главный playbook
    ├── README.md                 # Документация проекта
    └── .gitignore                # Исключения для git

------------------------------------------------------------------------

## 🚀 Запуск

1.  Установить зависимости:

    ``` bash
    sudo apt update
    sudo apt install -y ansible git
    ```

2.  Перейти в каталог проекта:

    ``` bash
    cd monitoring-ansible
    ```

3.  Запустить playbook:

    ``` bash
    ansible-playbook site.yml
    ```

------------------------------------------------------------------------

## ✅ Проверка работы

- Node Exporter: `http://localhost:9100/metrics`
- Prometheus: `http://localhost:9090`
- Grafana: `http://localhost:3000` (логин/пароль по умолчанию `admin/admin`)

------------------------------------------------------------------------

## 🛠️ Примечания

-   Все сервисы работают от своих пользователей (`grafana_user`,
    `prometheus_user`, `node_exporter_user`).
-   Рабочие каталоги расположены в `/srv/`.
-   Grafana автоматически подключается к Prometheus и импортирует
    дашборд **Node Exporter Full (ID 1860)**.

------------------------------------------------------------------------

📌 Орешко Владислав
