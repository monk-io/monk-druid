# Apache Druid & Monk
This repository contains Monk.io template to deploy Apache Druid either locally or on cloud of your choice (AWS, GCP, Azure, Digital Ocean).

# Prerequisites
- [Install Monk](https://docs.monk.io/docs/get-monk)
- [Register and Login Monk](https://docs.monk.io/docs/acc-and-auth)
- [Add Cloud Provider](https://docs.monk.io/docs/cloud-provider)
- [Add Instance](https://docs.monk.io/docs/multi-cloud)

#### Make sure monkd is running
```bash
foo@bar:~$ monk status
daemon: ready
auth: logged in
not connected to cluster
```

## Clone Repository
```bash
git clone https://github.com/monk-io/druid
```

## Load Template
```bash
cd druid
monk load MANIFEST
```


#### Let's take a look at the themes I have installed.
```bash
foo@bar:~$ monk list druid
✔ Got the list
Type      Template          Repository  Version  Tags
runnable  druid/broker         local       -        -
runnable  druid/coordinator    local       -        -
runnable  druid/db             local       -        -
runnable  druid/dzookeeper     local       -        -
runnable  druid/historical     local       -        -
runnable  druid/middlemanager  local       -        -
runnable  druid/router         local       -        -
group     druid/stack          local       -        -

```

## Deploy Stack
```bash
foo@bar:~$ monk run druid/stack
```

## Variables
The variables are in `stack.yml` file. You can quickly setup by editing the values here.

| Variable                            | Description                     | Default                                                                                                                                                                              |
|-------------------------------------|---------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| image_tag                           | Docker image tag                | v2.00.9                                                                                                                                                                              |
| java_xmx                            | The maximum heap size.          | 1024m                                                                                                                                                                                |
| java_xms                            | The initial heap size.          | 1024m                                                                                                                                                                                |
| java_max_new_size                   | Java max new size               | 256m                                                                                                                                                                                 |
| java_max_direct_memory              | set Java max direct memory size | 512m                                                                                                                                                                                 |
| single_node                         | Single node configuration       | micro-quickstart                                                                                                                                                                     |
| log_level                           | Log level                       | debug                                                                                                                                                                                |
| extensions                          | Druid extensions                | ["druid-histogram", "druid-datasketches", "druid-lookups-cached-global", "postgresql-metadata-storage", "druid-multi-stage-query"]                                                   |
| zookeeper_host                      | Zookeeper host                  |                                                                                                                                                                                      |
| metadata_storage_type               | Metadata storage type.          | postgresql                                                                                                                                                                           |
| metadata_storage_connector_password | Metadata storage password       | monk                                                                                                                                                                                 |
| metadata_storage_connector_user     | Metadata storage user           | monk                                                                                                                                                                                 |
| postgres_host                       | Postgresql host                 | 1024m                                                                                                                                                                                |
| droid_storage_type                  | Storage type                    | local                                                                                                                                                                                |
| droid_storage_directory             | Storage directory               | /opt/shared                                                                                                                                                                          |
| druid_processing_num                | Thread number                   | 2                                                                                                                                                                                    |
| druid_processing_num_merge          | Number of merge buffers         | 2                                                                                                                                                                                    |
| druid_processing_buffer             | Merge buffer size               | 56m                                                                                                                                                                                  |
| coordinator_balance                 | Coordinator balance strategy    | cachingCost                                                                                                                                                                          |
| indexer                             | Indexer java options            | ["-server", "-Xmx1g", "-Xms1g", "-XX:MaxDirectMemorySize=3g", "-Duser.timezone=UTC", "-Dfile.encoding=UTF-8", "-Djava.util.logging.manager=org.apache.logging.log4j.jul.LogManager"] |
| log4j                               | log4j configurations            | `<?xml version="1.0" encoding="UTF-8" ?><Configuration status="WARN"><Appenders><Console name="Console" target="SYSTEM_OUT"><PatternLayout pattern="%d{ISO8601} %p [%t] %c - %m%n"/></Console></Appenders><Loggers><Root level="info"><AppenderRef ref="Console"/></Root><Logger name="org.apache.druid.jetty.RequestLog" additivity="false" level="DEBUG"><AppenderRef ref="Console"/></Logger></Loggers></Configuration>`    |


## Stop, remove and clean up workloads and templates

```bash
monk purge -a
```

