---
title: "Metrics Quering"
date: 2022-05-09
---

### What is a vector and timeseries?
Timeseries is the mapping of timestamp to some data point. A related set of timeseries is called vector.

### What are Instant vector?
A set of timeseries where every timestamp map to single single value. Instant vectors can be charted, compared and arithemtic operations can be performed on them.

```
curl 'http://localhost:9090/api/v1/query' \
  --data 'query=http_requests_total{code="200"}' \
  --data time=1608481001

{
  "metric": {"__name__": "http_requests_total", "code": "200"},
  "value": [1608481001, "881"]
}
```

### What are Range vectors?
A set of timeseries where every timestamp with a duration is mapped to multiple data points. Range vector is always accompanied with a duration called range which is used to build the list of values for every timestamp. Range vectors cannot be charted not they can be compared nor arithmetic operations can be performed on them.

```
curl 'http://localhost:9090/api/v1/query' \
  --data 'query=http_requests_total{code="200"}[30s]' \
  --data time=1608481001

{
  "metric": {"__name__": "http_requests_total", "code": "200"},
  "values": [
    [1608480978, "863"],
    [1608480986, "874"],
    [1608480094, "881"]
  ]
}
```

### Offset Modifier
Offset modifier help us to chnage the base timestamp for evaluation. <br> eg: sum(http_requests_total{code="200"} offset 15m)

### @ modifier
@ modifier is also used to change the base timestamp for evaluation. The only difference is that instead of duration it uses unix timestamp. <br>  eg: sum(http_requests_total{code="200"} @ 1609746000)

### What is the difference between Instant vector and Range vector?
only difference between instant vector and range vector is that range vector is constructed from the instant vector by adding a lookbehind window in square brackets. For example, http_requests_total is an instant vector, while http_requests_total[30s] is a range vector.

### Why do we need Range vectors?
http_requests_total is a counter and gives the total number of request till that timestamp. But, we usually interested only in the increase of requests in certain duration. Lets say we want to find the increase in count in last 15 min. Then, we take the instant vector http_requests_total and append a range 15 m to it, which transform the instant vector to range vector. Then we apply an increase method that subtracts the count from last duration from start of the duration. The result is the instant vector which can be charted and further processed.

### Important concepts
1. Filtering based on labels <br> We can add labels in {} braces <br> eg: http_requests_total{job="prometheus",group="canary"} <br> We can use different matching operations for labels <br> a. = : exatcly matches the label value <br> b. != : Select labels that are not equal to the provided string <br> c. =~ : Select labels that regex-match the provided string. <br> d. !~: Select labels that do not regex-match the provided string
2. Getting all the labels of a metric <br> In Grafana type the metric name and all the lables with their values will be listed at the bottom.

### What is look behind window?


### What all metrics to record?

##### Credits :  
1. [Youtube: How to build a PromQL (Prometheus Query Language)](https://www.youtube.com/watch?v=hvACEDjHQZE)
2. [Prometheus Official Doc](https://prometheus.io/docs/prometheus/latest/querying/basics/)
3. [GrafanaCONline: Prometheus rate queries in Grafana](https://www.youtube.com/watch?v=09bR9kJczKM)
4. [Blog: Understanding Prometheus Range Vectors](https://satyanash.net/software/2021/01/04/understanding-prometheus-range-vectors.html)
5. [Stackoverflow: Prometheus instant vector vs range vector](https://stackoverflow.com/questions/68223824/prometheus-instant-vector-vs-range-vector)
6. [Grafana Docs: Prometheus data source](https://grafana.com/docs/grafana/latest/datasources/prometheus/#query-variable)
