---
title: "Metrics Quering"
date: 2022-05-09
---

### What is a vector and timeseries?
Timeseries is the mapping of timestamp to some data point. A related set of timeseries is called vector.

### What are Instant vector?
A set of timeseries where every timestamp map to singInstant vectors gives us a single value for single timestamp.

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
Range vectors gives us multiple values for a single timestamp.

##### Credits :  
1. [Youtube: How to build a PromQL (Prometheus Query Language)](https://www.youtube.com/watch?v=hvACEDjHQZE)
2. [Prometheus Official Doc](https://prometheus.io/docs/prometheus/latest/querying/basics/)
3. [GrafanaCONline: Prometheus rate queries in Grafana](https://www.youtube.com/watch?v=09bR9kJczKM)
4. [Blog: Understanding Prometheus Range Vectors](https://satyanash.net/software/2021/01/04/understanding-prometheus-range-vectors.html)
5. [Stackoverflow: Prometheus instant vector vs range vector](https://stackoverflow.com/questions/68223824/prometheus-instant-vector-vs-range-vector)
