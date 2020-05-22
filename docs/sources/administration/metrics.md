+++
title = "Internal ThingSPIN metrics"
description = "Internal metrics exposed by ThingSPIN"
keywords = ["grafana", "metrics", "internal metrics"]
type = "docs"
[menu.docs]
parent = "admin"
weight = 8
+++

# Internal ThingSPIN metrics

ThingSPIN collects some metrics about itself internally. ThingSPIN supports pushing metrics to Graphite or exposing them to be scraped by Prometheus.

For more information about configuration options related to ThingSPIN metrics, refer to [metrics]({{< relref "../installation/configuration/#metrics" >}}) and [metrics.graphite]({{< relref "../installation/configuration/#metrics-graphite" >}}) in [Configuration]({{< relref "../installation/configuration.md" >}}).

## Available metrics

When enabled, ThingSPIN exposes a number of metrics, including:

* Active ThingSPIN instances
* Number of dashboards, users, and playlists
* HTTP status codes
* Requests by routing group
* ThingSPIN active alerts
* ThingSPIN performance

## Pull metrics from ThingSPIN into Prometheus

These instructions assume you have already added Prometheus as a data source in ThingSPIN.

1. Enable Prometheus to scrape metrics from ThingSPIN. In your configuration file (`grafana.ini` or `custom.ini` depending on your operating system) remove the semicolon to enable the following configuration options: 

   ```
   # Metrics available at HTTP API Url /metrics
   [metrics]
   # Disable / Enable internal metrics
   enabled           = true

   # Disable total stats (stat_totals_*) metrics to be generated
   disable_total_stats = false
   ```

1. (optional) If you want to require authorization to view the metrics endpoint, then uncomment and set the following options:

   ```
   basic_auth_username =
   basic_auth_password =
   ```

1. Restart ThingSPIN. ThingSPIN now exposes metrics at http://localhost:3000/metrics.
1. Add the job to your prometheus.yml file.
   Example:

   ```
   - job_name: 'grafana_metrics'

      scrape_interval: 15s
      scrape_timeout: 5s
  
      static_configs:
        - targets: ['localhost:3000']
   ```
1. Restart Prometheus. Your new job should appear on the Targets tab.
1. In ThingSPIN, hover your mouse over the **Configuration** (gear) icon on the left sidebar and then click **Data Sources**.
1. Select the **Prometheus** data source.
1. On the Dashboards tab, **Import** the ThingSPIN metrics dashboard. All scraped ThingSPIN metrics are available in the dashboard.

## View ThingSPIN metrics in Graphite

These instructions assume you have already added Graphite as a data source in ThingSPIN.

1. Enable sending metrics to Graphite. In your configuration file (`grafana.ini` or `custom.ini` depending on your operating system) remove the semicolon to enable the following configuration options: 

   ```
   # Metrics available at HTTP API Url /metrics
   [metrics]
   # Disable / Enable internal metrics
   enabled           = true

   # Disable total stats (stat_totals_*) metrics to be generated
   disable_total_stats = false
   ```

1. Enable [metrics.graphite] options:
   ```
   # Send internal metrics to Graphite
   [metrics.graphite]
   # Enable by setting the address setting (ex localhost:2003)
   address = <hostname or ip>:<port#>
   prefix = prod.grafana.%(instance_name)s.
   ```

1. Restart ThingSPIN. ThingSPIN now exposes metrics at http://localhost:3000/metrics and sends them to the Graphite location you specified.
