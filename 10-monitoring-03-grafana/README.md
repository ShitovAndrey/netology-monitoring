# Домашнее задание к занятию 14 «Средство визуализации Grafana»

## Обязательные задания

### Задание 1
**<em>Решение домашнего задания — скриншот веб-интерфейса grafana со списком подключенных Datasource.</em>**  

![](/10-monitoring-03-grafana/images/01-grafana-ds-prometheus.png)  

## Задание 2
Создайте Dashboard и в ней создайте Panels:

- утилизация CPU для nodeexporter (в процентах, 100-idle);
- CPULA 1/5/15;
- количество свободной оперативной памяти;
- количество места на файловой системе.

**<em>Для решения этого задания приведите promql-запросы для выдачи этих метрик, а также скриншот получившейся Dashboard.</em>**  

```
# утилизация CPU для nodeexporter (в процентах, 100-idle)
100 - (avg(irate(node_cpu_seconds_total{instance="nodeexporter:9100", job="nodeexporter", mode="idle"}[30m])) * 100)

# CPULA 1/5/15
node_load1{instance="nodeexporter:9100", job="nodeexporter"}
node_load5{instance="nodeexporter:9100", job="nodeexporter"}
node_load15{instance="nodeexporter:9100", job="nodeexporter"}

# количество свободной оперативной памяти
node_filesystem_free_bytes{device="/dev/mapper/ubuntu--vg-root", fstype="ext4", instance="nodeexporter:9100", job="nodeexporter", mountpoint="/"}

# количество места на файловой системе
node_memory_MemAvailable_bytes{instance="nodeexporter:9100", job="nodeexporter"}
```
![](/10-monitoring-03-grafana/images/02-first-dashboard.png)


## Задание 3

Создайте для каждой Dashboard подходящее правило alert — можно обратиться к первой лекции в блоке «Мониторинг».  
**<em>В качестве решения задания приведите скриншот вашей итоговой Dashboard.</em>**  

![](/10-monitoring-03-grafana/images/03-alerts.png)  

## Задание 4

**<em>Сохраните ваш Dashboard. Для этого перейдите в настройки Dashboard, выберите в боковом меню «JSON MODEL». Далее скопируйте отображаемое json-содержимое в отдельный файл и сохраните его.</em>**  

Ссылка на JSON Model дашборда: [first_dashboard.json](/10-monitoring-03-grafana/first_dashboard.json)

---