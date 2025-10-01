---
title: Latency
---

# Latency and Throughput

Our approach to SQL performance benchmarking is to use `sysbench`, an
industry standard benchmarking tool. We also benchmark Dolt using 
[TPC-C](https://www.tpc.org/tpcc/), an industry standard transactional 
throughput metric.

## Performance Roadmap

Dolt is slightly slower than MySQL on the `sysbench` test suite. 
The goal is to get Dolt to match MySQL latency for common operations. 
Dolt is currently 10% slower than MySQL, approximately 10% faster 
on writes and 33% slower on reads. The `multiple` column represents this 
relationship with regard to a particular benchmark.

Dolt gets about 40% of the transactional throughput on TPC-C than MySQL, 
40 transactions per second versus about 100 for MySQL. Most applications
are not sensitive to transactional throughput beyond a handful per second.

It's important recognize that these are industry standard tests, and
are OLTP oriented. Performance results may vary but Dolt is 
generally competitive on latency with MySQL and Postgres.

## Benchmark Data

Below are the results of running `sysbench` MySQL tests against Dolt
SQL Server for the most recent release of Dolt in the current default 
storage format. We will update this with every release. The tests 
attempt to run as many queries as possible in a fixed 2 minute time 
window. The `Dolt` and `MySQL` columns show the median latency in 
milliseconds (ms) of each query during that 2 minute time window.

The Dolt version is `1.59.14`.

<!-- START___DOLT___LATENCY_RESULTS_TABLE -->
|       Read Tests        | MySQL |  Dolt  | Multiple |
|:-----------------------:|:-----:|:------:|:--------:|
|  covering\_index\_scan  | 1.82  |  0.65  |   0.36   |
|      groupby\_scan      | 13.95 | 18.28  |   1.31   |
|       index\_join       | 1.52  |  2.43  |   1.6    |
|    index\_join\_scan    |  1.5  |  1.39  |   0.93   |
|       index\_scan       | 34.95 | 30.26  |   0.87   |
|   oltp\_point\_select   |  0.2  |  0.28  |   1.4    |
|    oltp\_read\_only     | 3.89  |  5.37  |   1.38   |
| select\_random\_points  | 0.36  |  0.58  |   1.61   |
| select\_random\_ranges  | 0.39  |  0.61  |   1.56   |
|       table\_scan       | 34.95 | 32.53  |   0.93   |
|   types\_table\_scan    | 75.82 | 130.13 |   1.72   |
| reads\_mean\_multiplier |       |        |   1.24   |

|       Write Tests        | MySQL | Dolt  | Multiple |
|:------------------------:|:-----:|:-----:|:--------:|
|   oltp\_delete\_insert   | 8.43  | 6.67  |   0.79   |
|       oltp\_insert       | 4.18  | 3.25  |   0.78   |
|    oltp\_read\_write     | 9.39  | 11.87 |   1.26   |
|   oltp\_update\_index    | 4.25  |  3.3  |   0.78   |
| oltp\_update\_non\_index | 4.25  | 3.25  |   0.76   |
|    oltp\_write\_only     | 5.28  | 6.55  |   1.24   |
|  types\_delete\_insert   | 8.58  | 6.91  |   0.81   |
| writes\_mean\_multiplier |       |       |   0.92   |

|    TPC-C TPS Tests    | MySQL | Dolt  | Multiple |
|:---------------------:|:-----:|:-----:|:--------:|
|  tpcc-scale-factor-1  | 93.46 | 39.97 |   2.34   |
| tpcc\_tps\_multiplier |       |       |   2.34   |

| Overall Mean Multiple | 1.50 |
|:---------------------:|:----:|
<!-- END___DOLT___LATENCY_RESULTS_TABLE -->
<br/>
