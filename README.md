# Getting started

To get all docker containers up and running, in __ci-monitor-demo__ use:

```
vagrant up
```
#### With docker machine

| *Tool* | *Link* | *Credentials* |
| ------------- | ------------- | ------------- |
| Jenkins | http://${docker-machine ip default}:8888/ | no login required |
| SonarQube | http://${docker-machine ip default}:9000/ | admin/admin |
| Nexus | http://${docker-machine ip default}:8181/ | admin/admin123 |
| Selenium Grid | http://${docker-machine ip default}:4444/grid/console | no login required |
| Kibana | http://${docker-machine ip default}:5601 | no login required |
| Grafana | http://${docker-machine ip default}:3000 | admin/admin |
