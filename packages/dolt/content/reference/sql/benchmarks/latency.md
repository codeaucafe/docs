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

The Dolt version is `1.52.0`.

<!-- START___DOLT___LATENCY_RESULTS_TABLE -->
|       Read Tests        | MySQL |  Dolt  | Multiple |
|-------------------------|-------|--------|----------|
| covering\_index\_scan   |  1.86 |   0.67 |     0.36 |
| groupby\_scan           | 13.22 |  17.63 |     1.33 |
| index\_join             |  1.47 |   2.39 |     1.63 |
| index\_join\_scan       |  1.42 |   1.47 |     1.04 |
| index\_scan             | 34.33 |  30.26 |     0.88 |
| oltp\_point\_select     |  0.17 |   0.26 |     1.53 |
| oltp\_read\_only        |  3.36 |   5.18 |     1.54 |
| select\_random\_points  |  0.33 |    0.6 |     1.82 |
| select\_random\_ranges  |  0.36 |   0.62 |     1.72 |
| table\_scan             | 34.33 |  32.53 |     0.95 |
| types\_table\_scan      | 75.82 | 125.52 |     1.66 |
| reads\_mean\_multiplier |       |        |     1.31 |

|       Write Tests        | MySQL | Dolt  | Multiple |
|--------------------------|-------|-------|----------|
| oltp\_delete\_insert     |   8.9 |  6.32 |     0.71 |
| oltp\_insert             |  4.03 |  3.07 |     0.76 |
| oltp\_read\_write        |  8.74 | 11.45 |     1.31 |
| oltp\_update\_index      |   4.1 |  3.19 |     0.78 |
| oltp\_update\_non\_index |   4.1 |  3.07 |     0.75 |
| oltp\_write\_only        |  5.67 |  6.32 |     1.11 |
| types\_delete\_insert    |  8.28 |  6.67 |     0.81 |
| writes\_mean\_multiplier |       |       |     0.89 |

|    TPC-C TPS Tests    | MySQL | Dolt  | Multiple |
|-----------------------|-------|-------|----------|
| tpcc-scale-factor-1   | 97.45 | 39.27 |     2.48 |
| tpcc\_tps\_multiplier |       |       |     2.48 |

| Overall Mean Multiple | 1.56 |
|-----------------------|------|
<!-- END___DOLT___LATENCY_RESULTS_TABLE -->
<br/>
