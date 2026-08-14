---
title: "Configuration"
menu:
  oem:
    title: "Configuration"
    parent: "getting_started"
    weight: 4
---

The OEM software is configured primarily via environment variables set when running the Docker container.

## Configuration Options

- *Options marked as Required must be set for the OEM server to function.*
- *Options marked as Provisioning only apply as defaults on the first startup.*


|Environment Variable|Description|Default Value|Required?|Provisioning?|
|--------------------|-----------|-------------|---------|-------------|
|`INITIAL_ADMIN_USERNAME`|The default admin username.|`admin`|`N`|`Y`|
|`INITIAL_ADMIN_PASSWORD`|The default admin password.|`admin`|`N`|`Y`|
|`LICENSING_ORGANIZATION_ID`|A unique identifier for your organization, provided by the Vector Charts team.|N/A|`Y`|`N`|
|`LICENSING_SERVER_NAME`|A unique name for this server. If none is set, a random name is generated.|`<random>`|`N`|`Y`|
|`LICENSING_KEY`|A hardcoded licensing key. Optional; if no key is set, the OEM API will reach out to Vector Charts licensing servers and acquire a license.|N/A|`N`|`N`|
|`PROVISIONING_DEFAULT_TOKEN`|A default token to be added to the database. Can be used to automated headless deployments. Must be a UUID with no dashes.|N/A|`N`|`Y`|
|`DEPLOYMENT_SCALE_NUM_API_INSTANCES`|The number of API instances. A higher number supports more parallel API requests but does not necessarily speed up individual API requests. Can typically be left unset.|`4`|`N`|`N`|
|`JOB_PROCESSOR_MAX_WORKER_COUNT`|The number of worker threads used when processing chart data. Can typically be left unset.|`<number of processor cores>`|`N`|`N`|
|`JOB_PROCESSOR_ENABLE_AUTO_CHART_UPDATE`|If true, new NOAA charts are downloaded on provisioning and weekly.|`false`|`N`|`N`|
|`SUPPORT_REMOTE_ACCESS`|If `true`, remote VPN access is available into the container for Zydro staff.|`false`|`N`|`N`|
|`POSTGRES_SHARED_BUFFERS`|Sets the Postgres `shared_buffers` value. If you do not set this, the software calculates a default from the container memory.|Calculated: 12–20% of container memory, maximum 1GB|`N`|`N`|
|`POSTGRES_WORK_MEM`|Sets the Postgres `work_mem` value. This value applies to each sort or hash operation.|Calculated: `8MB` if memory is less than 4GB; `16MB` if memory is 4–8GB; `32MB` if memory is 8GB or more|`N`|`N`|
|`POSTGRES_MAINTENANCE_WORK_MEM`|Sets the Postgres `maintenance_work_mem` value.|Calculated: 5% of container memory, minimum 64MB, maximum 256MB|`N`|`N`|
|`POSTGRES_AUTOVACUUM_WORK_MEM`|Sets the Postgres `autovacuum_work_mem` value.|`64MB`|`N`|`N`|
|`POSTGRES_EFFECTIVE_CACHE_SIZE`|Gives a memory estimate to the Postgres planner. This setting does not allocate memory.|40% of container memory|`N`|`N`|
|`POSTGRES_RANDOM_PAGE_COST`|Sets the planner cost for a non-sequential page read. Use `1.1` for flash storage.|`1.1`|`N`|`N`|
|`POSTGRES_JIT`|Controls LLVM JIT for query execution.|`off`|`N`|`N`|
|`POSTGRES_EFFECTIVE_IO_CONCURRENCY`|Gives a concurrent disk I/O estimate to the Postgres planner.|`200`|`N`|`N`|
|`POSTGRES_MAX_PARALLEL_WORKERS_PER_GATHER`|Sets the maximum number of parallel workers for one gather operation.|`1` if memory is less than 4GB; otherwise `2`|`N`|`N`|
|`POSTGRES_MAX_PARALLEL_WORKERS`|Sets the maximum number of parallel workers for the database.|`2`|`N`|`N`|
|`POSTGRES_MAX_PARALLEL_MAINTENANCE_WORKERS`|Sets the maximum number of parallel workers for maintenance commands.|`1`|`N`|`N`|
|`POSTGRES_DYNAMIC_SHARED_MEMORY_TYPE`|Sets the location of shared memory for parallel queries. The value `mmap` does not use Docker `/dev/shm`.|`mmap`|`N`|`N`|

## PostgreSQL Tuning

Vector Charts runs an internal PostgreSQL database. The default settings give good performance on most devices. You may need to change these settings to get the best performance on your hardware.

When the container starts, the software sets PostgreSQL memory values from the container memory limit. The minimum calculation uses a device with 2GB of memory.

Use a `POSTGRES_*` variable from the table above only when you must set a fixed value.

We recommend that you start the container with `--shm-size=256m`. In Docker Compose, use `shm_size: 256m`.

This setting is not necessary for correct operation. Parallel queries use `mmap` in the data directory by default. The setting only prevents `/dev/shm` from staying at the Docker default of 64MB.
