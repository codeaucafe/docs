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

The Dolt version is `1.44.4`.

<!-- START___DOLT___LATENCY_RESULTS_TABLE -->
|       Read Tests        | MySQL |  Dolt  | Multiple |
|-------------------------|-------|--------|----------|
| covering\_index\_scan   |  1.93 |   0.62 |     0.32 |
| groupby\_scan           |  13.7 |  16.41 |      1.2 |
| index\_join             |  1.44 |    2.3 |      1.6 |
| index\_join\_scan       |  1.42 |   1.47 |     1.04 |
| index\_scan             | 34.33 |  46.63 |     1.36 |
| oltp\_point\_select     |  0.18 |   0.27 |      1.5 |
| oltp\_read\_only        |  3.49 |   5.37 |     1.54 |
| select\_random\_points  |  0.34 |   0.59 |     1.74 |
| select\_random\_ranges  |  0.37 |   0.62 |     1.68 |
| table\_scan             | 34.33 |  46.63 |     1.36 |
| types\_table\_scan      | 75.82 | 123.28 |     1.63 |
| reads\_mean\_multiplier |       |        |     1.36 |

|       Write Tests        | MySQL | Dolt  | Multiple |
|--------------------------|-------|-------|----------|
| oltp\_delete\_insert     |  8.74 |  6.21 |     0.71 |
| oltp\_insert             |  4.03 |  3.07 |     0.76 |
| oltp\_read\_write        |   8.9 | 11.45 |     1.29 |
| oltp\_update\_index      |   4.1 |  3.13 |     0.76 |
| oltp\_update\_non\_index |  4.18 |  3.07 |     0.73 |
| oltp\_write\_only        |  5.57 |  6.21 |     1.11 |
| types\_delete\_insert    |  8.28 |  6.55 |     0.79 |
| writes\_mean\_multiplier |       |       |     0.88 |

|    TPC-C TPS Tests    | MySQL | Dolt  | Multiple |
|-----------------------|-------|-------|----------|
| tpcc-scale-factor-1   | 97.12 | 41.19 |     2.36 |
| tpcc\_tps\_multiplier |       |       |     2.36 |

| Overall Mean Multiple | 1.53 |
|-----------------------|------|
<!-- END___DOLT___LATENCY_RESULTS_TABLE -->
<br/>