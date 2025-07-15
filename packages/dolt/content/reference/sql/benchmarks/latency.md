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

The Dolt version is `1.56.0`.

<!-- START___DOLT___LATENCY_RESULTS_TABLE -->
|       Read Tests        | MySQL |  Dolt  | Multiple |
|-------------------------|-------|--------|----------|
| covering\_index\_scan   |  1.89 |   0.68 |     0.36 |
| groupby\_scan           | 13.22 |  19.65 |     1.49 |
| index\_join             |  1.47 |   2.48 |     1.69 |
| index\_join\_scan       |  1.42 |   1.44 |     1.01 |
| index\_scan             | 34.33 |  31.37 |     0.91 |
| oltp\_point\_select     |   0.2 |   0.28 |      1.4 |
| oltp\_read\_only        |  3.68 |   5.37 |     1.46 |
| select\_random\_points  |  0.35 |   0.61 |     1.74 |
| select\_random\_ranges  |  0.38 |   0.63 |     1.66 |
| table\_scan             | 34.33 |  32.53 |     0.95 |
| types\_table\_scan      | 75.82 | 127.81 |     1.69 |
| reads\_mean\_multiplier |       |        |     1.31 |

|       Write Tests        | MySQL | Dolt  | Multiple |
|--------------------------|-------|-------|----------|
| oltp\_delete\_insert     |  8.28 |  6.55 |     0.79 |
| oltp\_insert             |   4.1 |  3.25 |     0.79 |
| oltp\_read\_write        |   8.9 | 11.87 |     1.33 |
| oltp\_update\_index      |  4.18 |   3.3 |     0.79 |
| oltp\_update\_non\_index |  4.18 |  3.25 |     0.78 |
| oltp\_write\_only        |  5.28 |  6.55 |     1.24 |
| types\_delete\_insert    |  8.43 |  6.91 |     0.82 |
| writes\_mean\_multiplier |       |       |     0.93 |

|    TPC-C TPS Tests    | MySQL | Dolt | Multiple |
|-----------------------|-------|------|----------|
| tpcc-scale-factor-1   | 94.93 | 39.1 |     2.43 |
| tpcc\_tps\_multiplier |       |      |     2.43 |

| Overall Mean Multiple | 1.56 |
|-----------------------|------|
<!-- END___DOLT___LATENCY_RESULTS_TABLE -->
<br/>
