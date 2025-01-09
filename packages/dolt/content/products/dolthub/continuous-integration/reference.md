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

# name

_String_. The case-insensitive name of the workflow, must be unique. Required.

# on

`on` identifies the events that should trigger the workflow to run.

# on.push

Runs workflow whenever a `push` event occurs. A `push` event refers to a branch head update on the remote database, usually following the [dolt push](../../../reference/cli/cli.md#dolt-push) command.

# on.pull_request

Runs workflow whenever a `pull_request` event occurs. A `pull_request` event refers to any "activity" or action involving a pull request on the remote database. Activities on pull request might include, but are not limited to, opening a pull request, closing a pull request, or synchronizing a pull request.

# on.<push|pull_request>.branches

_List_ _of_ _Strings_. Specifies the branch or branches affected which should cause the workflow to run. Required.

For example, if the `main` branch is listed under `on.push.branches`, then a push to `main` will trigger the workflow to run.

In the case of `on.pull_request.branches`, branches listed refer to the base branch of the pull request. If `main` is specified as a branch in this case, if a pull request is opened with `main` as its base branch, the workflow will run.

# on.pull_request.activities

_List_ _of_ _Strings_. Specifies the pull request activity types that should trigger the workflow. Optional.

Supported types as of Dolt v1.45.3 are:
- opened
- closed
- reopened

# jobs
# jobs.name
# jobs.steps
# jobs.steps.name
# jobs.steps.saved_query_name
# jobs.steps.expected_rows
# jobs.steps.expected_columns
