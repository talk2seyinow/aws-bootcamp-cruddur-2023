# Week 2 — Distributed Tracing

## Pillars of Observability
Observability is about instrumenting systems to gather useful data that tells you when and why systems are behaving in a certain way. Whenever a system develops a fault, you should first examine telemetry data to better understand why the error occurred.

- Logs
- Metrics
- Tracing

### Logs
Logs are structured and unstructured lines of text a system produces when certain codes run. In general, you can think of a log as a record of an event that happened within an application. Logs help uncover unpredictable and emergent behaviors exhibited by components of microservices architecture.

### Metrics
Metrics are a numerical representation of data that can be used to determine a service or component’s overall behavior over time. Metrics are a measured value derived from system performance. With Metrics, you can easily correlate them across infrastructure components to get a holistic view of system health and performance. They also enable easier querying and longer retention of data. You can gather metrics on system uptime, response time, the number of requests per second, and how much processing power or memory an application is using, for example. Typically, SREs and ops engineers use metrics to trigger alerts whenever a system value goes above a specified threshold. 

## Observability vs Monitoring
Monitoring is tooling or a technical solution that allows teams to watch and understand the state of their systems. Monitoring is based on gathering predefined sets of metrics or logs.

### Observability is tooling or a technical solution that allows teams to actively debug their system. Observability is based on exploring properties and patterns not defined in advance.

### Obeservability services in AWS

- AWS Cloudwatch logs
- AWS Cloudwatch metrics
- AWS X Ray traces

![image](https://user-images.githubusercontent.com/70094537/224244991-26ce039c-c668-4946-af56-b368a600874a.png)


Instrumentation is what helps you to create or produce logs metrics traces.



Log into honeycomb.io,create a new enviroment, copy your API key and create the gitpod env var
```
export HONEYCOMB_API_KEY=""
export HONEYCOMB_SERVICE_NAME="Cruddur"
gp env HONEYCOMB_API_KEY=""
gp env HONEYCOMB_SERVICE_NAME="Cruddur"
```
