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

The Dolt version is `1.50.1`.

<!-- START___DOLT___LATENCY_RESULTS_TABLE -->
|       Read Tests        | MySQL |  Dolt  | Multiple |
|-------------------------|-------|--------|----------|
| covering\_index\_scan   |  1.86 |   0.62 |     0.33 |
| groupby\_scan           | 13.22 |  17.63 |     1.33 |
| index\_join             |  1.47 |   2.57 |     1.75 |
| index\_join\_scan       |  1.44 |   1.42 |     0.99 |
| index\_scan             | 34.33 |  29.72 |     0.87 |
| oltp\_point\_select     |  0.18 |   0.26 |     1.44 |
| oltp\_read\_only        |  3.43 |   5.09 |     1.48 |
| select\_random\_points  |  0.33 |   0.58 |     1.76 |
| select\_random\_ranges  |  0.37 |    0.6 |     1.62 |
| table\_scan             | 34.95 |  30.81 |     0.88 |
| types\_table\_scan      | 75.82 | 108.68 |     1.43 |
| reads\_mean\_multiplier |       |        |     1.26 |

|       Write Tests        | MySQL | Dolt  | Multiple |
|--------------------------|-------|-------|----------|
| oltp\_delete\_insert     |   8.9 |  6.21 |      0.7 |
| oltp\_insert             |   4.1 |  3.07 |     0.75 |
| oltp\_read\_write        |   8.9 | 11.24 |     1.26 |
| oltp\_update\_index      |  4.18 |  3.13 |     0.75 |
| oltp\_update\_non\_index |  4.18 |  3.07 |     0.73 |
| oltp\_write\_only        |  5.67 |  6.21 |      1.1 |
| types\_delete\_insert    |  8.28 |  6.55 |     0.79 |
| writes\_mean\_multiplier |       |       |     0.87 |

|    TPC-C TPS Tests    | MySQL | Dolt  | Multiple |
|-----------------------|-------|-------|----------|
| tpcc-scale-factor-1   | 96.54 | 40.01 |     2.41 |
| tpcc\_tps\_multiplier |       |       |     2.41 |

| Overall Mean Multiple | 1.51 |
|-----------------------|------|
<!-- END___DOLT___LATENCY_RESULTS_TABLE -->
<br/>
