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

### Binary operators in Prometheus
Supported Arithmetic operators - ^ (exponent), *, /, %, +. -. ==, !=, <=, <, >=, >

#### Logical/set binary operators 
These operators are defined only between instant vectors. We have following binary operators
1. and (intersection) : <b> vector1 and vector2 </b> results in a vector with elements of vector1 that has matching elements with same labels in vector2. Other metric elements are dropped. Metric elements and names are carried from left-hand side metric
2. or (union) : <b> vector1 or vector2 </b> results in vector with all the original elements from vector1 with all the lables, from vector2 elements with labels are taken that are not present in vector1.
3. unless (complement) : <b> vector1 unless vector2 </b> results in a vector with all the elements of vector1 that has no elements in vector2 with same labels. All the matching elements in both the vectors are dropped.

#### Vector Matching
##### One-to-one vector matching
In this matching unique pair of elements are matched from left hand side and right hand side which has same set of labels and corresponding value.

##### Ignoring keyword
ignoring keyword allow us to discard labels in matching vectors. <br>
Eg: method_code:http_errors:rate5m{code="500"} / ignoring(code) method:http_requests:rate5m

##### on keyword
on keyword allow us to limit the number of labels matched in matching vectors. <br>
Eg: method_code:http_errors:rate5m{code="500"} / on(method) method:http_requests:rate5m

##### group_left keyword
group_left does Many-to-one matching. Meaning multiple elements from left vector matches single element in right vector. <br>

```
Syntax:
<vector expr> <bin-op> ignoring(<label list>) group_left(<label list>) <vector expr>
<vector expr> <bin-op> on(<label list>) group_left(<label list>) <vector expr>

Eg: method_code:http_errors:rate5m / ignoring(code) group_left method:http_requests:rate5m
```

##### group_right keyword
group_right does one-to-Many matching. Meaning multiple elements from right vector matches single element on the left vector <br>

```
Syntax:
<vector expr> <bin-op> ignoring(<label list>) group_right(<label list>) <vector expr>
<vector expr> <bin-op> on(<label list>) group_right(<label list>) <vector expr>
```

### Aggregations functions
Aggregation functions can be used only on instant vectors. They can be used for particular dimensions <br>
We can use following aggregation functions <br>
1. sum (calculate sum over dimensions)
2. min (select minimum over dimensions)
3. max (select maximum over dimensions)
4. avg (calculate the average over dimensions)
5. group (all values in the resulting vector are 1)
6. stddev (calculate population standard deviation over dimensions)
7. stdvar (calculate population standard variance over dimensions)
8. count (count number of elements in the vector)
9. count_values (count number of elements with the same value)
10. bottomk (smallest k elements by sample value)
11. topk (largest k elements by sample value)
12. quantile (calculate φ-quantile (0 ≤ φ ≤ 1) over dimensions)

**Note** parameter is only required for count_values, quantile, topk and bottomk. <br>

#### by and without clause
We can either aggregate over all the label dimensions or we can preserve the distinct dimensions using **by** and **without** keywords. Without removes the listed lables from the resulting vectors. By does the opposite, it drops the lables not listed in the list from the resulting vector.

```
<aggr-op> [without|by (<label list>)] ([parameter,] <vector expression>)
Or
<aggr-op>([parameter,] <vector expression>) [without|by (<label list>)]
```

### Functions
1. `abs(v instant-vector)`: returns the instance vector with all the values converted to absolute value.
2. `ceil(v instant-vector)`: returns the instance vector with all the values converted to nearest higher integer.
3. `floor(v instant-vector)`: returns the instance vector with all the values converted to nearest lower integer.
4. `absent(v instant-vector)`: Just like java isEmpty() this function tests the instant vector if it is empty. This function can be used in alerting to know if the time series is empty. <br>
Eg: `absent(nonexistent{job="myjob"})`
4. `absent_over_time(v range-vector)`: Same as above function, this function takes a range vector and check if it is empty for a period of time. <br>
Eg: `absent_over_time(nonexistent{job="myjob"}[1h])`
5. `changes(v range-vector)`: returns the number of times vector values has changed within the provided time range as an instant vector.
6. `clamp(v instant-vector, min scalar, max scalar)`: filters all the values that are within the min and max.
7. `clamp_max(v instant-vector, max scalar)`: filters all the values of vector to have upper limit of max.
8. `clamp_min(v instant-vector, min scalar)`: filters all the values of vector to have lower limit of min.
9. `day_of_month(v=vector(time()) instant-vector)`: Returns the day of the month for a given series in UTC (timestamp-timestamp series). Returned values are from 1 to 31.
10. `day_of_week(v=vector(time()) instant-vector)`: Same as above, Returned values are from 0 to 6, where 0 means Sunday etc.
11. `day_of_year(v=vector(time()) instant-vector)`: Same as above, Returned values are from 1 to 365 for non-leap years, and 1 to 366 in leap years.
12. `days_in_month(v=vector(time()) instant-vector)`: returns number of days in the month for each of the given times in UTC. Returned values are from 28 to 31.
13. `hour(v=vector(time()) instant-vector)`: returns the hour of the day for each of the given times in UTC. Returned values are from 0 to 23.
14. `delta(v range-vector)`: Calculates the difference between first and last value of each time series element in a range vector v, returning an instant vector of all the deltas with lables. Prometheus extrapolates the values to cover the full time range mentioned in the range vector selector, hence we can get decimal points even when the time series is of integer elements  
15. `deriv(v range-vector)`: Calculates the per second derivate of range vector v, using simple linear regression. It should only be used for guages.
16. `idelta(v range-vector)`: calculates the difference between the last two samples in the range vector v. This method should only be used with guages.
17. `exp(v instant-vector)`: Calculates exponential function for all the elements in the vector v.
18. `histogram_quantile(φ scalar, b instant-vector)`: calculates the φ-quantile (0 ≤ φ ≤ 1) from the buckets b of a histogram.
19. `holt_winters(v range-vector, sf scalar, tf scalar)`: This function smoothens the time series data by using the trends in the time series. Lower the smoothening factor (sf) more importance is given to real data points. Higher the trend factor (tf) the more trends in the data is considered. Both sf and tf must be between 0 and 1. **This function should only be used with guages**.
20. `rate(v range-vector)`: Calculates the average per second increase of time series in the range vector. This function extrapolates the values to account for server restarts, missed values and imperfect alignment of scrape cycles with the range's time period 
21. `increase(v range-vector)`: Calculates the increase in the time series in the range vector. It is same as range method multiplied by number of seconds in the specified window. `increase()` method should only be used with counters <br> Breaks in monotonicity is taken care of. Also, increase is extrapolated to cover the full time range as specified in the range vector selector. So it is possible to get decimal values even when increase is in integer.
22. `irate(v range-vector)`: calculates the per-second instant rate of increase of the time series in the range vector. This is used because it automatically adjust for breaks in monotonicity. It should only be used when graphing volatile, fast-moving counters.
23. `ln(v instant-vector)`: calculates natural logarithm for all elements in timeseries. 
24. `log2(v instant-vector)`: calculates the log2 of all elements in timeseries.


<details>
    <summary>How many responses larger than 4kb were served on 12th June 2022 between 14:00 UTC to 14:15 UTC?</summary>
    <p>To be added</p>
</details>
<details>
    <summary>What percentage of requests in last hour got a response of 100ms or less?</summary>
    <p>histogram_quantile(0.99, sum(rate(http_delay_in_ms[5m])) by (1e))</p>
</details>

<details>
  <summary> <h4> What is 99th Percentile response time? </h4> </summary>
  <p>It is the measure of the maximum latency for the fastest 99% requests. For eg: if the 99th percentile is 2 sec then it means application executed 99% of requests in less than 2 sec. </p>
</details>

<details>
  <summary> <h4> What is 50th Percentile response time? </h4> </summary>
  <p>It is the measure of the maximum latency for the fastest 50% requests. For eg: if the 50th percentile is 2 sec then it means application executed 50% of requests in less than 2 sec. </p>
</details>

<details>
  <summary> <h4> How 99 percentile or 50 percentile better than mean/average or median? </h4> </summary>
  <p> Mean and median are not a very good metric to show outliers. For eg: if at 9 AM for a short duration traffic goes up, then 99th & 50th percentile will be very high. But, mean and median will be pretty low </p>
</details>

### What is look behind window?


### What all metrics to record?


Questions
1. How can we configure metric alerts so that we can know when to add new server, DB instance or any other computing resource to our fleet?
2. What alerts in general to configure? Which failures?
3. 

##### Credits :  
1. [Youtube: How to build a PromQL (Prometheus Query Language)](https://www.youtube.com/watch?v=hvACEDjHQZE)
2. [Prometheus Official Doc](https://prometheus.io/docs/prometheus/latest/querying/basics/)
3. [Grafana: official Videos](https://www.youtube.com/watch?v=_nZSrY784sY)
4. [Youtuve: PromQL Tutorial - Prometheus and Thanos Observability](https://www.youtube.com/watch?v=t6jZUR-xYVM)
5. [GrafanaCONline: Prometheus rate queries in Grafana](https://www.youtube.com/watch?v=09bR9kJczKM)
6. [Blog: Understanding Prometheus Range Vectors](https://satyanash.net/software/2021/01/04/understanding-prometheus-range-vectors.html)
7. [Stackoverflow: Prometheus instant vector vs range vector](https://stackoverflow.com/questions/68223824/prometheus-instant-vector-vs-range-vector)
8. [Grafana Docs: Prometheus data source](https://grafana.com/docs/grafana/latest/datasources/prometheus/#query-variable)
9. [Youtube: Aggregation Operators](https://www.youtube.com/watch?v=aTH7OTH5-Mc)
10. [Youtube: Better Histograms for Prometheus - Björn Rabenstein, Grafana Labs](https://www.youtube.com/watch?v=HG7uzON-IDM)
11. [Goolge cloud Engineering Docs: Latency metrics](https://cloud.google.com/spanner/docs/latency)
12. [Why Percentiles Don’t Work the Way You Think](https://orangematter.solarwinds.com/2016/11/18/why-percentiles-dont-work-the-way-you-think/)
