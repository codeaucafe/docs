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

The Dolt version is `1.50.4`.

<!-- START___DOLT___LATENCY_RESULTS_TABLE -->
|       Read Tests        | MySQL |  Dolt  | Multiple |
|-------------------------|-------|--------|----------|
| covering\_index\_scan   |  1.96 |   0.67 |     0.34 |
| groupby\_scan           | 13.46 |  17.63 |     1.31 |
| index\_join             |   1.5 |   2.43 |     1.62 |
| index\_join\_scan       |  1.44 |   1.42 |     0.99 |
| index\_scan             | 36.89 |  29.72 |     0.81 |
| oltp\_point\_select     |  0.18 |   0.26 |     1.44 |
| oltp\_read\_only        |  3.49 |   5.09 |     1.46 |
| select\_random\_points  |  0.34 |   0.59 |     1.74 |
| select\_random\_ranges  |  0.37 |   0.62 |     1.68 |
| table\_scan             | 36.89 |  30.81 |     0.84 |
| types\_table\_scan      | 80.03 | 112.67 |     1.41 |
| reads\_mean\_multiplier |       |        |     1.24 |

|       Write Tests        | MySQL | Dolt  | Multiple |
|--------------------------|-------|-------|----------|
| oltp\_delete\_insert     |   8.9 |  6.21 |      0.7 |
| oltp\_insert             |   4.1 |  3.07 |     0.75 |
| oltp\_read\_write        |  9.06 | 11.24 |     1.24 |
| oltp\_update\_index      |  4.18 |  3.13 |     0.75 |
| oltp\_update\_non\_index |  4.18 |  3.07 |     0.73 |
| oltp\_write\_only        |  5.77 |  6.21 |     1.08 |
| types\_delete\_insert    |  8.43 |  6.55 |     0.78 |
| writes\_mean\_multiplier |       |       |     0.86 |

|    TPC-C TPS Tests    | MySQL | Dolt  | Multiple |
|-----------------------|-------|-------|----------|
| tpcc-scale-factor-1   |  96.5 | 40.13 |      2.4 |
| tpcc\_tps\_multiplier |       |       |      2.4 |

| Overall Mean Multiple | 1.50 |
|-----------------------|------|
<!-- END___DOLT___LATENCY_RESULTS_TABLE -->
<br/>
