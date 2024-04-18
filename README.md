# Grafana Dashboard для панели Marzban

![image](https://github.com/lifeindarkside/marzban-grafana-pannel/assets/66727826/454ccf25-9572-47cd-bd16-b088ad1a6904)

Этот дашборд создан для использования в панели Marzban.

**Важно**: Вся панель работает по времени UTC. Если у вас некорректно отображается время, попробуйте корректировать запросы:
Для MySQL:
```sql
DATESUB(NOW(), INTERVAL 3 HOUR)
```
Для SQLite:
```sql
datetime('now', '-3 hour')
```

## Установка Grafana

Следуйте [официальной инструкции по установке Grafana](https://grafana.com/docs/grafana/latest/setup-grafana/installation/), или воспользуйтесь docker-compose:

```yml
version: "3.8"
services:
  grafana:
    image: grafana/grafana:latest
    restart: unless-stopped
    environment:
      - TERM=linux
      - GFINSTALLPLUGINS=grafana-clock-panel,grafana-polystat-panel,frser-sqlite-datasource
    ports:
      - '3000:3000'
    volumes:
      - 'grafanastorage:/var/lib/grafana'
      - /var/lib/marzban:/var/lib/marzban
volumes:
  grafanastorage: {}
```

После запуска Grafana будет доступна на порту `3000`. Войдите, используя имя пользователя и пароль `admin`. Система предложит сменить пароль.

## Настройка источника данных

Подключите источник данных:

![image](https://github.com/lifeindarkside/marzban-grafana-pannel/assets/66727826/dfe74b0e-7ea5-40d4-b529-b6b2ef533f2f)

Нажмите `Add your first datasource`.

## Импорт дашборда

Добавьте дашборд, выбрав `import dashboard`.

![image](https://github.com/lifeindarkside/marzban-grafana-pannel/assets/66727826/d925d298-fbea-43bb-b101-d1ce9e5bba26)

Нажмите `import from JSON file` и приложите файл скачанный из репозитория

![image](https://github.com/lifeindarkside/marzban-grafana-pannel/assets/66727826/674a5b8a-ed12-462f-8809-3ca3756d8bc4)

Выберите ваш источник данных и нажмите `Import`.

![image](https://github.com/lifeindarkside/marzban-grafana-pannel/assets/66727826/b2da5145-5c62-4e37-828b-b51a0b6ee196)

Ваш дашборд готов:

![image](https://github.com/lifeindarkside/marzban-grafana-pannel/assets/66727826/493f797e-1b0b-4967-93a9-96e77b74b7ed)
