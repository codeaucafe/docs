---
title: Installer configuration file reference
---

# Installer configuration file reference

```yaml
# installer_config.yaml

version: "v2.3.0"
host: "127.0.0.1"
docker_network: "doltlab"
metrics_disabled: false
whitelist_all_users: true
  use_env: false
  runtime: docker
services:
  doltlabenvoy:
    replicas: 1
    placement:
      constraints: ["node.labels.doltlabenvoy == true"]
      preferences:
        - spread: "nodes.labels.doltlabenvoy"
  doltlabdb:
    host: "127.0.0.1"
    port: 3306
    admin_password: "*****"
    dolthubapi_password: "*****"
    tls_skip_verify: true
    auto_gc_enabled: true
    server_config: "/local/path/to/server/config.yaml"
    volume_paths:
      data_volume_path: "/local/path/to/store/database/data"
      root_volume_path: "/local/path/to/store/database/root"
      backups_volume_path: "/local/path/to/store/database/file/backups"
      configs_volume_path: "/local/path/to/store/database/configs" # Removed in DoltLab >= v2.3.12
    replicas: 1
    placement:
      constraints: ["node.labels.doltlabdb == true"]
      preferences:
        - spread: "nodes.labels.doltlabdb"
  doltlabapi:
    host: "127.0.0.1"
    port: 9443
    csv_port: 9444
    cloud_storage:
      aws_region: "us-west-2"
      user_import_uploads_aws_bucket: "uploads-bucket"
      query_job_aws_bucket: "query-job-bucket"
      asyncworker_aws_sqs_queue: "async-queue"
    replicas: 1
    placement:
      constraints: ["node.labels.doltlabapi == true"]
      preferences:
        - spread: "nodes.labels.doltlabapi"
  doltlabremoteapi:
    host: "127.0.0.1"
    port: 50051
    file_server_port: 100
    cloud_storage:
      aws_region: "us-west-2"
      aws_bucket: "data-bucket"
      aws_dynamodb_table: "manifest-db"
    volume_paths:
      data_volume_path: "/local/path/to/store/remote/data"
    replicas: 1
    placement:
      constraints: ["node.labels.doltlabremoteapi == true"]
      preferences:
        - spread: "nodes.labels.doltlabremoteapi"
  doltlabfileserviceapi:
    host: "127.0.0.1"
    port: 4321
    volume_paths:
      uploads_volume_path: "/local/path/to/store/uploads"
    replicas: 1
    placement:
      constraints: ["node.labels.doltlabfileserviceapi == true"]
      preferences:
        - spread: "nodes.labels.doltlabfileserviceapi"
  doltlabgraphql:
    host: "127.0.0.1"
    port: 9000
    replicas: 1
    placement:
      constraints: ["node.labels.doltlabgraphql == true"]
      preferences:
        - spread: "nodes.labels.doltlabgraphql"
  doltlabui:
    host: "127.0.0.1"
    port: 80
    replicas: 1
    placement:
      constraints: ["node.labels.doltlabui == true"]
      preferences:
        - spread: "nodes.labels.doltlabui"
default_user:
  name: "admin"
  email: "admin@localhost"
  password: "*****"
jobs:
  concurrency_limit: 10
  concurrency_loop_seconds: 30
  max_retries: 5
enterprise:
  online_product_code: "*****"
  online_shared_key: "*****"
  online_api_key: "*****"
  online_license_key: "*****"
  offline_product_code: "*****"
  offline_shared_key: "*****"
  offline_api_key: "*****"
  offline_license_key: "*****"
  request_offline_activation: false
  offline_license_file: "/local/path/to/license/file"
  multihost_deployment: true
  no_multihost_default_placement_constraints: false
  no_multihost_default_placement_preferences_spreads: false
  scheme: "http"
  tls:
    cert_chain: "/path/to/cert.pem" # Deprecated: use `full_chain_cert` instead.
    full_chain_cert: "/path/to/cert.pem"
    private_key: "/path/to/key.pem"
  smtp:
    host: "smtp.email.com"
    port: 587
    auth_method: "plain"
    no_reply_email: "user@email.com"
    username: "user@email.com"
    password: "*****"
    oauth_token: "*****"
    identity: "doltlab"
    trace: "doltlab"
    client_hostname: "doltlab"
    implicit_tls: false
    insecure_tls: false
  saml:
    metadata_descriptor_file: "/path/to/metadata/descriptor"
    cert_common_name: "doltlab"
  oidc:
    issuer_url: "https://myidp.com/oidc"
    client_id: "my-oidc-client-id"
    client_secret: "my-oidc-client-secret"
  customize:
    logo: "/path/to/custom/logo"
    email_templates: true
    color_overrides:
      rgb_accent_1: "10, 10, 10"
      rgb_background_accent_1: "10, 10, 10"
      rgb_background_gradient_start: "10, 10, 10"
      rgb_button_1: "10, 10, 10"
      rgb_button_2: "10, 10, 10"
      rgb_link_1: "10, 10, 10"
      rgb_link_2: "10, 10, 10"
      rgb_link_light: "10, 10, 10"
  automated_backups:
    remote_url: "{aws,gs,oci}://remotebackupurl"
    aws_region: "us-west-2"
    aws_profile: "backup_profile"
    aws_shared_credentials_file: "/path/to/aws/shared/credentials/file"
    aws_config_file: "/path/to/aws/config/file"
    google_credentials_file: "/path/to/gcloud/credentials/file"
    oci_config_file: "/path/to/oci/config/file"
    oci_key_file: "/path/to/oci/key/file"
  super_admins: ["admin1@localhost", "admin2@localhost"]
```

The following are top-level `installer_config.yaml` options:

- [version](#version)
- [host](#host)
- [docker_network](#docker_network)
- [metrics_disabled](#metrics_disabled)
- [whitelist_all_users](#whitelist_all_users)
- [use_env](#use_env)
- [runtime](#runtime)
- [services](#services)
- [default_user](#default_user)
- [jobs](#jobs)
- [enterprise](#enterprise)

## version

_String_. The version of the configuration file and DoltLab. _Required_.

```yaml
# installer_config.yaml
version: v2.1.4
```

## host

_String_. The hostname or IP address of the host running DoltLab. _Required_.

```yaml
# example installer_config.yaml
host: mydoltlab.mycompany.com
```

```yaml
# example installer_config.yaml
host: 123.456.78.90
```

Command line equivalent [host](./cli.md#host).

## docker_network

_String_. The name of the docker network used for DoltLab, defaults to `doltlab`. _Optional_.

```yaml
# example installer_config.yaml
docker_network: doltlab
```

Command line equivalent [docker-network](./cli.md#docker-network).

## metrics_disabled

_Boolean_. If true, disables first party usage metrics for a DoltLab instance, defaults to `false`. _Optional_.

```yaml
# example installer_config.yaml
metrics_disabled: false
```

Command line equivalent [disable-usage-metrics](./cli.md#disable-usage-metrics).

## whitelist_all_users

_Boolean_. If true, allows any user to create an account on a DoltLab instance, defaults to `true`. _Optional_

```yaml
# example installer_config.yaml
whitelist_all_users: true
```

See [prevent unauthorized user account creation](../../guides/basic.md#prevent-unauthorized-user-account-creation) for more information.

Command line equivalent [whitelist-all-users](./cli.md#whitelist-all-users).

## use_env

_Boolean_. If true, sensitive values will not be written to generated assets and environment variables will be expected instead.

```yaml
# example installer_config.yaml
use_env: true
```

Command line equivalent [use-env](./cli.md#use-env).

## runtime

_String_. Selects the container runtime used by generated assets. Allowed values: `docker` (default) or `podman`.

When `runtime: podman` is set, the installer adjusts generated files to be compatible with Podman, including:

- Removing service `depends_on` entries (not supported by podman-compose)
- Setting `doltlabapi` service `user: "${UID}:${GID}"` and exporting `UID`/`GID` in `start.sh`
- Mapping the rootless Podman socket at `/run/user/${UID}/podman/podman.sock:/var/run/docker.sock`
- Setting `ENVOY_UID=0` for the `doltlabenvoy` service

```yaml
# example installer_config.yaml
runtime: podman
```

Command line equivalent [runtime](./cli.md#runtime).

## services

_Dictionary_. Configuration options for DoltLab's various services. `doltlabdb` passwords are _Required_ in single host deployments, other service definitions are _Required_ for multi-host deployments.

- [doltlabdb](#doltlabdb)
- [doltlabapi](#doltlabapi)
- [doltlabremoteapi](#doltlabremoteapi)
- [doltlabfileserviceapi](#doltlabfileserviceapi)
- [doltlabgraphql](#doltlabgraphql)
- [doltlabui](#doltlabui)
- [doltlabenvoy](#doltlabenvoy)

### doltlabdb

_Dictionary_. Configuration options for `doltlabdb`.

- [host](#doltlabdb-host)
- [port](#doltlabdb-port)
- [admin_password](#admin_password)
- [dolthubapi_password](#dolthubapi_password)
- [tls_skip_verify](#tls_skip_verify)
- [server_config](#server_config)
- [auto_gc_enabled](#auto_gc_enabled)
- [volume_paths](#doltlabdb-volume-paths)
- [replicas](#doltlabdb-replicas)
- [placement](#doltlabdb-placement)

<h4 id="doltlabdb-host">host</h4>

_String_. The host name or IP address of the host running `doltlabdb`. _Required_ for [configuring an external application database](../../guides/basic.md#use-external-database) and for multi-host deployments.

```yaml
# example installer_config.yaml
services:
  doltlabdb:
    host: "127.0.0.1"
```

Command line equivalent [doltlabdb-host](./cli.md#doltlabdb-host).

<h4 id="doltlabdb-port">port</h4>

_Number_. The port for `doltlabdb`. _Required_ for [configuring an external application database](../../guides/basic.md#use-external-database) and for [configuring multi-host deployments](../../guides/basic.md#deploy-doltlab-across-multiple-hosts).

```yaml
# example installer_config.yaml
services:
  doltlabdb:
    port: 3306
```

Command line equivalent [doltlabdb-port](./cli.md#doltlabdb-port).

#### admin_password

_String_. The password used to for creating user `dolthubadmin` in DoltLab's application database. _Required_.

```yaml
# example installer_config.yaml
services:
  doltlabdb:
    admin_password: "mypassword"
```

Command line equivalent [doltlabdb-admin-password](./cli.md#doltlabdb-admin-password).

#### dolthubapi_password

_String_. The password used to for creating user `dolthubapi` in DoltLab's application database. _Required_.

```yaml
# example installer_config.yaml
services:
  doltlabdb:
    dolthubapi_password: mypassword
```

Command line equivalent [doltlabdb-dolthubapi-password](./cli.md#doltlabdb-dolthubapi-password).

#### tls_skip_verify

_String_. If true, skips TLS verification during connection to `doltlabdb`. _Optional_.

```yaml
# example installer_config.yaml
services:
  doltlabdb:
    tls_skip_verify: false
```

Command line equivalent [doltlabdb-tls-skip-verify](./cli.md#doltlabdb-tls-skip-verify).

#### server_config

_String_. Absolute path to the `doltlabdb` server configuration file. _Optional_. If set, all other server specific settings
will be ignored, and this specified config file will be used in `doltlabdb`.

```yaml
# example installer_config.yaml
services:
  doltlabdb:
    server_config: /path/to/server/config.yaml
```

Command line equivalent [doltlabdb-server-config-file](./cli.md#doltlabdb-server-config-file).

#### auto_gc_enabled

_Boolean_. If true, [auto GC](https://docs.dolthub.com/sql-reference/server/garbage-collection#automated-gc) will be enabled on `doltlabdb`. _Optional_. This
will not be active if `server_config` is provided. In this case, enable auto GC on the config being supplied in `server_config`.

```yaml
# example installer_config.yaml
services:
  doltlabdb:
    auto_gc_enabled: true
```

Command line equivalent [doltlabdb-autogc-enabled](./cli.md#doltlabdb-autogc-enabled).

<h4 id="doltlabdb-volume-paths">volume_paths</h4>

_Dictionary_. Local paths used for persisting `doltlabdb` Docker volumes.

- [data_volume_path](#doltlabdb-data-volume-path)
- [root_volume_path](#root_volume_path)
- [backups_volume_path](#backups_volume_path)
- [configs_volume_path](#configs_volume_path)

<h4 id="doltlabdb-data-volume-path">data_volume_path</h4>

_String_. The path to an existing directory on the DoltLab host used for persisting the 'doltlabdb-dolt-data' Docker volume.

```yaml
# example installer_config.yaml
services:
  doltlabdb:
    volume_paths:
      data_volume_path: "/local/path/for/persisting/data"
```

Command line equivalent [doltlabdb-data-volume-host-path](./cli.md#doltlabdb-data-volume-host-path).

#### root_volume_path

_String_. The path to an existing directory on the DoltLab host used for persisting the 'doltlabdb-dolt-root' Docker volume.

```yaml
# example installer_config.yaml
services:
  doltlabdb:
    volume_paths:
      root_volume_path: "/local/path/for/persisting/doltlabdb/root"
```

Command line equivalent [doltlabdb-root-volume-host-path](./cli.md#doltlabdb-root-volume-host-path).

#### backups_volume_path

_String_. The path to an existing directory on the DoltLab host used for persisting the 'doltlabdb-dolt-backups' Docker volume.

```yaml
# example installer_config.yaml
services:
  doltlabdb:
    volume_paths:
      backups_volume_path: "/local/path/for/persisting/file/backups"
```

Command line equivalent [doltlabdb-backups-volume-host-path](./cli.md#doltlabdb-backups-volume-host-path).

#### configs_volume_path

_String_. The path to an existing directory on the DoltLab host used for persisting the 'doltlabdb-dolt-configs' Docker volume. The field volume has been removed in DoltLab >= v2.3.12
in favor of the [server_config](#server_config) field.

```yaml
# example installer_config.yaml
services:
  doltlabdb:
    volume_paths:
      configs_volume_path: "/local/path/for/persisting/doltlabdb/configs"
```

Command line equivalent [doltlabdb-configs-volume-host-path](./cli.md#doltlabdb-configs-volume-host-path).

<h4 id="doltlabdb-replicas">replicas</h4>

_Number_. Specifies the number of doltlabdb service replicas to run. NOTE: only a single replica of `doltlabdb` is currently supported. _Optional_, used for multi-host deployments.

```yaml
# example installer_config.yaml
services:
  doltlabdb:
    replicas: 1 
```

Command line equivalent [doltlabdb-replicas](./cli.md#doltlabdb-replicas).

<h4 id="doltlabdb-placement">placement</h4>

_Dictionary_. Configuration options for `placement`.

- [constraints](#doltlabdb-placement-constraints)
- [preferences](#doltlabdb-placement-preferences)

<h5 id="doltlabdb-placement-constraints">constraints</h5>

_String_ _Array_. The placement constraints to add to the `doltlabdb` service. By default, DoltLab will add the `node.labels.doltlabdb == true` constraint to a multihost deployment. DoltLab Enterprise only. _Optional_, used for multi-host deployments.

```yaml
# example installer_config.yaml
services:
  doltlabdb:
    placement:
      constraints: ["node.labels.doltlabdb == true"]
```

Command line equivalent [doltlabdb-placement-constraint](./cli.md#doltlabdb-placement-constraint).

<h5 id="doltlabdb-preferences">preferences</h5>

_Dictionary_. Configuration options for `preferences`.

- [spread](#doltlabdb-placement-preferences-spread)

<h6 id="doltlabdb-placement-preferences-spread">spread</h6>

_Dictionary_ _Array_. The spread preferences to add to the `doltlabdb` service. By default, DoltLab will add the `node.labels.doltlabdb` spread preference to a multihost deployment. DoltLab Enterprise only. _Optional_, used for multi-host deployments.

```yaml
# example installer_config.yaml
services:
  doltlabdb:
    placement:
      preferences:
        - spread: "node.labels.doltlabdb"
```

Command line equivalent [doltlabdb-placement-preferences-spread](./cli.md#doltlabdb-placement-preferences-spread).

### doltlabapi

_Dictionary_. Configuration options for `doltlabapi`.

- [csv_port](#csv_port)
- [cloud_storage](#doltlabapi-cloud-storage)
- [replicas](#doltlabapi-replicas)
- [placement](#doltlabapi-placement)

#### csv_port

_Number_. The port for `doltlabapi`'s csv service. _Required_ for [configuring multi-host deployments](../../guides/enterprise.md#deploy-doltlab-across-multiple-hosts).

```yaml
# example installer_config.yaml
services:
  doltlabapi:
    csv_port: 3306
```

Command line equivalent [doltlabapi-csv-port](./cli.md#doltlabapi-csv-port).

<h4 id="doltlabapi-cloud-storage">cloud_storage</h4>

_Dictionary_. Configuration options for persisting `doltlabapi` data to cloud resources.

- [aws_region](#doltlabapi-aws-region)
- [user_import_uploads_aws_bucket](#user_import_uploads_aws_bucket)
- [query_job_aws_bucket](#query_job_aws_bucket)
- [asyncworker_aws_sqs_queue](#asyncworker_aws_sqs_queue)

<h5 id="doltlabapi-aws-region">aws_region</h5>

_String_. The AWS region for 'doltlabapi' cloud storage AWS resources, DoltLab Enterprise only.

```yaml
# example installer_config.yaml
services:
  doltlabapi:
    cloud_storage:
      aws_region: "us-east-2"
```

Command line equivalent [doltlabapi-aws-region](./cli.md#doltlabapi-aws-region).

##### user_import_uploads_aws_bucket

_String_. The name of the S3 bucket used to store user uploaded files, DoltLab Enterprise only.

```yaml
# example installer_config.yaml
services:
  doltlabapi:
    cloud_storage:
      user_import_uploads_aws_bucket: "uploads-bucket"
```

Command line equivalent [doltlabapi-user-import-uploads-aws-s3-bucket](./cli.md#doltlabapi-user-import-uploads-aws-s3-bucket).

##### asyncworker_aws_sqs_queue

_String_. The name of the SQS queue used for processing asynchronous tasks, DoltLab Enterprise only.

```yaml
# example installer_config.yaml
services:
  doltlabapi:
    cloud_storage:
      asyncworker_aws_sqs_queue: "async-queue"
```

Command line equivalent [doltlabapi-asyncworker-aws-sqs-queue](./cli.md#doltlabapi-asyncworker-aws-sqs-queue).

<h4 id="doltlabapi-replicas">replicas</h4>

_Number_. Specifies the number of doltlabapi service replicas to run. _Optional_, used for multi-host deployments.

```yaml
# example installer_config.yaml
services:
  doltlabapi:
    replicas: 1 
```

Command line equivalent [doltlabapi-replicas](./cli.md#doltlabapi-replicas).

<h4 id="doltlabapi-placement">placement</h4>

_Dictionary_. Configuration options for `placement`.

- [constraints](#doltlabapi-placement-constraints)
- [preferences](#doltlabapi-placement-preferences)

<h5 id="doltlabapi-placement-constraints">constraints</h5>

_String_ _Array_. The placement constraints to add to the `doltlabapi` service. By default, DoltLab will add the `node.labels.doltlabapi == true` constraint to a multihost deployment. DoltLab Enterprise only. _Optional_, used for multi-host deployments.

```yaml
# example installer_config.yaml
services:
  doltlabapi:
    placement:
      constraints: ["node.labels.doltlabapi == true"]
```

Command line equivalent [doltlabapi-placement-constraint](./cli.md#doltlabapi-placement-constraint).

<h5 id="doltlabapi-preferences">preferences</h5>

_Dictionary_. Configuration options for `preferences`.

- [spread](#doltlabapi-placement-preferences-spread)

<h6 id="doltlabapi-placement-preferences-spread">spread</h6>

_Dictionary_ _Array_. The spread preferences to add to the `doltlabapi` service. By default, DoltLab will add the `node.labels.doltlabapi` spread preference to a multihost deployment. DoltLab Enterprise only. _Optional_, used for multi-host deployments.

```yaml
# example installer_config.yaml
services:
  doltlabapi:
    placement:
      preferences:
        - spread: "node.labels.doltlabapi"
```

Command line equivalent [doltlabapi-placement-preferences-spread](./cli.md#doltlabapi-placement-preferences-spread).

### doltlabremoteapi

_Dictionary_. Configuration options for `doltlabremoteapi`.

- [volume_paths](#doltlabremoteapi-volume-paths)
- [cloud_storage](#doltlabremoteapi-cloud-storage)
- [replicas](#doltlabremoteapi-replicas)
- [placement](#doltlabremoteapi-placement)

<h4 id="doltlabremoteapi-volume-paths">volume_paths</h4>

_Dictionary_. Local paths used for persisting `doltlabremoteapi` Docker volumes.

- [data_volume_path](#doltlabremoteapi-data-volume-path)

<h4 id="doltlabremoteapi-data-volume-path">data_volume_path</h4>

_String_. The path to an existing directory on the DoltLab host used for persisting the 'doltlab-remote-storage' Docker volume.

```yaml
# example installer_config.yaml
services:
  doltlabremoteapi:
    volume_paths:
      data_volume_path: "/path/for/persisting/remote/data"
```

Command line equivalent [doltlabremoteapi-data-volume-host-path](./cli.md#doltlabremoteapi-data-volume-host-path).

<h4 id="doltlabremoteapi-cloud-storage">cloud_storage</h4>

_Dictionary_. Configuration options for persisting `doltlabremoteapi` data to cloud resources.

- [aws_region](#doltlabremoteapi-aws-region)
- [aws_bucket](#doltlabremoteapi-aws-bucket)
- [aws_dynamodb_table](#aws_dynamodb_table)

<h5 id="doltlabremoteapi-aws-region">aws_region</h5>

_String_. The AWS region where the DynamoDb table is located. DoltLab Enterprise only.

```yaml
# example installer_config.yaml
services:
  doltlabremoteapi:
    cloud_storage:
      aws_region: "us-west-2"
```

Command line equivalent [doltlabremoteapi-storage-aws-region](./cli.md#doltlabremoteapi-storage-aws-region).

<h5 id="doltlabremoteapi-aws-bucket">aws_bucket</h5>

_String_. The AWS S3 bucket used for storing remote data files. DoltLab Enterprise only.

```yaml
# example installer_config.yaml
services:
  doltlabremoteapi:
    cloud_storage:
      aws_bucket: "remote-bucket"
```

Command line equivalent [doltlabremoteapi-storage-aws-bucket](./cli.md#doltlabremoteapi-storage-aws-bucket).

##### aws_dynamodb_table

_String_. The AWS DynamoDb table name used for storing the manifest of remote databases. DoltLab Enterprise only.

```yaml
# example installer_config.yaml
services:
  doltlabremoteapi:
    cloud_storage:
      aws_dynamodb_table: "manifest-db"
```

Command line equivalent [doltlabremoteapi-storage-aws-dynamodb-table](./cli.md#doltlabremoteapi-storage-aws-dynamodb-table).

<h4 id="doltlabremoteapi-replicas">replicas</h4>

_Number_. Specifies the number of doltlabremoteapi service replicas to run. NOTE: only a single replica of `doltlabremoteapi` is supported when cloud-backed storage is NOT configured. Use cloud-backed storage to remove this scaling limitation. DoltLab Enterprise only. _Optional_, used for multi-host deployments.

```yaml
# example installer_config.yaml
services:
  doltlabremoteapi:
    replicas: 1 
```

Command line equivalent [doltlabremoteapi-replicas](./cli.md#doltlabremoteapi-replicas).

<h4 id="doltlabremoteapi-placement">placement</h4>

_Dictionary_. Configuration options for `placement`.

- [constraints](#doltlabremoteapi-placement-constraints)
- [preferences](#doltlabremoteapi-placement-preferences)

<h5 id="doltlabremoteapi-placement-constraints">constraints</h5>

_String_ _Array_. The placement constraints to add to the `doltlabremoteapi` service. By default, DoltLab will add the `node.labels.doltlabremoteapi == true` constraint to a multihost deployment. DoltLab Enterprise only. _Optional_, used for multi-host deployments.

```yaml
# example installer_config.yaml
services:
  doltlabremoteapi:
    placement:
      constraints: ["node.labels.doltlabremoteapi == true"]
```

Command line equivalent [doltlabremoteapi-placement-constraint](./cli.md#doltlabremoteapi-placement-constraint).

<h5 id="doltlabremoteapi-preferences">preferences</h5>

_Dictionary_. Configuration options for `preferences`.

- [spread](#doltlabremoteapi-placement-preferences-spread)

<h6 id="doltlabremoteapi-placement-preferences-spread">spread</h6>

_Dictionary_ _Array_. The spread preferences to add to the `doltlabremoteapi` service. By default, DoltLab will add the `node.labels.doltlabremoteapi` spread preference to a multihost deployment. DoltLab Enterprise only. _Optional_, used for multi-host deployments.

```yaml
# example installer_config.yaml
services:
  doltlabremoteapi:
    placement:
      preferences:
        - spread: "node.labels.doltlabremoteapi"
```

Command line equivalent [doltlabremoteapi-placement-preferences-spread](./cli.md#doltlabremoteapi-placement-preferences-spread).

### doltlabfileserviceapi

_Dictionary_. Configuration options for `doltlabapifileserviceapi`.

- [volume_paths](#doltlabfileserviceapi-volume-paths)
- [replicas](#doltlabfileserviceapi-replicas)
- [placement](#doltlabfileserviceapi-placement)

<h4 id="doltlabfileserviceapi-volume-paths">volume_paths</h4>

_Dictionary_. Local paths used for persisting `doltlabfileserviceapi` Docker volumes.

- [uploads_volume_path](#uploads_volume_path)

<h4 id="doltlabfileserviceapi-uploads-volume-path">uploads_volume_path</h4>

_String_. The path to an existing directory on the DoltLab host for persisting the 'doltlab-user-uploads' Docker volume.

```yaml
# example installer_config.yaml
services:
  doltlabfileserviceapi:
    volume_paths:
      uploads_volume_path: "/path/for/persisting/user/uploads"
```

Command line equivalent [doltlabfileserviceapi-uploads-volume-host-path](./cli.md#doltlabfileserviceapi-uploads-volume-host-path).

<h4 id="doltlabfileserviceapi-replicas">replicas</h4>

_Number_. Specifies the number of doltlabfileserviceapi service replicas to run. NOTE: only a single replica of `doltlabfileserviceapi` is currently supported. Use cloud-backed storage to remove this scaling limitation. DoltLab Enterprise only. _Optional_, used for multi-host deployments.

```yaml
# example installer_config.yaml
services:
  doltlabfileserviceapi:
    replicas: 1 
```

Command line equivalent [doltlabfileserviceapi-replicas](./cli.md#doltlabfileserviceapi-replicas).

<h4 id="doltlabfileserviceapi-placement">placement</h4>

_Dictionary_. Configuration options for `placement`.

- [constraints](#doltlabfileserviceapi-placement-constraints)
- [preferences](#doltlabfileserviceapi-placement-preferences)

<h5 id="doltlabfileserviceapi-placement-constraints">constraints</h5>

_String_ _Array_. The placement constraints to add to the `doltlabfileserviceapi` service. By default, DoltLab will add the `node.labels.doltlabfileserviceapi == true` constraint to a multihost deployment. DoltLab Enterprise only. _Optional_, used for multi-host deployments.

```yaml
# example installer_config.yaml
services:
  doltlabfileserviceapi:
    placement:
      constraints: ["node.labels.doltlabfileserviceapi == true"]
```

Command line equivalent [doltlabfileserviceapi-placement-constraint](./cli.md#doltlabfileserviceapi-placement-constraint).

<h5 id="doltlabfileserviceapi-preferences">preferences</h5>

_Dictionary_. Configuration options for `preferences`.

- [spread](#doltlabfileserviceapi-placement-preferences-spread)

<h6 id="doltlabfileserviceapi-placement-preferences-spread">spread</h6>

_Dictionary_ _Array_. The spread preferences to add to the `doltlabfileserviceapi` service. By default, DoltLab will add the `node.labels.doltlabfileserviceapi` spread preference to a multihost deployment. DoltLab Enterprise only. _Optional_, used for multi-host deployments.

```yaml
# example installer_config.yaml
services:
  doltlabfileserviceapi:
    placement:
      preferences:
        - spread: "node.labels.doltlabfileserviceapi"
```

Command line equivalent [doltlabfileserviceapi-placement-preferences-spread](./cli.md#doltlabfileserviceapi-placement-preferences-spread).

### doltlabgraphql

_Dictionary_. Configuration options for `doltlabgraphql`.

- [replicas](#doltlabgraphql-replicas)
- [placement](#doltlabgraphql-placement)

<h4 id="doltlabgraphql-replicas">replicas</h4>

_Number_. Specifies the number of doltlabgraphql replicas to run. DoltLab Enterprise only. _Optional_, used for multi-host deployments.

```yaml
# example installer_config.yaml
services:
  doltlabgraphql:
    replicas: 1 
```

Command line equivalent [doltlabgraphql-replicas](./cli.md#doltlabgraphql-replicas).

<h4 id="doltlabgraphql-placement">placement</h4>

_Dictionary_. Configuration options for `placement`.

- [constraints](#doltlabgraphql-placement-constraints)
- [preferences](#doltlabgraphql-placement-preferences)

<h5 id="doltlabgraphql-placement-constraints">constraints</h5>

_String_ _Array_. The placement constraints to add to the `doltlabgraphql` service. By default, DoltLab will add the `node.labels.doltlabgraphql == true` constraint to a multihost deployment. DoltLab Enterprise only. _Optional_, used for multi-host deployments.

```yaml
# example installer_config.yaml
services:
  doltlabgraphql:
    placement:
      constraints: ["node.labels.doltlabgraphql == true"]
```

Command line equivalent [doltlabgraphql-placement-constraint](./cli.md#doltlabgraphql-placement-constraint).

<h5 id="doltlabgraphql-preferences">preferences</h5>

_Dictionary_. Configuration options for `preferences`.

- [spread](#doltlabgraphql-placement-preferences-spread)

<h6 id="doltlabgraphql-placement-preferences-spread">spread</h6>

_Dictionary_ _Array_. The spread preferences to add to the `doltlabgraphql` service. By default, DoltLab will add the `node.labels.doltlabgraphql` spread preference to a multihost deployment. DoltLab Enterprise only. _Optional_, used for multi-host deployments.

```yaml
# example installer_config.yaml
services:
  doltlabgraphql:
    placement:
      preferences:
        - spread: "node.labels.doltlabgraphql"
```

Command line equivalent [doltlabgraphql-placement-preferences-spread](./cli.md#doltlabgraphql-placement-preferences-spread).

### doltlabui

_Dictionary_. Configuration options for `doltlabui`.

- [replicas](#doltlabui-replicas)
- [placement](#doltlabui-placement)

<h4 id="doltlabui-replicas">replicas</h4>

_Number_. Specifies the number of doltlabui replicas to run. DoltLab Enterprise only. _Optional_, used for multi-host deployments.

```yaml
# example installer_config.yaml
services:
  doltlabui:
    replicas: 1 
```

Command line equivalent [doltlabui-replicas](./cli.md#doltlabui-replicas).

<h4 id="doltlabui-placement">placement</h4>

_Dictionary_. Configuration options for `placement`.

- [constraints](#doltlabui-placement-constraints)
- [preferences](#doltlabui-placement-preferences)

<h5 id="doltlabui-placement-constraints">constraints</h5>

_String_ _Array_. The placement constraints to add to the `doltlabui` service. By default, DoltLab will add the `node.labels.doltlabui == true` constraint to a multihost deployment. DoltLab Enterprise only. _Optional_, used for multi-host deployments.

```yaml
# example installer_config.yaml
services:
  doltlabui:
    placement:
      constraints: ["node.labels.doltlabui == true"]
```

Command line equivalent [doltlabui-placement-constraint](./cli.md#doltlabui-placement-constraint).

<h5 id="doltlabui-preferences">preferences</h5>

_Dictionary_. Configuration options for `preferences`.

- [spread](#doltlabui-placement-preferences-spread)

<h6 id="doltlabui-placement-preferences-spread">spread</h6>

_Dictionary_ _Array_. The spread preferences to add to the `doltlabui` service. By default, DoltLab will add the `node.labels.doltlabui` spread preference to a multihost deployment. DoltLab Enterprise only. _Optional_, used for multi-host deployments.

```yaml
# example installer_config.yaml
services:
  doltlabui:
    placement:
      preferences:
        - spread: "node.labels.doltlabui"
```

Command line equivalent [doltlabui-placement-preferences-spread](./cli.md#doltlabui-placement-preferences-spread).

### doltlabenvoy

_Dictionary_. Configuration options for `doltlabenvoy`.

- [replicas](#doltlabenvoy-replicas)
- [placement](#doltlabenvoy-placement)

<h4 id="doltlabenvoy-replicas">replicas</h4>

_Number_. Specifies the number of doltlabenvoy replicas to run. DoltLab Enterprise only. _Optional_, used for multi-host deployments.

```yaml
# example installer_config.yaml
services:
  doltlabenvoy:
    replicas: 1 
```

Command line equivalent [doltlabenvoy-replicas](./cli.md#doltlabenvoy-replicas).

<h4 id="doltlabenvoy-placement">placement</h4>

_Dictionary_. Configuration options for `placement`.

- [constraints](#doltlabenvoy-placement-constraints)
- [preferences](#doltlabenvoy-placement-preferences)

<h5 id="doltlabenvoy-placement-constraints">constraints</h5>

_String_ _Array_. The placement constraints to add to the `doltlabenvoy` service. By default, DoltLab will add the `node.labels.doltlabenvoy == true` constraint to a multihost deployment. DoltLab Enterprise only. _Optional_, used for multi-host deployments.

```yaml
# example installer_config.yaml
services:
  doltlabenvoy:
    placement:
      constraints: ["node.labels.doltlabenvoy == true"]
```

Command line equivalent [doltlabenvoy-placement-constraint](./cli.md#doltlabenvoy-placement-constraint).

<h5 id="doltlabenvoy-preferences">preferences</h5>

_Dictionary_. Configuration options for `preferences`.

- [spread](#doltlabenvoy-placement-preferences-spread)

<h6 id="doltlabenvoy-placement-preferences-spread">spread</h6>

_Dictionary_ _Array_. The spread preferences to add to the `doltlabenvoy` service. By default, DoltLab will add the `node.labels.doltlabenvoy` spread preference to a multihost deployment. DoltLab Enterprise only. _Optional_, used for multi-host deployments.

```yaml
# example installer_config.yaml
services:
  doltlabenvoy:
    placement:
      preferences:
        - spread: "node.labels.doltlabenvoy"
```

Command line equivalent [doltlabenvoy-placement-preferences-spread](./cli.md#doltlabenvoy-placement-preferences-spread).

## default_user

_Dictionary_. Configuration options for DoltLab's default user. _Required_.

- [name](#name)
- [password](#default-user-password)
- [email](#email)

### name

_String_. The username of the default user. _Required_.

```yaml
# example installer_config.yaml
default_user:
  name: admin
```

Command line equivalent [default-user](./cli.md#default-user).

<h3 id="default-user-password">password</h3>

_String_. The password of the default user. _Required_.

```yaml
# example installer_config.yaml
default_user:
  password: mypassword
```

Command line equivalent [default-user-password](./cli.md#default-user-password).

### email

_String_. The email address of the default user. _Required_.

```yaml
# example installer_config.yaml
default_user:
  email: admin@localhost
```

Command line equivalent [default-user-email](./cli.md#default-user-email).

## jobs

_Dictionary_. Job configuration options. _Optional_. See [improving DoltLab performance](../../guides/basic.md#improve-doltlab-performance) for more information.

- [concurrency_limit](#concurrency_limit)
- [concurrency_loop_seconds](#concurrency_loop_seconds)
- [max_retries](#max_retries)

### concurrency_limit

_Number_. The maximum number of concurrent Jobs. _Optional_.

```yaml
# example installer_config.yaml
jobs:
  concurrency_limit: 10
```

Command line equivalent [job-concurrency-limit](./cli.md#job-concurrency-limit).

### concurrency_loop_seconds

_Number_. The wait time in seconds before scheduling the next batch of jobs. _Optional_.

```yaml
# example installer_config.yaml
jobs:
  concurrency_loop_seconds: 30
```

Command line equivalent [job-concurrency-loop-seconds](#job-concurrency-loop-seconds).

### max_retries

_Number_. The maximum number of times to retry failed Jobs. _Optional_.

```yaml
# example installer_config.yaml
jobs:
  max_retries: 5
```

Command line equivalent [job-max-retries](./cli.md#job-max-retries).

## enterprise

_Dictionary_. Enterprise configuration options. _Optional_.

- [online_product_code](#online_product_code)
- [online_shared_key](#online_shared_key)
- [online_api_key](#online_api_key)
- [online_license_key](#online_license_key)
- [offline_product_code](#offline_product_code)
- [offline_shared_key](#offline_shared_key)
- [offline_api_key](#offline_api_key)
- [offline_license_key](#offline_license_key)
- [request_offline_activation](#request_offline_activation)
- [offline_license_file](#offline_license_file)
- [multihost_deployment](#multihost_deployment)
- [no_multihost_default_placement_constraints](#no_multihost_default_placement_constraints)
- [no_multihost_default_placement_preferences_spreads](#no_multihost_default_placement_preferences_spreads)
- [scheme](#scheme)
- [tls](#tls)
- [smtp](#smtp)
- [customize](#customize)
- [automated_backups](#automated_backups)
- [super_admins](#super_admins)
- [saml](#saml)
- [oidc](#oidc)

### online_product_code

_String_. The online product code for your Enterprise account. _Required_.

```yaml
# example installer_config.yaml
enterprise:
  online_product_code: "myproductcode"
```

Command line equivalent [enterprise-online-product-code](./cli.md#enterprise-online-product-code).

### online_shared_key

_String_. The online shared key for your Enterprise account. _Required_.

```yaml
# example installer_config.yaml
enterprise:
  online_shared_key: "mysharedkey"
```

Command line equivalent [enterprise-online-shared-key](./cli.md#enterprise-online-shared-key).

### online_api_key

_String_. The online api key for your Enterprise account. _Required_.

```yaml
# example installer_config.yaml
enterprise:
  online_api_key: "myapikey"
```

Command line equivalent [enterprise-online-api-key](./cli.md#enterprise-online-api-key).

### online_license_key

_String_. The online license key for your Enterprise account. _Required_.

```yaml
# example installer_config.yaml
enterprise:
  online_license_key: "mylicensekey"
```

### offline_product_code

_String_. The offline product code for your Enterprise account. _Required_ for offline Enterprise.

```yaml
# example installer_config.yaml
enterprise:
  offline_product_code: "myproductcode"
```

Command line equivalent [enterprise-offline-product-code](./cli.md#enterprise-offline-product-code).

### offline_shared_key

_String_. The offline shared key for your Enterprise account. _Required_ for offline Enterprise.

```yaml
# example installer_config.yaml
enterprise:
  offline_shared_key: "mysharedkey"
```

Command line equivalent [enterprise-offline-shared-key](./cli.md#enterprise-offline-shared-key).

### offline_api_key

_String_. The offline api key for your Enterprise account. _Required_ for offline Enterprise.

```yaml
# example installer_config.yaml
enterprise:
  offline_api_key: "myapikey"
```

Command line equivalent [enterprise-offline-api-key](./cli.md#enterprise-offline-api-key).

### offline_license_key

_String_. The offline license key for your Enterprise account. _Required_ for offline Enterprise.

```yaml
# example installer_config.yaml
enterprise:
  offline_license_key: "mylicensekey"
```

Command line equivalent [enterprise-offline-license-key](./cli.md#enterprise-offline-license-key).

### request_offline_activation

_Boolean_. If true, will generate an activation file that must be provided to the DoltLab team.. _Optional_.

```yaml
# example installer_config.yaml
enterprise:
  request_offline_activation: true
```

Command line equivalent [enterprise-offline-license-key](./cli.md#enterprise-offline-license-key).

### offline_license_file

_String_. The offline license file for your Enterprise account, provided by the DoltHub team. _Required_ for offline Enterprise.

```yaml
# example installer_config.yaml
enterprise:
  offline_license_file: "/path/to/license/file"
```

Command line equivalent [enterprise-offline-license-file](./cli.md#enterprise-offline-license-file).

### multihost_deployment

_Boolean_. If true, generates DoltLab Enterprise assets that will run via Docker Swarm. DoltLab Enterprise only. _Optional_.

```yaml
# example installer_config.yaml
enterprise:
  multihost_deployment: true
```

Command line equivalent [multihost-deployment](./cli.md#multihost-deployment).

### no_multihost_default_placement_constraints

_Boolean_. If true, will not add the default placement contraints to services when running in multihost deployment mode. DoltLab Enterprise only.. _Optional_.

```yaml
# example installer_config.yaml
enterprise:
  no_multihost_default_placement_constraints: true
```

Command line equivalent [no-default-placement-constraints](./cli.md#no-default-placement-constraints).

### no_multihost_default_placement_preferences_spreads

_Boolean_. If true, will not add the default placement preferences spread to services when running in multihost deployment mode. DoltLab Enterprise only. _Optional_.

```yaml
# example installer_config.yaml
enterprise:
  no_multihost_default_placement_preferences_spreads: true
```

Command line equivalent [no-default-placement-preferences-spreads](./cli.md#no-default-placement-preferences-spreads).

## scheme

_String_. The HTTP scheme of the DoltLab deployment, defaults to `http`. DoltLab Enterprise only. _Optional_.

```yaml
# example installer_config.yaml
enterprise:
  scheme: http
```

See [how to serve DoltLab over HTTPS](../../guides/enterprise.md#doltlab-https-natively) for more information.

Command line equivalent [scheme](./cli.md#scheme).

## tls

_Dictionary_. TLS configuration options. DoltLab Enterprise only. _Optional_. See [serving DoltLab natively over HTTPS](../../guides/enterprise.md#serve-doltlab-over-https-natively) for more information.

- [cert_chain](#cert_chain) Deprecated, use `full_chain_cert` instead.
- [full_chain_cert](#full_chain_cert)
- [private_key](#private_key)

### cert_chain

_String_. Deprecated, use `full_chain_cert` instead. The absolute path to a TLS full chain certificate with `.pem` extension. _Required_.

```yaml
# example installer_config.yaml
enterprise:
  tls:
    cert_chain: /path/to/tls/cert/chain.pem
```

Command line equivalent [tls-cert-chain](./cli.md#tls-cert-chain).

### full_chain_cert

_String_. The absolute path to a TLS full chain certificate with `.pem` extension. _Required_.

```yaml
# example installer_config.yaml
enterprise:
  tls:
    full_chain_cert: /path/to/tls/cert/chain.pem
```

Command line equivalent [tls-full-chain-cert](./cli.md#tls-full-chain-cert).

### private_key

_String_. The absolute path to a TLS private key with `.pem` extension. _Required_.

```yaml
# example installer_config.yaml
enterprise:
  tls:
    private_key: /path/to/tls/private/key.pem
```

Command line equivalent [tls-private-key](./cli.md#tls-private-key).

## smtp

_Dictionary_. The configuration options for an external SMTP server. DoltLab Enterprise only. _Optional_. See [connecting DoltLab to an SMTP server](../../guides/enterprise.md#connect-doltlab-to-an-smtp-server) for more information.

- [auth_method](#auth_method)
- [host](#smtp-host)
- [port](#smtp-port)
- [no_reply_email](#no_reply_email)
- [username](#username)
- [password](#smtp-password)
- [oauth_token](#oauth-token)
- [identity](#identity)
- [trace](#trace)
- [implicit_tls](#implicit-tls)
- [insecure_tls](#insecure-tls)

### auth_method

_String_. The authentication method used by the SMTP server. _Required_. One of `plain`, `login`, `oauthbearer`, `anonymous`, `external`, and `disable`.

```yaml
# example installer_config.yaml
enterprise:
  smtp:
    auth_method: plain
```

Command line equivalent [smtp-auth-method](./cli.md#smtp-auth-method).

<h3 id="smtp-host">host</h3>

_String_. The host name of the SMTP server. _Required_.

```yaml
# example installer_config.yaml
enterprise:
  smtp:
    host: smtp.gmail.com
```

Command line equivalent [smtp-host](./cli.md#smtp-host).

<h3 id="smtp-port">port</h3>

_Number_. The port of the SMTP server. _Required_.

```yaml
# example installer_config.yaml
enterprise:
  smtp:
    port: 587
```

Command line equivalent [smtp-port](./cli.md#smtp-port).

### no_reply_email

_String_. The email address used to send emails from DoltLab. _Required_.

```yaml
# example installer_config.yaml
enterprise:
  smtp:
    no_reply_email: admin@localhost
```

Command line equivalent [no-reply-email](./cli.md#no-reply-email).

### username

_String_. The username used for connecting to the SMTP server. _Required_ for `auth_method` `login` and `plain`.

```yaml
# example installer_config.yaml
enterprise:
  smtp:
    username: mysmtpusername
```

Command line equivalent [smtp-username](./cli.md#smtp-username).

<h3 id="smtp-password">password</h3>

_String_. The password used for connecting to the SMTP server. _Required_ for `auth_method` `login` and `plain`.

```yaml
# example installer_config.yaml
enterprise:
  smtp:
    password: mypassword
```

Command line equivalent [smtp-password](./cli.md#smtp-password).

### oauth_token

_String_. The oauth token used for connecting to the SMTP server. _Required_ for `auth_method` `oauthbearer`.

```yaml
# example installer_config.yaml
enterprise:
  smtp:
    oauth_token: myoauthtoken
```

Command line equivalent [smtp-oauth-token](./cli.md#smtp-oauth-token).

### identity

_String_. The SMTP server identity. _Optional_.

```yaml
# example installer_config.yaml
enterprise:
  smtp:
    identity: mysmtpidentity
```

Command line equivalent [smtp-identity](./cli.md#smtp-identity).

### trace

_String_. The SMTP server trace. _Optional_.

```yaml
# example installer_config.yaml
enterprise:
  smtp:
    trace: mysmtptrace
```

Command line equivalent [smtp-trace](./cli.md#smtp-trace).

### implicit_tls

_Boolean_. If true, uses implicit TLS to connect to the SMTP server. _Optional_.

```yaml
# example installer_config.yaml
enterprise:
  smtp:
    implicit_tls: false
```

Command line equivalent [smtp-implicit-tls](./cli.md#smtp-implicit-tls).

### insecure_tls

_Boolean_. If true, uses insecure TLS to connect to the SMTP server. _Optional_.

```yaml
# example installer_config.yaml
enterprise:
  smtp:
    insecure_tls: false
```

Command line equivalent [smtp-insecure-tls](./cli.md#smtp-insecure-tls).

### customize

_Dictionary_. Customizable option configuration. _Optional_.

- [email_templates](#email_templates)
- [logo](#logo)
- [color_overrides](#color_overrides)

#### email_templates

_Boolean_. If true, generates email templates that can be customized. DoltLab Enterprise only. _Optional_. See [customizing DoltLab emails](../../guides/enterprise.md#customize-automated-emails) for more information.

```yaml
# example installer_config.yaml
enterprise:
  email_templates: true
```

Command line equivalent [custom-email-templates](./cli.md#custom-email-templates).

#### logo

_String_. Absolute path to custom logo file. _Optional_. See [customizing DoltLab's logo](../../guides/enterprise.md#use-custom-logo-on-doltlab-instance) for more information.

```yaml
# example installer_config.yaml
enterprise:
  logo: "/path/to/custom/logo.png"
```

Command line equivalent [custom-logo](./cli.md#custom-logo).

#### color_overrides

_Dictionary_. Color override options. _Optional_. See [customizing DoltLab colors](../../guides/enterprise.md#customize-doltlab-colors) for more information.

- [rgb_accent_1](#rgb_accent_1)
- [rgb_background_accent_1](#rgb_background_accent_1)
- [rgb_background_gradient_start](#rgb_background_gradient_start)
- [rgb_button_1](#rgb_button_1)
- [rgb_button_2](#rgb_button_2)
- [rgb_link_1](#rgb_link_1)
- [rgb_link_2](#rgb_link_2)
- [rgb_link_light](#rgb_link_light)
- [rgb_primary](#rgb_primary)
- [rgb_code_background](#rgb_code_background)

##### rgb_accent_1

_String_. Comma separated RGB color used to replace accent 1. _Optional_.

```yaml
# example installer_config.yaml
enterprise:
  customize:
    color_overrides:
      rgb_accent_1: "5, 117, 245"
```

Command line equivalent [custom-color-rgb-accent-1]./cli.md(#custom-color-rgb-accent-1).

##### rgb_background_accent_1

_String_. Comma separated RGB color used to replace background accent 1. _Optional_.

```yaml
# example installer_config.yaml
enterprise:
  customize:
    color_overrides:
      rgb_background_accent_1: "5, 117, 245"
```

Command line equivalent [custom-color-rgb-background-accent-1](./cli.md#custom-color-rgb-background-accent-1).

##### rgb_background_gradient_start

_String_. Comma separated RGB color used to replace background gradient start. _Optional_.

```yaml
# example installer_config.yaml
enterprise:
  customize:
    color_overrides:
      rgb_background_gradient_start: "5, 117, 245"
```

Command line equivalent [custom-color-rgb-background-gradient-start](./cli.md#custom-color-rgb-background-gradient-start).

##### rgb_button_1

_String_. Comma separated RGB color used to replace button 1. _Optional_.

```yaml
# example installer_config.yaml
enterprise:
  customize:
    color_overrides:
      rgb_button_1: "5, 117, 245"
```

Command line equivalent [custom-color-rgb-button-1](./cli.md#custom-color-rgb-button-1).

##### rgb_button_2

_String_. Comma separated RGB color used to replace button 2. _Optional_.

```yaml
# example installer_config.yaml
enterprise:
  customize:
    color_overrides:
      rgb_button_2: "5, 117, 245"
```

Command line equivalent [custom-color-rgb-button-2](./cli.md#custom-color-rgb-button-2).

##### rgb_link_1

_String_. Comma separated RGB color used to replace link 1. _Optional_.

```yaml
# example installer_config.yaml
enterprise:
  customize:
    color_overrides:
      rgb_link_1: "5, 117, 245"
```

Command line equivalent [custom-color-rgb-link-1](./cli.md#custom-color-rgb-link-1).

##### rgb_link_2

_String_. Comma separated RGB color used to replace link 2. _Optional_.

```yaml
# example installer_config.yaml
enterprise:
  customize:
    color_overrides:
      rgb_link_2: "5, 117, 245"
```

Command line equivalent [custom-color-rgb-link-2](./cli.md#custom-color-rgb-link-2).

##### rgb_link_light

_String_. Comma separated RGB color used to replace link light. _Optional_.

```yaml
# example installer_config.yaml
enterprise:
  customize:
    color_overrides:
      rgb_link_light: "5, 117, 245"
```

Command line equivalent [custom-color-rgb-link-light](./cli.md#custom-color-rgb-link-light).

##### rgb_primary

_String_. Comma separated RGB color used to replace primary. _Optional_.

```yaml
# example installer_config.yaml
enterprise:
  customize:
    color_overrides:
      rgb_primary: "5, 117, 245"
```

Command line equivalent [custom-color-rgb-primary](./cli.md#custom-color-rgb-primary).

##### rgb_code_background

_String_. Comma separated RGB color used to replace code background. _Optional_.

```yaml
# example installer_config.yaml
enterprise:
  customize:
    color_overrides:
      rgb_code_background: "5, 117, 245"
```

Command line equivalent [custom-color-rgb-code-background](./cli.md#custom-color-rgb-code-background).

### automated_backups

_Dictionary_. Automated backups options. _Optional_. See [automated backups](../../guides/enterprise.md#automated-remote-backups) for more information.

- [remote_url](#remote_url)
- [cron_schedule](#cron_schedule)
- [backup_on_boot](#backup_on_boot)
- [aws_region](#aws_region)
- [aws_profile](#aws_profile)
- [aws_shared_credentials_file](#aws_shared_credentials_file)
- [aws_config_file](#aws_config_file)
- [google_credentials_file](#google_credentials_file)
- [oci_config_file](#oci_config_file)
- [oci_key_file](#oci_key_file)

#### remote_url

_String_. Remote url for pushing `doltlabdb` backups. _Required_.

```yaml
# example installer_config.yaml
enterprise:
  automated_backups:
    remote_url: "aws://[dolt_dynamo_table:dolt_remotes_s3_storage]/backup_name"
```

Command line equivalent [automated-dolt-backups-url](./cli.md#automated-dolt-backups-url).

#### cron_schedule

_String_. Cron schedule for backup frequency. _Optional_.

```yaml
# example installer_config.yaml
enterprise:
  automated_backups:
    cron_schedule: "*/15 * * * *"
```

Command line equivalent [automated-dolt-backups-cron-schedule](./cli.md#automated-dolt-backups-cron-schedule).

#### backup_on_boot

_Boolean_. If true, creates first backup when DoltLab is started. _Optional_.

```yaml
# example installer_config.yaml
enterprise:
  automated_backups:
    backup_on_boot: true
```

Command line equivalent [automated-dolt-backups-backup-on-boot](./cli.md#automated-dolt-backups-backup-on-boot).

#### aws_region

_String_. AWS region. _Required_ if `remote_url` has scheme `aws://`.

```yaml
# example installer_config.yaml
enterprise:
  automated_backups:
    aws_region: "us-west-2"
```

Command line equivalent [aws-region](./cli.md#aws-region).

#### aws_profile

_String_. AWS profile name. _Required_ if `remote_url` has scheme `aws://`.

```yaml
# example installer_config.yaml
enterprise:
  automated_backups:
    aws_profile: "doltlab_backuper"
```

Command line equivalent [aws-profile](./cli.md#aws-profile).

#### aws_shared_credentials_file

_String_. Absolute path to AWS shared credentials file. _Required_ if `remote_url` has scheme `aws://`.

```yaml
# example installer_config.yaml
enterprise:
  automated_backups:
    aws_shared_credentials_file: "/absolute/path/to/aws/credentials"
```

Command line equivalent [aws-shared-credentials-file](./cli.md#aws-shared-credentials-file).

#### aws_config_file

_String_. Absolute path to AWS config file. _Required_ if `remote_url` has scheme `aws://`.

```yaml
# example installer_config.yaml
enterprise:
  automated_backups:
    aws_config_file: "/absolute/path/to/aws/config"
```

Command line equivalent [aws-config-file](./cli.md#aws-config-file).

#### google_credentials_file

_String_. Absolute path to Google cloud application credentials file. _Required_ if `remote_url` has scheme `gs://`.

```yaml
# example installer_config.yaml
enterprise:
  automated_backups:
    google_credentials_file: "/absolute/path/to/gcloud/credentials"
```

Command line equivalent [google-creds-file](./cli.md#google-creds-file).

#### oci_config_file

_String_. Absolute path to Oracle cloud configuration file. _Required_ if `remote_url` has scheme `oci://`.

```yaml
# example installer_config.yaml
enterprise:
  automated_backups:
    oci_config_file: "/absolute/path/to/oci/config"
```

Command line equivalent [oci-config-file](./cli.md#oci-config-file).

#### oci_key_file

_String_. Absolute path to Oracle cloud key file. _Required_ if `remote_url` has scheme `oci://`.

```yaml
# example installer_config.yaml
enterprise:
  automated_backups:
    oci_key_file: "/absolute/path/to/oci/key"
```

Command line equivalent [oci-key-file](./cli.md#oci-key-file).

#### super_admins

_String_ _Array_. Email addresses for users granted "super admin" privileges.

```yaml
# example installer_config.yaml
enterprise:
  super_admins: ["admin1@email.com", "admin2@gmail.com"]
```

Command line equivalent [super-admin-email](./cli.md#super-admin-email).

## saml

_Dictionary_. SAML single-sign-on options. _Optional_. See [saml configuration](../../guides/enterprise.md#configure-saml-single-sign-on) for more information.

- [metadata_descriptor_file](#metadata_descriptor_file)
- [cert_common_name](#cert_common_name)

### metadata_descriptor_file

_String_. Absolute path to metadata descriptor file. _Required_.

```yaml
# example installer_config.yaml
enterprise:
  saml:
    metadata_descriptor_file: "/absolute/path/to/metadata/descriptor/file"
```

Command line equivalent [sso-saml-metadata-descriptor](./cli.md#sso-saml-metadata-descriptor).

### cert_common_name

_String_. Common name to use in generated SAML certificate. _Required_.

```yaml
# example installer_config.yaml
enterprise:
  saml:
    cert_common_name: "mydoltlabcommonname"
```

Command line equivalent [sso-saml-cert-common-name](./cli.md#sso-saml-cert-common-name).

## oidc 

_Dictionary_. OIDC single-sign-on options. _Optional_. See [oidc configuration](../../guides/enterprise.md#configure-oidc-single-sign-on) for more information.

- [issuer_url](#issuer_url)
- [client_id](#client_id)
- [client_secret](#client_secret)

### issuer_url

_String_. The url of the OIDC identity provider. _Required_.

```yaml
# example installer_config.yaml
enterprise:
  oidc:
    issuer_url: "https://myidp.com/oidc"
```

### client_id

_String_. The OIDC client id. _Required_.

```yaml
# example installer_config.yaml
enterprise:
  oidc:
    client_id: "my-oidc-client-id"
```

### client_secret

_String_. The OIDC client secret. _Required_.

```yaml
# example installer_config.yaml
enterprise:
  oidc:
    client_secret: "my-oidc-client-secret"
```

