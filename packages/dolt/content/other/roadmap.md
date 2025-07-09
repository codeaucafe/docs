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

Our biggest announcement this quarter is the [Beta release of
Doltgres](https://www.dolthub.com/blog/2025-04-16-doltgres-goes-beta/), which means we think it's
ready to start building production applications. Try it and let us know what you think.

Roadmap last updated Jul 2025, next update Oct 2025.

## Upcoming features

Work to improve the performance and availability of Dolt is a constant theme and not called out
explicitly unless it's a major separable effort.

### Dolt

| Feature                                                                                  | Estimate    |
|------------------------------------------------------------------------------------------|-------------|
| Automatic garbage collection by default                                                  | Q3 2025     |
| Archival storage by default                                                              | 2025        |
| [User-defined functions](https://github.com/dolthub/dolt/issues/6193)                    | 2025        |
| More function coverage                                                                   | Ongoing     |
| Update multiple branches in a transaction                                                | Unscheduled |
| [Transaction isolation levels](https://github.com/dolthub/dolt/issues/2007)              | Unscheduled |
| Row-level locking (`SELECT FOR UPDATE`)                                                  | Unscheduled |
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
| pg_catalog query performance                                    | Q3 2025  |
| Stored procedures                                               | Q3 2025  |
| Extension suport                                                | Q3 2025  |
| Common table expressions (WITH)                                 | Q4 2025  |
| Window functions                                                | Q4 2025  |
| Full psql support                                               | Q3 2025  |
| Collation support                                               | 2025     |
| Custom indexing (anything not built in)                         | 2026     |
| Custom aggregate functions                                      | 2026     |
| More built-in function support                                  | Ongoing  |
| Additional DDL statements (e.g. `ALTER SEQUENCE`,  `COMMENT ON` | Ongoing  |
| Better pg_catalog support                                       | Ongoing  |

## Selection of recent feature launches

| Feature                                                                                                                            | Launch Date |
|------------------------------------------------------------------------------------------------------------------------------------|-------------|
| [Merge conflict preview](https://www.dolthub.com/blog/2025-06-25-preview-merge-conflicts/)                                         | Jun 2025    |
| [INSERT .. RETURNING](https://www.dolthub.com/blog/2025-06-12-insert-returning/)                                                   | Jun 2025    |
| [UPDATE ... FROM](https://www.dolthub.com/blog/2025-06-13-doltgres-update-from-support/)                                           | Jun 2025    |
| [MariaDB -> Dolt replication](https://www.dolthub.com/blog/2025-05-28-mariadb-to-dolt-replication/)                                | May 2025    |
| [Better stored procedure support](https://www.dolthub.com/blog/2025-05-07-stored-procedures-v2/)                                   | May 2025    |
| [SHOW statements in Doltgres](https://www.dolthub.com/blog/2025-05-13-show-statements-doltgres/)                                   | May 2025    |
| [Doltgres Triggers](https://www.dolthub.com/blog/2025-04-30-doltgres-supports-triggers/)                                           | Apr 2025    |
| [Doltgres Beta release](https://www.dolthub.com/blog/2025-04-16-doltgres-goes-beta/)                                               | Apr 2025    |
| [Virtual private cloud for Google Cloud in hosted deployments](https://www.dolthub.com/blog/2025-03-28-hosted-dolt-using-psc/)     | Mar 2025    |
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
