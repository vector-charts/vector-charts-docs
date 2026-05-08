---
title: "Configuration"
menu:
  oem:
    title: "Configuration"
    parent: "getting_started"
    weight: 4
---

The OEM software is configured primarily via environment variables set when running the Docker container. There are a number of configuration parameters

## Configuration Options

- *Options marked as Required must be set for the OEM server to function.*
- *Options marked as Provisioning only apply as defaults on the first startup.*


|Environment Variable|Description|Default Value|Required?|Provisioning?|
|--------------------|-----------|-------------|---------|-------------|
|`INITIAL_ADMIN_USERNAME`|The default admin username.|`admin`|`N`|`Y`|
|`INITIAL_ADMIN_PASSWORD`|The default admin password.|`admin`|`N`|`Y`|
|`LICENSING_ORGANIZATION_ID`|A unique identifier for your organization, provided by the Vector Charts team.|N/A|`Y`|`N`|
|`LICENSING_SERVER_NAME`|A unique name for this server. If none is set, a random name is generated.|`<random>`|`N`|`Y`|
|`LICENSING_KEY`|A hardcoded licensing key. Optional; if no key is set, the OEM API will reach out to Vector Charts licensing servers and acquire a license.|`N`|`N`|
|`PROVISIONING_DEFAULT_TOKEN`|A default token to be added to the database. Can be used to automated headless deployments. Must be a UUID with no dashes.|N/A|`N`|`Y`|
|DEPLOYMENT_SCALE_NUM_API_INSTANCES|The number of API instances. A higher number supports more parallel API requests but does not necessarily speed up individual API requests. Can typically be left unset.|`4`|`N`|`N`|
|JOB_PROCESSOR_MAX_WORKER_COUNT|The number of worker threads used when processing chart data. Should typically be set to be less than or equal to the number of cores on the host.|`<number of processor cores>|`N`|`N`|
|JOB_PROCESSOR_ENABLE_AUTO_CHART_UPDATE|If true, new NOAA charts are downloaded weekly.|`true`|`N`|`N`|
|SUPPORT_REMOTE_ACCESS|If `true`, remote VPN access is available into the container for Zydro staff.|`false`|`N`|`N`|