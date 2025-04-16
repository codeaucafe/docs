---
title: Roadmap
---

# Roadmap

Full details on [supported SQL
features](../reference/sql/sql-support/README.md) are
available on the docs site.

This is a selection of unimplemented features we're working on. Don't
see what you need on here? [Let us
know!](https://github.com/dolthub/dolt/issues) Paying customers get
their feature requests implemented first.

Our next major goal is getting the Postgres version of Dolt, [Doltgres](https://www.doltgres.com/),
to a [production quality Beta
release](https://www.dolthub.com/blog/2024-08-06-doltgres-beta/). Doltgres Beta will ship in Q1
2025, with hosted deployment available.

Roadmap last updated Apr 2025, next update Jun 2025.

## Upcoming features

Work to improve the performance and availability of Dolt is a constant theme and not called out
explicitly unless it's a major separable effort.

### Dolt

| Feature                                                                                  | Estimate    |
|------------------------------------------------------------------------------------------|-------------|
| Virtual private cloud for Google Cloud in hosted deployments                             | Q2 2025     |
| Archival storage by default                                                              | Q2 2025     |
| Better stored procedure support                                                          | 2025        |
| [User-defined functions](https://github.com/dolthub/dolt/issues/6193)                    | 2025        |
| Update multiple branches in a transaction                                                | 2025        |
| Row-level locking (`SELECT FOR UPDATE`)                                                  | 2025        |
| [Transaction isolation levels](https://github.com/dolthub/dolt/issues/2007)              | 2025        |
| More function coverage                                                                   | Ongoing     |
| [Rebase schema conflict resolution support](https://github.com/dolthub/dolt/issues/7820) | Unscheduled |
| [Multiple DBs in one repo](https://github.com/dolthub/dolt/issues/3043)                  | Unscheduled |
| [Customized merge rules](https://github.com/dolthub/dolt/issues/7680)                    | Unscheduled |
| Images / video types                                                                     | Unscheduled |
| [History compression](https://github.com/dolthub/dolt/issues/5355)                       | Unscheduled |
| [Embedded Dolt](https://github.com/dolthub/dolt/issues/8953)                             | Unscheduled |
| Lock / unlock tables                                                                     | Unscheduled |
| Updateable views                                                                         | Unscheduled |
| Encryption at rest                                                                       | Unscheduled |
| Pipeline query processing                                                                | Unscheduled |
| Other database frontends (e.g. Mongo, SQL Server)                                        | Unscheduled |

### Doltgres

Dolt and Doltgres share an engine, so most features on the Dolt roadmap also apply to Doltgres.

| Feature                                                         | Estimate |
|-----------------------------------------------------------------|----------|
| Triggers                                                        | May 2025 |
| Stored procedures                                               | Q2 2025  |
| Collation support                                               | Q3 2025  |
| Support for most common extensions, e.g. geospatial types       | Q3 2025  |
| Common table expressions (WITH)                                 | Q3 2025  |
| Updates on two or more tables in the same statement             | Q3 2025  |
| Window functions                                                | Q3 2025  |
| Full psql support                                               | Q3 2025  |
| Extension suport                                                | Q4 2025  |
| Custom operators                                                | Q4 2025  |
| Custom indexing (anything not built in)                         | 2026     |
| Custom aggregate functions                                      | 2026     |
| More built-in function support                                  | Ongoing  |
| Additional DDL statements (e.g. `ALTER SEQUENCE`,  `COMMENT ON` | Ongoing  |

## Selection of recent feature launches

| Feature                                                                                                                            | Launch Date |
|------------------------------------------------------------------------------------------------------------------------------------|-------------|
| [Doltgres TOAST types](https://www.dolthub.com/blog/2025-04-14-adaptive-encoding/)                                                 | Apr 2025    |
| [Doltges Beta release](https://www.dolthub.com/blog/2025-04-16-doltgres-goes-beta/)                                                | Apr 2025    |
| [Automatic garbage collection](https://www.dolthub.com/blog/2025-02-28-announcing-automatic-gc-in-sql-server/)                     | Mar 2025    |
| Doltgres user defined functions                                                                                                    | Feb 2024    |
| [dolt_help table](https://www.dolthub.com/blog/2025-02-12-dolt-help-table/)                                                        | Feb 2025    |
| [Hosted Doltgres](https://www.dolthub.com/blog/2025-02-07-hosted-doltgres/)                                                        | Feb 2025    |
| Doltgres user defined types                                                                                                        | Jan 2025    |
| Doltgres users and auth                                                                                                            | Jan 2025    |
| [Vector indexes](https://www.dolthub.com/blog/2025-01-16-announcing-vector-indexes/)                                               | Jan 2025    |
| [Remote support in Dolt Workbench](https://www.dolthub.com/blog/2025-01-07-fetching-and-syncing-remotes-using-the-dolt-workbench/) | Jan 2025    |
| [dolt fsck](https://www.dolthub.com/blog/2024-10-09-fsck-announce/)                                                                | Oct 2024    |
| [Doltgres support for workbench](https://www.dolthub.com/blog/2024-10-17-dolt-workbench-supports-doltgres/)                        | Oct 2024    |
| [Data conflict resolution for dolt rebase](https://www.dolthub.com/blog/2024-09-05-rebase-conflict-resolution/)                    | Sep 2024    |
| [Doltgres: COPY support](https://www.dolthub.com/blog/2024-09-17-tabular-data-imports/)                                            | Sep 2024    |
| Doltgres: 90% correctness                                                                                                          | Sep 2024    |
| [Signed commits](https://www.dolthub.com/blog/2024-09-16-signed-commits/)                                                          | Sep 2024    |
| [Improved JSON performance](https://www.dolthub.com/blog/2024-07-15-json-prolly-trees/)                                            | Jul 2024    |
| [Postgres function support](https://www.dolthub.com/blog/2024-07-30-re-introducing-dolt-functions/)                                | Jul 2024    |
| [Dolt to MySQL binlog replication](https://www.dolthub.com/blog/2024-07-05-binlog-source-preview/)                                 | Jul 2024    |
| [pg_catalog support](https://www.dolthub.com/blog/2024-07-02-pg-catalog-update/)                                                   | Jul 2024    |
| [Doltgres schema support](https://www.dolthub.com/blog/2024-05-07-understanding-postgres-schemas/)                                 | May 2024    |
| [Storage archives](https://www.dolthub.com/blog/2024-04-29-dolt-storage-v2/)                                                       | Apr 2024    |
| [Zstd dictionary compression](https://www.dolthub.com/blog/2024-04-22-dolt-storage-dictionaries/)                                  | Apr 2024    |
| [Postgres to Doltgres replication](https://www.dolthub.com/blog/2024-04-23-announcing-postgres-to-doltgres-replication/)           | Apr 2024    |
| [Doltgres prepared statements](https://www.dolthub.com/blog/2024-04-01-prepared-statements-postgres/)                              | Apr 2024    |
| [Automatic table statistics](https://www.dolthub.com/blog/2024-02-16-stats-refresh/)                                               | Mar 2024    |
