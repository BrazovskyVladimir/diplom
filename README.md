# Diplom
Реализовано развертывание на базе хоста Ubuntu инфраструктуры для запуска простого проекта веб-калькулятора написанного на Python.
Для этого используется Ansible с несколькими ролями. 
Команда для запуска:  

```ansible
ansible-playbook - i inventory.ini start.yml -u acd --ask-become-pass
```

Первоначально на хосте устанавливается и запускается Kubernetes с контейнерами CRI-O.
Дополнительно на хост устанавливается Helm и реверс прокси на базе Nginx.

С помощью заранее отредактированных файлов helm chart-ов происходит установка и конфигурирование Zabbix, Prometheus, Grafana, Jenkins.
На хост Ubuntu устанавливается агент Zabbix и настраивается связь с сервером.
Prometheus настроен для получения метрик из базы etcd с подключением по https и получения метрик от exporter встроенного в рабочее приложение.
Grafana настроена на получение данных из Prometheus и Zabbix.
Jenkins предварительно настроен на запуск тестов, билдов и деплоя на текущий Kubernetes. Имеется 3 pipelines для тестов приложения, создания и 
загрузки image на докерхаб и разворачивания приложения в Kubernetes. 

Репозиторий приложения https://github.com/BrazovskyVladimir/Web-calculator.git имеет две ветки: test и master.

Jenkins: http://jenkins-diplom.local
Grafana: http://grafana-diplom.local
Приложение: http://calc-diplom.local
