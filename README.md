# Jmeter load test automation example (Jenkins)

### Описание:

    jmeter-load-test.jmx - jmeter скрипт, подготовленный в Jmeter Gui
    search.csv и edit.csv - тестовые данные, необходимые для теста
    pom.xml - включает jmeter-maven-plugin для запуска тестов локально 
    prometheus listener - настроена отправка метрик из jmeter в prometheus
    jmeter_dashboard.json - настроен дашборд для отображения ключевых метрик теста
    
### Для запуска сборки в Jenkins нужно:
- выбрать фристайл проект
- указать GitHub project
- Source Code Management - Git, указать репозиторий
- Build Steps - выбрать Invoke top-level Maven targets
- Goals - указать clean verify

### Инфраструктура мониторинга
- Prometheus Listener в Jmeter
- Prometheus - нужно добавить джобу в prometheus.yml
```chatinput
  - job_name: jmeter
    static_configs:
      - targets: ['localhost:9270']
```
- Grafana нужно импортировать jmeter_dashboard.json

### Система сборки:
``maven``

### Запуск сборки и теста:
``mvn clean verify``

### Запуск сборки и теста с переопределением параметров:
``mvn -Dthread.number=2 -Dtarget.rpm=4 -Dtest.duration=120 clean verify``
