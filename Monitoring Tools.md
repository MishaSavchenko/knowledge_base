
 [Logz.io article for open source monitoring tools](https://logz.io/blog/open-source-monitoring-tools/)
 
 * Short List: 
	 * syslog-ng
		 * seen it before in the aether
		 * free / open-source
	 * Grafana
		 * supports a whole bunch of data sources
		 * currently doesnt support log analysis but they are working on it 
	 * Prometheus
		 * core server scrapes and stores metrics
		 * bunch of client libraries 
		 * multi-dimensional data model 
		 * metrics are pulled over HTTP instead of push into the system\
		 * designed for high performance
	 * OpenTelemetry
		 * specifically for capturing telemetry from cloud-native apps 
		 * "collect trace and metric data"
		 * seems to be very cloud oriented
	 * Graphite
		 * three components for collecting, storing, and visualizing metrics 
		 * require careful planning around i/o, cpu, disk capacity 
	 * InfluxDB
		 * multi dimensional with key value pairs
		 * high performance 
		 * sql-like querying language
	 * Fleuntd
		 * open source log collector processor and aggregator
		 * good performance 
		 * de-facto standard log aggregator 
	 * Jaeger
		 * distributed tracing tool
		 * root cause analysis 
		 * OpenTracing-based instrumentation
	 * ELK
		 * no longer open source 






## Follow ups 

> For logs, this heavy lifting is performed by log forwarders, aggregators and shippers.

* Seems like i havent considered that you forward the logs into a different format *
> adoption of microservices, distributed tracing has emerged as a monitoring and troubleshooting best practice.

*  distributed tracing :surprise_pikachu: 





---
[[ROS 2 Logging]]