---
title: Installer command line reference
---

# Installer command line reference

## automated-dolt-backups-backup-on-boot

_Boolean_. If true, will create a backup when the `backup-syncer` service comes online, DoltLab Enterprise only (default true).

Configuration file equivalent [backup_on_boot](./configuration-file.md#backup_on_boot).

## automated-dolt-backups-cron-schedule

_String_. The cron schedule to use for automated doltlabdb backups, DoltLab Enterprise only, (default "0 0 * * *").

Configuration file equivalent [cron_schedule](./configuration-file.md#cron_schedule).

## automated-dolt-backups-url

_String_. Dolt remote url used for creating automated backups of DoltLab's Dolt server, DoltLab Enterprise only.

Configuration file equivalent [remote_url](./configuration-file.md#remote_url).

## aws-config-file

_String_. AWS configuration file, used for configuring automated `doltlabdb` backups to AWS, DoltLab Enterprise only.

Configuration file equivalent [aws_config_file](./configuration-file.md#aws_config_file).

## aws-profile

_String_. AWS profile, used for configuring `doltlabdb` automated AWS backups, DoltLab Enterprise only.

Configuration file equivalent [aws_profile](./configuration-file.md#aws_profile).

## aws-region

_String_. AWS region, used for configuring `doltlabdb` automated AWS backups, DoltLab Enterprise only.

Configuration file equivalent [aws_region](./configuration-file.md#aws_region).

## aws-shared-credentials-file

_String_. Absolute path to an AWS shared credentials file, used for configuring `doltlabdb` automated aws backups, DoltLab Enterprise only.

Configuration file equivalent [aws_shared_credentials_file](./configuration-file.md#aws_shared_credentials_file).

## centos

_Boolean_. If true will generate a script to install DoltLab's dependencies on CentOS.

## config

_String_. Absolute path to `installer` configuration file. By default, the `installer` will look for `installer_config.yaml` in its same directory.

## custom-color-rgb-accent-1

_String_. Supply a comma-separated RGB value for `accent_1`, DoltLab Enterprise only.

Configuration file equivalent [rgb_accent_1](./configuration-file.md#rgb_accent_1).

## custom-color-rgb-background-accent-1

_String_. Supply a comma-separated RGB value for `background_accent_1`, DoltLab Enterprise only.

Configuration file equivalent [rgb_background_accent_1](./configuration-file.md#rgb_background_accent_1).

## custom-color-rgb-background-gradient-start

_String_. Supply a comma-separated RGB value for `background_gradient_start`, DoltLab Enterprise only.

Configuration file equivalent [rgb_background_gradient_start](./configuration-file.md#rgb_background_gradient_start).

## custom-color-rgb-button-1

_String_. Supply a comma-separated RGB value for `button_1`, DoltLab Enterprise only.

Configuration file equivalent [rgb_button_1](./configuration-file.md#rgb_button_1).

## custom-color-rgb-button-2

_String_. Supply a comma-separated RGB value for `button_2`, DoltLab Enterprise only.

Configuration file equivalent [rgb_button_2](./configuration-file.md#rgb_button_2).

## custom-color-rgb-link-1

_String_. Supply a comma-separated RGB value for `link_1`, DoltLab Enterprise only.

Configuration file equivalent [rgb_link_1](./configuration-file.md#rgb_link_1).

## custom-color-rgb-link-2

_String_. Supply a comma-separated RGB value for `link_2`, DoltLab Enterprise only.

Configuration file equivalent [rgb_link_2](./configuration-file.md#rgb_link_2).

## custom-color-rgb-link-light

_String_. Supply a comma-separated RGB value for `link_light`, DoltLab Enterprise only.

Configuration file equivalent [rgb_link_light](./configuration-file.md#rgb_link_light).

## custom-color-rgb-primary

_String_. Supply a comma-separated RGB value for `primary`, DoltLab Enterprise only.

Configuration file equivalent [rgb_primary](./configuration-file.md#rgb_primary).

## custom-color-rgb-code-background

_String_. Supply a comma-separated RGB value for `code_background`, DoltLab Enterprise only.

Configuration file equivalent [rgb_code_background](./configuration-file.md#rgb_code_background).

## custom-email-templates

_Boolean_. If true, will generate email templates that can be customized, DoltLab Enterprise only.

Configuration file equivalent [email_templates](./configuration-file.md#email_templates).

## custom-logo

_String_. Absolute path to an image file to replace DoltLab's logo, DoltLab Enterprise only.

Configuration file equivalent [logo](./configuration-file.md#logo).

## default-user

_String_. The desired username of the default DoltLab user, (default "admin").

Configuration file equivalent [name](./configuration-file.md#name).

## default-user-email

_String_. The email address used to create the default DoltLab user.

Configuration file equivalent [email](./configuration-file.md#email).

## default-user-password

_String_. The password used to create the default DoltLab user.

Configuration file equivalent [password](./configuration-file.md#default-user-password).

## disable-usage-metrics

_Boolean_. If true, will not collect first-party metrics.

Configuration file equivalent [metrics_disabled](./configuration-file.md#metrics_disabled).

## docker-network

_String_. The docker network to run DoltLab in, (default "doltlab").

Configuration file equivalent [docker_network](./configuration-file.md#docker_network).

## doltlabapi-asyncworker-aws-sqs-queue

_String_. The name of the SQS queue used for processing asynchronous tasks, DoltLab Enterprise only.

Configuration file equivalent [asyncworker_aws_sqs_queue](./configuration-file.md#asyncworker_aws_sqs_queue).

## doltlabapi-aws-region

_String_. The AWS region for 'doltlabapi' cloud storage AWS resources, DoltLab Enterprise only.

Configuration file equivalent [aws_region](./configuration-file.md#doltlabapi-aws-region).

## doltlabapi-csv-port

_Number_. The port for `doltlabapi`'s CSV service.

Configuration file equivalent [csv_port](./configuration-file.md#csv_port).

## doltlabapi-query-job-aws-s3-bucket

_String_. The name of the S3 bucket used to store the results of SQL query Jobs, DoltLab Enterprise only.

Configuration file equivalent [query_job_aws_bucket](./configuration-file.md#query_job_aws_bucket).

## doltlabdb-admin-password

_String_. The `dolthubadmin` SQL user password of the `doltlabdb` instance.

Configuration file equivalent [admin_password](./configuration-file.md#admin_password).

## doltlabdb-autogc-enabled

_Boolean_. If true, automatic garbage collection will be enabled on the `doltlabdb` server..

Configuration file equivalent [auto_gc_enabled](./configuration-file.md#auto_gc_enabled).

## doltlabdb-backups-volume-host-path

_String_. The path to an existing directory on the DoltLab host used for persisting the 'doltlabdb-dolt-backups' Docker volume.

Configuration file equivalent [backups_volume_path](./configuration-file.md#backups_volume_path).

## doltlabdb-config-volume-host-path

_String_. The path to an existing directory on the DoltLab host used for persisting the 'doltlabdb-dolt-configs' Docker volume. This has been removed
in DoltLab >= v2.3.12 in favor of [doltlabdb-server-config-file](#doltlabdb-server-config-file).

Configuration file equivalent [configs_volume_path](./configuration-file.md#configs_volume_path).

## doltlabdb-data-volume-host-path

_String_. The path to an existing directory on the DoltLab host used for persisting the 'doltlabdb-dolt-data' Docker volume.

Configuration file equivalent [data_volume_path](./configuration-file.md#doltlabdb-data-volume-path).

## doltlabdb-dolthubapi-password

_String_. The `dolthubapi` SQL user password of the `doltlabdb` instance.

Configuration file equivalent [dolthubapi_password](./configuration-file.md#dolthubapi_password).

## doltlabdb-host

_String_. The hostname or IP address of `doltlabdb`.

Configuration file equivalent [host](./configuration-file.md#doltlabdb-host).

## doltlabdb-placement-constraint

_String_. The placement constraint to add to the doltlabdb service. Can be supplied multiple times. By default, DoltLab will add the `node.labels.doltlabdb == true` constraint to a multihost deployment. DoltLab Enterprise only.

Configuration file equivalent [placement_constraints](./configuration-file.md#doltlabdb-placement-constraints).

## doltlabdb-placement-preferences-spread

_String_. The placement preferences spread to add to the doltlabdb service. Can be supplied multiple times. DoltLab Enterprise only.

Configuration file equivalent [placement_preferences_spread](./configuration-file.md#doltlabdb-placement-preferences-spread).

## doltlabdb-port

_Number_. The port of `doltlabdb`.

Configuration file equivalent [port](./configuration-file.md#doltlabdb-port).

## doltlabdb-replicas

_Number_. Specifies the number of doltlabdb service replicas to run. NOTE: only a single replica of `doltlabdb` is currently supported. DoltLab Enterprise only.

Configuration file equivalent [replicas](./configuration-file.md#doltlabdb-replicas).

## doltlabdb-root-volume-host-path

_String_. The path to an existing directory on the DoltLab host used for persisting the 'doltlabdb-dolt-root' Docker volume.

Configuration file equivalent [root_volume_path](./configuration-file.md#root_volume_path).

## doltlabdb-tls-skip-verify

_Boolean_. If true, will disable TLS verification for connection to `doltlabdb`.

Configuration file equivalent [tls_skip_verify](./configuration-file.md#tls_skip_verify).

## doltlabdb-server-config-file

_String_. Absolute path to the `doltlabdb` server configuration file.

Configuration file equivalent [server_config](./configuration-file.md#server_config).

## doltlabapi-placement-constraint

_String_. The placement constraint to add to the doltlabapi service. Can be supplied multiple times. By default, DoltLab will add the `node.labels.doltlabapi == true` constraint to a multihost deployment. DoltLab Enterprise only.

Configuration file equivalent [placement_constraints](./configuration-file.md#doltlabapi-placement-constraints).

## doltlabapi-placement-preferences-spread

_String_. The placement preferences spread to add to the doltlabapi service. Can be supplied multiple times. DoltLab Enterprise only.

Configuration file equivalent [placement_preferences_spread](./configuration-file.md#doltlabapi-placement-preferences-spread).

## doltlabapi-replicas

_Number_. Specifies the number of doltlabapi service replicas to run. DoltLab Enterprise only.

Configuration file equivalent [replicas](./configuration-file.md#doltlabapi-replicas).

## doltlabenvoy-placement-constraint

_String_. The placement constraint to add to the doltlabenvoy service. Can be supplied multiple times. By default, DoltLab will add the `node.labels.doltlabenvoy == true` constraint to a multihost deployment. DoltLab Enterprise only.

Configuration file equivalent [placement_constraints](./configuration-file.md#doltlabenvoy-placement-constraints).

## doltlabenvoy-placement-preferences-spread

_String_. The placement preferences spread to add to the doltlabenvoy service. Can be supplied multiple times. DoltLab Enterprise only.

Configuration file equivalent [placement_preferences_spread](./configuration-file.md#doltlabenvoy-placement-preferences-spread).

## doltlabenvoy-replicas

_Number_. Specifies the number of doltlabenvoy service replicas to run. DoltLab Enterprise only.

Configuration file equivalent [replicas](./configuration-file.md#doltlabenvoy-replicas).

## doltlabfileserviceapi-uploads-volume-host-path

_String_. The path to an existing directory on the DoltLab host for persisting the 'doltlab-user-uploads' Docker volume.

Configuration file equivalent [uploads_volume_path](./configuration-file.md#uploads_volume_path).

## doltlabfileserviceapi-placement-constraint

_String_. The placement constraint to add to the doltlabfileserviceapi service. Can be supplied multiple times. By default, DoltLab will add the `node.labels.doltlabfileserviceapi == true` constraint to a multihost deployment. DoltLab Enterprise only.

Configuration file equivalent [placement_constraints](./configuration-file.md#doltlabfileserviceapi-placement-constraints).

## doltlabfileserviceapi-placement-preferences-spread

_String_. The placement preferences spread to add to the doltlabfileserviceapi service. Can be supplied multiple times. DoltLab Enterprise only.

Configuration file equivalent [placement_preferences_spread](./configuration-file.md#doltlabfileserviceapi-placement-preferences-spread).

## doltlabfileserviceapi-replicas

_Number_. Specifies the number of doltlabfileserviceapi service replicas to run. NOTE: only a single replica of `doltlabfileserviceapi` is currently supported. Use cloud-backed storage to remove this scaling limitation. DoltLab Enterprise only.

Configuration file equivalent [replicas](./configuration-file.md#doltlabfileserviceapi-replicas).

## doltlabgraphql-placement-constraint

_String_. The placement constraint to add to the doltlabgraphql service. Can be supplied multiple times. By default, DoltLab will add the `node.labels.doltlabgraphql == true` constraint to a multihost deployment. DoltLab Enterprise only.

Configuration file equivalent [placement_constraints](./configuration-file.md#doltlabgraphql-placement-constraints).

## doltlabgraphql-placement-preferences-spread

_String_. The placement preferences spread to add to the doltlabgraphql service. Can be supplied multiple times. DoltLab Enterprise only.

Configuration file equivalent [placement_preferences_spread](./configuration-file.md#doltlabgraphql-placement-preferences-spread).

## doltlabgraphql-replicas

_Number_. Specifies the number of doltlabgraphql service replicas to run. DoltLab Enterprise only.

Configuration file equivalent [replicas](./configuration-file.md#doltlabgraphql-replicas).

## doltlabremoteapi-data-volume-host-path

_String_. The path to an existing directory on the DoltLab host used for persisting the 'doltlab-remote-storage' Docker volume.

Configuration file equivalent [data_volume_path](./configuration-file.md#doltlabremoteapi-data-volume-path).

## doltlabremoteapi-placement-constraint

_String_. The placement constraint to add to the doltlabremoteapi service. Can be supplied multiple times. By default, DoltLab will add the `node.labels.doltlabremoteapi == true` constraint to a multihost deployment. DoltLab Enterprise only. 

Configuration file equivalent [placement_constraints](./configuration-file.md#doltlabremoteapi-placement-constraints).

## doltlabremoteapi-placement-preferences-spread

_String_. The placement preferences spread to add to the doltlabremoteapi service. Can be supplied multiple times. DoltLab Enterprise only.

Configuration file equivalent [placement_preferences_spread](./configuration-file.md#doltlabremoteapi-placement-preferences-spread).

## doltlabremoteapi-replicas

_Number_. Specifies the number of doltlabremoteapi service replicas to run. NOTE: only a single replica of `doltlabremoteapi` is supported when cloud-backed storage is NOT configured. Use cloud-backed storage to remove this scaling limitation. DoltLab Enterprise only.

Configuration file equivalent [replicas](./configuration-file.md#doltlabremoteapi-replicas).

## doltlabremoteapi-storage-aws-bucket

_String_. The AWS S3 bucket used for storing remote data files. DoltLab Enterprise only.

Configuration file equivalent [aws_bucket](./configuration-file.md#doltlabremoteapi-aws-bucket).

## doltlabremoteapi-storage-aws-dynamodb-table

_String_. The AWS DynamoDb table name used for storing the manifest of remote databases. DoltLab Enterprise only.

Configuration file equivalent [aws_dynamodb_table](./configuration-file.md#aws_dynamodb_table).

## doltlabremoteapi-storage-aws-region

_String_. The AWS region where the DynamoDb table is located. DoltLab Enterprise only.

Configuration file equivalent [aws_region](./configuration-file.md#doltlabremoteapi-aws-region).

## doltlabui-placement-constraint

_String_. The placement constraint to add to the doltlabui service. Can be supplied multiple times. By default, DoltLab will add the `node.labels.doltlabui == true` constraint to a multihost deployment. DoltLab Enterprise only.

Configuration file equivalent [placement_constraints](./configuration-file.md#doltlabui-placement-constraints).

## doltlabui-placement-preferences-spread

_String_. The placement preferences spread to add to the doltlabui service. Can be supplied multiple times. DoltLab Enterprise only.

Configuration file equivalent [placement_preferences_spread](./configuration-file.md#doltlabui-placement-preferences-spread).

## doltlabui-replicas

_Number_. Specifies the number of doltlabui service replicas to run. DoltLab Enterprise only.

Configuration file equivalent [replicas](./configuration-file.md#doltlabui-replicas).

## enterprise-online-api-key

_String_. The online api key for DoltLab Enterprise.

Configuration file equivalent [online_api_key](./configuration-file.md#online_api_key).

## enterprise-online-license-key

_String_. The online license key for DoltLab Enterprise.

Configuration file equivalent [online_license_key](./configuration-file.md#online_license_key).

## enterprise-online-product-code

_String_. The online product code for DoltLab Enterprise.

Configuration file equivalent [online_product_code](./configuration-file.md#online_product_code).

## enterprise-online-shared-key

_String_. The online shared key for DoltLab Enterprise.

Configuration file equivalent [online_shared_key](./configuration-file.md#online_shared_key).

## enterprise-offline-api-key

_String_. The offline api key for DoltLab Enterprise.

Configuration file equivalent [offline_api_key](./configuration-file.md#offline_api_key).

## enterprise-offline-license-key

_String_. The offline license key for DoltLab Enterprise.

Configuration file equivalent [offline_license_key](./configuration-file.md#offline_license_key).

## enterprise-offline-product-code

_String_. The offline product code for DoltLab Enterprise.

Configuration file equivalent [offline_product_code](./configuration-file.md#offline_product_code).

## enterprise-offline-shared-key

_String_. The offline shared key for DoltLab Enterprise.

Configuration file equivalent [offline_shared_key](./configuration-file.md#offline_shared_key).

## enterprise-offline-license-file

_String_. The offline license file for DoltLab Enterprise.

Configuration file equivalent [offline_license_file](./configuration-file.md#offline_license_file).

## enterprise-offline-request-activation

_Boolean_. If true, will generate an activation file that must be provided to the DoltLab team.

Configuration file equivalent [request_offline_activation](./configuration-file.md#request_offline_activation).

## google-creds-file

_String_. Absolute path to a Google application credentials file, used for configuring automated `doltlabdb backups` to Google Cloud Storage, DoltLab Enterprise only.

Configuration file equivalent [google_credentials_file](./configuration-file.md#google_credentials_file).

## help

_Boolean_. Print `installer` usage information.

## host

_String_. The hostname or IP address of the host running DoltLab or one of its services.

Configuration file equivalent [host](./configuration-file.md#host).

## https

_Boolean_. If true, will set the url scheme of DoltLab to `https://`. DoltLab Enterprise only.

Configuration file equivalent [scheme](./configuration-file.md#scheme).

## job-concurrency-limit

_Number_. The limit of concurrent `running` Jobs.

Configuration file equivalent [concurrency_limit](./configuration-file.md#concurrency_limit).

## job-concurrency-loop-seconds

_Number_. The number of seconds to wait before attempting to schedule more `pending` Jobs.

Configuration file equivalent [concurrency_loop_seconds](./configuration-file.md#concurrency_loop_seconds).

## job-max-retries

_Number_. The number of times to retry `failed` Jobs.

Configuration file equivalent [max_retries](./configuration-file.md#max_retries).

## multihost-deployment

_Boolean_. If true, generates DoltLab Enterprise assets that will run via Docker Swarm. DoltLab Enterprise only.
 
Configuration file equivalent [multihost_deployment](./configuration-file.md#multihost_deployment).

## no-default-placement-constraints

_Boolean_. If true, will not add the default placment contraints to services when running in multihost deployment mode. DoltLab Enterprise only.

Configuration file equivalent [no_default_placement_contraints](./configuration-file.md#no_default_placement_contraints).

## no-default-placement-preferences-spreads

_Boolean_. If true, will not add the default placment preferences spread to services when running in multihost deployment mode. DoltLab Enterprise only.

Configuration file equivalent [no_default_placement_preferences_spreads](./configuration-file.md#no_default_placement_preferences_spreads).

## no-reply-email

_String_. The email address used as the "from" address in emails sent from DoltLab. DoltLab Enterprise only.

Configuration file equivalent [no_reply_email](./configuration-file.md#no_reply_email).

## oci-config-file

_String_. Absolute path to an Oracle Cloud config file, used for configuring automated doltlabdb backups to Oracle Cloud, DoltLab Enterprise only.

Configuration file equivalent [oci_config_file](./configuration-file.md#oci_config_file).

## oci-key-file

_String_. Absolute path to an Oracle Cloud key file, used for configuring automated doltlabdb backups to Oracle Cloud, DoltLab Enterprise only.

Configuration file equivalent [oci_key_file](./configuration-file.md#oci_key_file).

## smtp-auth-method

_String_. The authentication method of an SMTP server, one of `plain`, `login`, `anonymous`, `external`, `oauthbearer`, or `disable`. DoltLab Enterprise only.

Configuration file equivalent [auth_method](./configuration-file.md#auth_method).

## smtp-client-hostname

_String_. The client hostname of an SMTP server. DoltLab Enterprise only.

Configuration file equivalent [client_hostname](./configuration-file.md#client_hostname).

## smtp-host

_String_. The hostname of an SMTP server. DoltLab Enterprise only.

Configuration file equivalent [host](./configuration-file.md#smtp-host).

## smtp-identity

_String_. The identity of an SMTP server. DoltLab Enterprise only.

Configuration file equivalent [identity](./configuration-file.md#identity).

## smtp-implicit-tls

_Boolean_. If true, will use implicit TLS when DoltLab connects to the SMTP server. DoltLab Enterprise only.

Configuration file equivalent [implicit_tls](./configuration-file.md#implicit_tls).

## smtp-insecure-tls

_String_. If true, will skip TLS verification when DoltLab connects to the SMTP server. DoltLab Enterprise only.

Configuration file equivalent [insecure_tls](./configuration-file.md#insecure_tls).

## smtp-oauth-token

_String_. The Oauth token used for authenticating against an SMTP server. DoltLab Enterprise only.

Configuration file equivalent [oauth_token](./configuration-file.md#oauth_token).

## smtp-password

_String_. The password used for authenticating against an SMTP server. DoltLab Enterprise only.

Configuration file equivalent [password](./configuration-file.md#smtp-password).

## smtp-port

_Number_. The port of an SMTP server. DoltLab Enterprise only.

Configuration file equivalent [port](./configuration-file.md#smtp-port).

## smtp-trace

_String_. The trace of an SMTP server. DoltLab Enterprise only.

Configuration file equivalent [trace](./configuration-file.md#trace).

## smtp-username

_String_. The username used for authenticating against an SMTP server. DoltLab Enterprise only.

Configuration file equivalent [username](./configuration-file.md#username).

## sso-saml-cert-common-name

_String_. The common name used for generating the SAML signing certificate, DoltLab Enterprise only.

Configuration file equivalent [cert_common_name](./configuration-file.md#cert_common_name).

## sso-saml-metadata-descriptor

_String_. Absolute path to the SAML metadata descriptor file from an identity provider, DoltLab Enterprise only.

Configuration file equivalent [metadata_descriptor_file](./configuration-file.md#metadata_descriptor_file).

## sso-oidc-issuer-url 

_String_. The URL of the OIDC identity provider, DoltLab Enterprise only.

Configuration file equivalent [issuer_url](./configuration-file.md#issuer_url).

## sso-oidc-client-id

_String_. The OIDC client id, DoltLab Enterprise only.

Configuration file equivalent [client_id](./configuration-file.md#client_id).

## sso-oidc-client-secret

_String_. The OIDC client secret, DoltLab Enterprise only.

Configuration file equivalent [client_secret](./configuration-file.md#client_secret).

## super-admin-email

_String_. The email address of a DoltLab user granted "super admin" privileges. Can be supplied multiple times. DoltLab Enterprise only.

Configuration file equivalent [super_admins](./configuration-file.md#super_admins).

## tls-cert-chain

_String_. Deprecated, use `tls-full-chain-cert` instead. Absolute path to a TLS full chain certificate with `.pem` extension. DoltLab Enterprise only.

Configuration file equivalent [cert_chain](./configuration-file.md#cert_chain).

## tls-full-chain-cert

_String_. Absolute path to a TLS full chain certificate with `.pem` extension. DoltLab Enterprise only.

Configuration file equivalent [full_chain_cert](./configuration-file.md#full_chain_cert).

## tls-private-key

_String_. Absolute path to TLS private key with `.pem` extension. DoltLab Enterprise only.

Configuration file equivalent [private_key](./configuration-file.md#private_key).

## ubuntu

_Boolean_. If true will generate a script to install DoltLab's dependencies on Ubuntu.

## upgrade

_Boolean_. If true will upgrade DoltLab to the latest version. DoltLab Enterprise only.

## use-env

_Boolean_. If true, sensitive values will not be written to generated assets and environment variables will be expected instead.

Configuration file equivalent [use_env](./configuration-file.md#use_env).

## whitelist-all-users

_Boolean_. If true, allows all users create accounts on a DoltLab instance, (default true).

Configuration file equivalent [whitelist_all_users](./configuration-file.md#whitelist_all_users).
