# Docker Logging with Vector, Loki and Grafana

This is an example setup on how to collect Docker logs in Loki using Vector. They can then be explored using Grafana.

The goal of this is to provide a basic setup that allows to have all logs in a homelab in one place. 
It can be easily extended by creating other Vector sources for different services on your homelab and process or enrich the logs before writing them to Loki.

## Components

### Docker

The Docker [syslog logging driver](https://docs.docker.com/config/containers/logging/syslog/) is being utilized to write logs to a udp syslog endpoint. A tag is given that allows filtering for the different containers later.

### Vector

[Vector](https://vector.dev) is used to collect the logs and write them to Loki in this example. In more complex cases, it can also transform or enrichs them. It also writes its own logs into Loki.

### Loki

[Loki](https://grafana.com/oss/loki/) is used as a storage and query engine for the logs. In this configuration it uses the local filesystem to store the data without replication. Statistics reporting back to Grafana Labs is disabled.

### Grafana

[Grafana](https://grafana.com/grafana/) can be used to explore the logs and to create dashboards. Loki as a datasource is provisioned at startup and logs should directly appear in the Explore view. Initial credentials are `admin:admin`. The frontend can be reached under `localhost:3000`.

## What to do next

This is a very basic setup that can and should be extended when used in a homelab context. Especially the config of Loki should be tailored to the specific needs of the respective environment. Limits and compaction should be configured according to those needs. 