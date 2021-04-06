---
category: Notes
url_path: '/notes'
title: 'Integration of ElasticStack'

layout: null
---

## Common Use Cases
+ Keep track of the number of errors in a web application
+ For Application performance management by keeping track of memory usage of the server 
+ Send events / user statistics  to Elasticsearch, e.g. website clicks, sales, new subscribers, logins, other user activities

### 1. Examples of integration

+ 1.1 ELK
![elastic_stack_elk](https://github.com/rayyiu002/ray_TechWorld/blob/gh-pages/image/elastic_stack_elk.png?raw=true)

+ 1.2 ELF with MQ
![elastic_stack_elk_with_mq](https://github.com/rayyiu002/ray_TechWorld/blob/gh-pages/image/elastic_stack_elk_mq.png?raw=true)

+ 1.3 EFK
![elastic_stack_efk](https://github.com/rayyiu002/ray_TechWorld/blob/gh-pages/image/elastic_stack_efk.png?raw=true)

+ 1.4 Comparison of Log Collectors - Fluentd vs Logstash
![comparison_logstash_fluentd](https://github.com/rayyiu002/ray_TechWorld/blob/gh-pages/image/comparison_logstash_fluentd.png?raw=true)

### 2. Example of deployment

+ 2.1 Basic deployment architecture (Signle node)
![elastic_stack_basic_deploy](https://github.com/rayyiu002/ray_TechWorld/blob/gh-pages/image/elastic_stack_basic_deploy.png?raw=true)

+ 2.2 Advanced deployment of ELK with HA
![elastic_stack_ha_deploy](https://github.com/rayyiu002/ray_TechWorld/blob/gh-pages/image/elastic_stack_ha_deploy.png?raw=true)

+ 2.3 Advanced deployment with HA and Redis
![elastic_stack_ha_deploy_with_redis](https://github.com/rayyiu002/ray_TechWorld/blob/gh-pages/image/elastic_stack_ha_deploy_with_redis.png?raw=true)

+ 2.4 Advanced deployment with HA and Kafka
![elastic_stack_ha_deploy_with_kafka](https://github.com/rayyiu002/ray_TechWorld/blob/gh-pages/image/elastic_stack_ha_deploy_with_kafka.png?raw=true)

<br/>

![elastic_stack_ha_deploy_with_kafka](https://github.com/rayyiu002/ray_TechWorld/blob/gh-pages/image/elastic_stack_ha_deploy_with_kafka_2.png?raw=true)

### Reference
+ [https://dzone.com/articles/introduction-to-elasticsearch-and-the-elk-stack](https://dzone.com/articles/introduction-to-elasticsearch-and-the-elk-stack)
+ [https://github.com/srinisbook/kubernetes-efk-stack](https://github.com/srinisbook/kubernetes-efk-stack)
+ [https://logz.io/blog/fluentd-logstash/](https://logz.io/blog/fluentd-logstash/)
+ [https://dzone.com/articles/logging-with-elastic-stack](https://dzone.com/articles/logging-with-elastic-stack)
+ [https://www.programmersought.com/article/87274254582/](https://www.programmersought.com/article/87274254582/)
+ [https://www.elastic.co/guide/en/logstash/current/deploying-and-scaling.html](https://www.elastic.co/guide/en/logstash/current/deploying-and-scaling.html)
