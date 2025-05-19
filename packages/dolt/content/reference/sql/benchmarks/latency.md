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

The Dolt version is `1.53.5`.

<!-- START___DOLT___LATENCY_RESULTS_TABLE -->
|       Read Tests        | MySQL |  Dolt  | Multiple |
|-------------------------|-------|--------|----------|
| covering\_index\_scan   |   2.0 |   0.65 |     0.32 |
| groupby\_scan           | 13.46 |  17.95 |     1.33 |
| index\_join             |  1.47 |   2.39 |     1.63 |
| index\_join\_scan       |  1.42 |    1.5 |     1.06 |
| index\_scan             | 34.33 |  30.26 |     0.88 |
| oltp\_point\_select     |  0.18 |   0.26 |     1.44 |
| oltp\_read\_only        |  3.43 |   5.28 |     1.54 |
| select\_random\_points  |  0.33 |   0.59 |     1.79 |
| select\_random\_ranges  |  0.37 |   0.61 |     1.65 |
| table\_scan             | 34.33 |  32.53 |     0.95 |
| types\_table\_scan      | 75.82 | 125.52 |     1.66 |
| reads\_mean\_multiplier |       |        |      1.3 |

|       Write Tests        | MySQL | Dolt  | Multiple |
|--------------------------|-------|-------|----------|
| oltp\_delete\_insert     |   8.9 |  6.32 |     0.71 |
| oltp\_insert             |   4.1 |  3.07 |     0.75 |
| oltp\_read\_write        |  8.74 | 11.45 |     1.31 |
| oltp\_update\_index      |  4.18 |  3.19 |     0.76 |
| oltp\_update\_non\_index |  4.18 |  3.07 |     0.73 |
| oltp\_write\_only        |  5.67 |  6.32 |     1.11 |
| types\_delete\_insert    |  8.28 |  6.67 |     0.81 |
| writes\_mean\_multiplier |       |       |     0.88 |

|    TPC-C TPS Tests    | MySQL | Dolt  | Multiple |
|-----------------------|-------|-------|----------|
| tpcc-scale-factor-1   | 97.61 | 39.19 |     2.49 |
| tpcc\_tps\_multiplier |       |       |     2.49 |

| Overall Mean Multiple | 1.56 |
|-----------------------|------|
<!-- END___DOLT___LATENCY_RESULTS_TABLE -->
<br/>
