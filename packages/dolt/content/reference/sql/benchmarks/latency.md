---
title: Latency
---

# Latency and Throughput

Our approach to SQL performance benchmarking is to use `sysbench`, an
industry standard benchmarking tool.

## Performance Roadmap

Dolt is slower than MySQL. The goal is to get Dolt to match 
MySQL latency for common operations. Dolt is currently 2X slower 
than MySQL, approximately 1.5X on writes and 2.5X on reads. The 
`multiple` column represents this relationship with regard to a 
particular benchmark.

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

The Dolt version is `1.45.6`.

<!-- START___DOLT___LATENCY_RESULTS_TABLE -->
|       Read Tests        | MySQL |  Dolt  | Multiple |
|-------------------------|-------|--------|----------|
| covering\_index\_scan   |  1.89 |   0.65 |     0.34 |
| groupby\_scan           | 13.22 |  17.32 |     1.31 |
| index\_join             |  1.44 |   2.43 |     1.69 |
| index\_join\_scan       |  1.42 |   1.44 |     1.01 |
| index\_scan             | 34.33 |  30.81 |      0.9 |
| oltp\_point\_select     |  0.18 |   0.26 |     1.44 |
| oltp\_read\_only        |  3.49 |   5.37 |     1.54 |
| select\_random\_points  |  0.37 |    0.6 |     1.62 |
| select\_random\_ranges  |   0.4 |   0.63 |     1.57 |
| table\_scan             | 34.33 |  33.12 |     0.96 |
| types\_table\_scan      | 74.46 | 114.72 |     1.54 |
| reads\_mean\_multiplier |       |        |     1.27 |

|       Write Tests        | MySQL | Dolt  | Multiple |
|--------------------------|-------|-------|----------|
| oltp\_delete\_insert     |   8.9 |  6.21 |      0.7 |
| oltp\_insert             |   4.1 |  3.07 |     0.75 |
| oltp\_read\_write        |  9.06 | 11.45 |     1.26 |
| oltp\_update\_index      |  4.18 |  3.13 |     0.75 |
| oltp\_update\_non\_index |  4.18 |  3.07 |     0.73 |
| oltp\_write\_only        |  5.67 |  6.32 |     1.11 |
| types\_delete\_insert    |  8.43 |  6.55 |     0.78 |
| writes\_mean\_multiplier |       |       |     0.87 |

|    TPC-C TPS Tests    | MySQL | Dolt  | Multiple |
|-----------------------|-------|-------|----------|
| tpcc-scale-factor-1   | 95.72 | 39.79 |     2.41 |
| tpcc\_tps\_multiplier |       |       |     2.41 |

| Overall Mean Multiple | 1.52 |
|-----------------------|------|
<!-- END___DOLT___LATENCY_RESULTS_TABLE -->
<br/>