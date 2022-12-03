On the thirty third day, I learned the following things about Prometheus.

# Prometheus

- Prometheus is a free software application that is used for monitoring and alerting.

- The record(metrics) that is monitored is going to be stored in a time-series database and that record is built using a HTTP pull model.

- Prometheus will hit the target to collect the metrics, show the data or even alert if some threshold are met.

## Why Prometheus?

- It contributes to the DevOps system by monitoring cloud native applications, infrastructure and hundreds of microservices.

- It fits both machine centric monitoring as well as monitoring of highly dynamic service orientated architecture.

- It is designed for reliability. It will quickly diagnose the problems.

- Each prometheus server is standalone. It means that it is not dependent on network storage or other remote services.

- You don't need an extensive infrastructure to use it.

- The most important thing that differentiate prometheus from other time-series databases is that it is pull-based tool unlike nagios, amazon cloud watch, new relic etc.

- When you're working with many microservices and each service is pushing their metrics to the monitoring system, it creates a high load of traffic within your infrastructure. The infrastructure is overloaded with constant push requests.

- It pulls the targets in order to retrieve metrics for them. E.g: Node exporter or application exporter.

- Prometheus retrieves the metrics via HTTP call. Node exporter and application exporter will listen to particular pod and then a prometheus server will initiate a HTTP call to this particular exporter and fetch system or appliction metrics from the end.

## Continuous monitoring in prometheus

- Monitoring applications and application servers is an important part of DevOps culture and process.

- You continuously want to monitor applications and servers for application exception, server CPU, memory usage or storage spikes.

- Prometheus will also give the notification if the cpu or memory goes up or down so that you can perform appropriate actions.

- That's why prometheus is used in continuous monitoring.

## Prometheus architecture

- The core prometheus has a main component called prometheus server that does the actual monitoring service.

- Prometheus server is made of three parts.

    1. Retrieval - It pulls the metric data
    2. Storage - It stores the metric data
    3. HTTP Server - It accept the queries

- **Target:** The things that prometheus monitors are called targets. In short the prometheus server monitors the target.

- **Metric:** Each unit of target such as current cpu status, memory usage or any other specific unit that you want to monitor is called a metric.

- Prometheus server collects metric from the target over HTTP, stores them localy or remotely and then displays them back in the prometheus server.

- Prometheus server scrapes a target for a specific interval and after that, it will store it in a time-series database.

- You define the targets to be scraped and also define the time interval for scrapping metrics in the *prometheus.yml* configuration file.

- You get the metric details by querying from the prometheus time-series database where the prometheus stores metrics and it uses a query language PromQL in the prometheus server to query metrics about the target.

- In other words, you ask the prometheus server via PromQL to show us a status of a particular target at a one particular time.

- **Retrieval:** Prometheus has a data retrieval type that is responsible for getting or pulling the metrics from applications, services, servers and other target resources and storing and pushing them into the database.

- **Storage:** Prometheus has the time-series database that stores all the metrics data like the current cpu usage or the number of excptions in an application.

- **HTTP Server:** Prometheus accepts the queries for the stored data, web server or the server api that is used to display it on a dashboard either through prometheus dashboard or other data visualization tool called Grafana.

- Prometheus provides client libraries in a number of languages that you can use to provide health status of your application.

- Here is the link of the [client library](https://prometheus.io/docs/instrumenting/clientlibs/).

- Prometheus is not only about application monitoring. You can use exporter to monitor third-party systems also.

- Exporter is a piece of software that gets existing metrics from a third-party system and eventually export them to metric format that the prometheus server can eventually understands.

- Prometheus has a list of exporters for different services that you can find them [here](https://prometheus.io/docs/instrumenting/exporters/).

## Prometheus metrics and its types

- Each unit of a target such as the current cpu status, memory usage or any other specific unit that you want to monitor is called a metric.

- Server collects the metrics and stores them locally or remotely and displays them on the prometheus graphical user interface.

- Metrics has four different types

    **1. Counter Type:** A counter is a cumulative metric that represents a single value that can only increase or be reset to zero on restart. E.g. To represent the number of request served, tasks completed or errors. 
    
    Don't use a counter to expose a value that decreases or don't use a counter for the number of currently using processes.

    **2. Gauge Type:** A gauge is a metric that represents a single numerical value that can go up and down. It is used to measure temprature, current memory usage.

    **3. Histogram Type:** It takes many measurements of a value to later calculate averages or percentile. You know what the range of values will be up front, so you can define your own. E.g: How long something took or how big the size of the request was.

    **4. Summary Type:** It is similar to a histogram but you don't know what the range of the values will be up front, so you cannot use histogram.

Read in detail [here](https://prometheus.io/docs/concepts/metric_types/).

## **Explaining it in a video**

Here you can get an explanation in a video. [33/60 Day of DevOps Challenge](https://www.youtube.com/watch?v=s4f3xxZxGYI&list=PLptbpfKzsc3BtEki4tHQm5Xmpj8w1_JlM&index=31)