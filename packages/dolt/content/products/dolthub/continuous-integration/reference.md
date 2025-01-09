---
title: Workflow Reference
---

Workflows are yaml files stored in a Dolt database that specify one or more CI Jobs and identify when those Job(s) should run.

```yaml
name: "workflow name"
on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
jobs:
  - name: "job name"
    steps:
      - name: "step name"
        saved_query_name: "saved query name"
        expected_rows: "== 2"
        expected_columns: "== 1"
```
