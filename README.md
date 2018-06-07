# docker-se-influxdb

*[InfluxDB](https://www.influxdata.com/) is a data store for any use case involving large amounts of timestamped data,*
*including DevOps monitoring, application metrics, IoT sensor data, and real-time analytics.*
 
No SE specific Docker Image is defined nor required here. 
This repo is a placeholder for documentation
and a guide to environment settings.

In addition to general configuration in `influxdb.conf`,
database creation and defining users & roles can also be effected via `INFLUX_*` environment
variables when using the official [InfluxDB Docker image](https://hub.docker.com/_/influxdb/). 
A restriction is that only one InfluxDB Database can be defined per instance/container.
This is not a problem at the moment. For now two instances of InfluxDB thus databases 
are run:

* `smartemission` : used internally for Calibration (raw inputs, RIVM refdata and results)
* `airsenseur`: used for the external SE Data Collector (where AirSensEUR sensor stations push their data) 

## Hosting

The Docker Image is hosted [at DockerHub](https://hub.docker.com/_/influxdb/).
The GitHub for this image is https://github.com/influxdata/influxdata-docker/tree/master/influxdb.

## Environment

There are many env vars [defined in the documentation](https://docs.influxdata.com/influxdb/v1.5/administration/config). 
Most have sensible defaults. Database and credentials can only be defined when using the
InfluxDB Docker image. These env vars are listed below. 
 
These need to be set, either via `docker-compose` or Kubernetes.
The variable `INFLUXDB_DATA_INDEX_VERSION` will need to 
be set to `tsi1` to enable [Time Series Indexing (TSI)](https://docs.influxdata.com/influxdb/v1.5/concepts/time-series-index/).


Variable|Meaning |Example
---|---|--- 
`INFLUXDB_DATA_INDEX_VERSION`|indexing method to be used, default `inmem` but `tsi1` (TSI) recommended|`tsi1`
`INFLUXDB_DB`|name of database to create|airsenseur
`INFLUXDB_HTTP_AUTH_ENABLED`|Enables authentication|true
`INFLUXDB_ADMIN_USER`|name of the admin user to be created|admin
`INFLUXDB_ADMIN_PASSWORD`|password for the admin user configured with `INFLUXDB_ADMIN_USER`|secret
`INFLUXDB_USER`|If `INFLUXDB_DB` is set, this user will be granted r/w permissions there|secret
`INFLUXDB_USER_PASSWORD`|password for the user configured with `INFLUXDB_USER`|secret
`INFLUXDB_READ_USER`|user to be created with read privileges on `INFLUXDB_DB`|secret
`INFLUXDB_READ_USER_PASSWORD`|password for the user configured with `INFLUXDB_READ_USER`|secret
`INFLUXDB_WRITE_USER`|user to be created with write privileges on `INFLUXDB_DB`|secret
`INFLUXDB_WRITE_USER_PASSWORD`|password for the user configured with `INFLUXDB_WRITE_USER`|secret


## Architecture

The official [InfluxDB Docker image](https://hub.docker.com/_/influxdb/) Image is directly used.

## Links

* [InfluxDB Docker image](https://hub.docker.com/_/influxdb/) 
* SE Platform doc: http://smartplatform.readthedocs.io/en/latest/

