---
title: Miscellaneous
---

# Miscellaneous

## Misc features

| Component                         | Supported | Notes and limitations                                                                                                 |
|:----------------------------------|:----------|:----------------------------------------------------------------------------------------------------------------------|
| Information schema                | ✅         |                                                                                                                       |
| Views                             | ✅         |                                                                                                                       |
| Window functions                  | 🟠         | Some functions not supported, see [window function docs](./expressions-functions-operators.md#window-functions)       |
| Common table expressions \(CTEs\) | ✅         |                                                                                                                       |
| Stored procedures                 | 🟠         | Only a few statements are not yet supported, see [compound statements](./supported-statements.md#compound-statements) |
| Cursors                           | ✅         |                                                                                                                       |
| Triggers                          | ✅         |                                                                                                                       |

## Client Compatibility

Some MySQL features are client features, not server features. Dolt ships with a client (ie. [`dolt sql`](../../cli/cli.md#dolt-sql)) and a server ([`dolt sql-server`](../../cli/cli.md#dolt-sql-server)). The Dolt client is not as sophisticated as the `mysql` client. To access these features you can use the `mysql` client that ships with MySQL.

| Feature                         | Supported | Notes and limitations                                                                                    |
|:--------------------------------|:----------|:---------------------------------------------------------------------------------------------------------|
| SOURCE                          | ❌        | Works with Dolt via the `mysql` client                                                                    |
| LOAD DATA LOCAL INFILE          | ❌        | LOAD DATA INFILE works with the Dolt client. The LOCAL option only works with Dolt via the `mysql` client |

## Join hints

Dolt supports the following join hints:

| name                     | supported | detail                                                                                          |
|--------------------------|-----------|-------------------------------------------------------------------------------------------------|
| JOIN_ORDER(<table1>,...) | ✅         | Join tree in scope should use the following join execution order. Must include all table names. |
| LOOKUP_JOIN(<t1>,<t2>)   | ✅         | Use LOOKUP strategy joining two tables.                                                         |
| MERGE_JOIN(<t1>,<t2>)    | ✅         | Use MERGE strategy joining two tables.                                                          |
| HASH_JOIN(<t1>,<t2>)     | ✅         | Use HASH strategy joining two tables.                                                           |
| INNER_JOIN(<t1>,<t2>)    | ✅         | Use INNER strategy joining two tables.                                                          |
| SEMI_JOIN(<t1>,<t2>)     | ✅         | Use SEMI strategy joining two tables (for `EXISTS` or `IN` queries).                            |
| ANTI_JOIN(<t1>,<t2>)     | ✅         | Use ANTI strategy joining two tables (for `NOT EXISTS` or `NOT IN` queries).                    |
| JOIN_FIXED_ORDER         | ❌         | Join tree uses in-place table order for execution.                                              |
| NO_ICP                   | ❌         | Disable indexed range scans on index using filters.                                             |

Join hints are indicated immediately after a `SELECT` token in a special
comment format `/*+ */`. Multiple hints should be separated by spaces:

```sql
SELECT /*+ JOIN_ORDER(arg1,arg2) */ 1
SELECT /*+ JOIN_ORDER(arg1,arg2) NO_ICP */ 1
```

Join hints currently require a full set of valid hints for all to be
applied. For example, if we have a three table join we can enforce
JOIN_ORDER on its own, join strategies on their own, or both order
and strategy:

```sql
SELECT /*+ JOIN_ORDER(xy,uv,ab) LOOKUP_JOIN(xy,uv) HASH_JOIN(uv,ab) */ 1
FROM xy
JOIN uv on x = u
JOIN ab on a = u;
```

Additional notes:
- If one hint is invalid given the execution options, no hints are applied and the engine falls back to default costing.
- Join operator hints are order-insensitive
- Join operator hints apply as long as the indicated tables are subsets of the join left/right.

## Table Statistics

### ANALYZE table

Dolt currently supports table statistics for index and join costing.

Statistics are collected by running `ANALYZE TABLE <table, ...>`.

Here is an example of how to initialize and observe statistics:

```sql
CREATE TABLE xy (x int primary key, y int);
INSERT INTO xy values (1,1), (2,2);
ANALYZE TABLE xy;
SELECT * from information_schema.tables;
+-------------+------------+-------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| SCHEMA_NAME | TABLE_NAME | COLUMN_NAME | HISTOGRAM                                                                                                                                                                                                                                                                                                                                                      |
+-------------+------------+-------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| tmp4        | xy         | x           | {"statistic": {"avg_size": 0, "buckets": [{"bound_count": 1, "distinct_count": 2, "mcv_counts": [1,1], "mcvs": [[1],[2]], "null_count": 0, "row_count": 2, "upper_bound": [2]}], "columns": ["x"], "created_at": "2023-11-14T11:33:32.250178-08:00", "distinct_count": 2, "null_count": 2, "qualifier": "tmp4.xy.PRIMARY", "row_count": 2, "types:": ["int"]}} |
+-------------+------------+-------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
```

Statistics are persisted in database's chunk store in a `refs/stats` ref stored separately from the commit graph. Each database has its own statistics store. The contents of the `refs/stats` reflect a single point-in-time for a single branch and are un-versioned. The contents of this ref in the current database can be inspected with the `dolt_statistics` system table. 

```sql
create table horses (id int primary key, name varchar(10), key(name));
insert into horses select x, 'Steve' from (with recursive inputs(x) as (select 1 union select x+1 from inputs where x < 1000) select * from inputs) dt;
analyze table horses;
select `index`, `position`, row_count, distinct_count, columns, upper_bound, upper_bound_cnt, mcv1 from dolt_statistics;
+---------+----------+-----------+----------------+----------+-------------+-----------------+-----------+
| index   | position | row_count | distinct_count | columns  | upper_bound | upper_bound_cnt | mcv1      |
+---------+----------+-----------+----------------+----------+-------------+-----------------+-----------+
| primary | 0        | 344       | 344            | ["id"]   | [344]       | 1               | [344]     |
| primary | 1        | 125       | 125            | ["id"]   | [469]       | 1               | [469]     |
| primary | 2        | 249       | 249            | ["id"]   | [718]       | 1               | [718]     |
| primary | 3        | 112       | 112            | ["id"]   | [830]       | 1               | [830]     |
| primary | 4        | 170       | 170            | ["id"]   | [1000]      | 1               | [1000]    |
| name    | 5        | 260       | 1              | ["name"] | ["Steve"]   | 260             | ["Steve"] |
| name    | 6        | 237       | 1              | ["name"] | ["Steve"]   | 237             | ["Steve"] |
| name    | 7        | 137       | 1              | ["name"] | ["Steve"]   | 137             | ["Steve"] |
| name    | 8        | 188       | 1              | ["name"] | ["Steve"]   | 188             | ["Steve"] |
| name    | 9        | 178       | 1              | ["name"] | ["Steve"]   | 178             | ["Steve"] |
+---------+----------+-----------+----------------+----------+-------------+-----------------+-----------+
```

### Auto-Refresh

Static statistics become stale quickly for tables that change frequently. Users can choose to manually manage run `ANALYZE` statements, or use some form of auto-refresh.

Auto-refresh statistic updates work the same way as partial `ANALYZE` updates. A table's "former" and "new" chunk set will 1) share common chunks preexisting in "former" 2) differ by deleted chunks only in the "former" table, and 3) differ by new chunks in the "new" table. This mirrors Dolt's inherent structural sharing. Rather than forcing an update on every refresh interval, we can toggle how many changes triggers the update.

When the auto-refresh threshold is 0%, the auto-refresh thread behaves like a cron job that runs `ANALYZE` periodically.

Setting a non-zero threshold defers updates until after a certain fraction of chunks are edited. For example, a 100% difference threshold updates stats when:

1) The table was previously empty and now contains data.

2) The table grew or shrank such that the tree height grew or shrank, and therefore the target fanout level changed.

3) Inserts added twice as many chunks.

4) Deletes removed 100% of the preexisting chunks.

5) 50% of the chunks were edited (an in-place edit deletes one chunk and adds one chunk, for a total of two changes relative to the original chunk)

Any combination of edits/inserts/deletes that exceeds the trigger threshold will also update stats.

We enable refresh with one mandatory and two optional system variables:

```sql
dolt sql -q "set @@PERSIST.dolt_stats_auto_refresh_enabled   = 1;"
dolt sql -q "set @@PERSIST.dolt_stats_auto_refresh_interval  = 120;"
dolt sql -q "set @@PERSIST.dolt_stats_auto_refresh_threshold = 0.5"
```

The first enables auto-refresh. It is a global variable that must be set during `dolt sql-server` startup and affects all databases in a server context. Databases added or dropped to a running server automatically opt-in to statistics refresh if enabled.

The second two variables configure 1) how often a timer wakes up to check stats freshness (seconds), and 2) the threshold updating a table's active statistics (new+deleted/previous chunks as a percentage between 0-1). For example, `dolt_stats_auto_refresh_interval = 600` means the server only attempt to update stats every 10 minutes, regardless of how much a table has changed. Setting `dolt_stats_auto_refresh_threshold = 0` forces stats to update in response to any table change.

A last variable blocks statistics from loading from disk on startup, or writing to disk on ANALYZE:

```sql
dolt sql -q "set @@PERSIST.dolt_stats_memory_only = 1"
```

### Stats Controller Functions

Dolt exposes a set of helper functions for managing statistics collection and use:

- `dolt_stats_drop()`: Deletes the stats ref on disk and wipes the database stats held in memory for the current database.

- `dolt_stats_stop()`: Cancels active auto-refresh threads for the current database.

- `dolt_stats_restart()`: Stops and restarts a refresh thread for the current database with the current session's interval and threshold variables.

- `dolt_stats_status()`: Returns the latest update to statistics for the current database.

### Performance

Lowering check intervals and update thresholds increases the refresh read and write load. Refreshing statistics uses shortcuts to avoid reading from disk when possible, but in most cases at least needs to read the target fanout level of the tree from disk to compare previous and current chunk sets. Exceeding the refresh threshold reads all data from disk associated with the new chunk ranges, which will be the most expensive impact of auto-refresh. Dolt uses ordinal offsets to avoid reading unnecessary data, but the tree growing or shrinking by a level forces a full tablescan.

For example, setting the check interval to 0 seconds (constant), the update threshold to 0 (any change triggers refresh) reduces the `oltp_read_write` sysbench benchmark's throughput by 15%. An increase in the update threshold for a 0-interval reduces throughput even more. On the other hand, basically any non-zero interval reduces the fraction of time spent performing stats updates to a negligible level:

| interval(s) | threshold(%) | latency  |
|------------|---------------|----------|
| 0          | 0             | -15%     |
| 0          | 1             | -46%     |
| 0          | 10            | -45%     |
| 1          | 0             | -.1%     |
| 1          | 1             | 0%       |

A small set of TPC-C run with one thread has a similar pattern compared to the baseline values, comparing queries per second (qps) now:

| interval(s) | threshold(%) | qps  |
|-------------|--------------|------|
| 0           | 0            | -15% |
| 0           | 1            | -26% |
| 0           | 10           | -10% |
| 1           | 0            | -4%  |
| 1           | 1            | 0%   |

Statistics' usefulness is rarely improved by immediate updates. Updating every minute or hour is probably fine for most workloads. If you do need quick statistics updates, performing them immediately instead of in batches appears to be preferable with the current implementation tradeoffs.

Statistics also have read performance implications, expensing more compute cycles to obtain better join cost estimates. Histograms with the maximum bucket fanout will be the most expensive to use. That said, at the time of writing this sysbench read benchmarks are not impacted by stats estimate overhead. Behavior for custom workloads will depend on read/write/freshness trade-offs.
