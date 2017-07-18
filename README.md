# streamsx.metricsmonitor.starterkit
Get started monitoring streams application metrics and send alerts to Slack when threshold rules are reached.

<img src="http://i.imgur.com/QB6ByJ3.png" width="90%">

## Overview
Metrics are a convenient way to output information about your Streams application, whether it be about the flow/congestion of your application or a memory leak that you want to catch. You can view the metrics change, in real-time, with the Metrics view in IBM Streams Studio.

This starter kit aims to provide an easy way for users to get started monitoring their application's metrics and get alerted when anything unexpected happens. This is achieved by using the provided metrics monitoring application.



## Get Started
To launch the metrics monitor starter application:
1. `git clone https://github.com/IBMStreams/streamsx.metricsmonitor.starterkit.git`.
2. `cd streamsx.metricsmonitor.starterkit`
3. `gradle build`
4. Set up application configuration. See **Application Configuration Parameters** below.
4. `gradle execute`



## Application Configuration Parameters
Ensure that the 6 parameters below are defined before launching the metrics monitor starter application.

### [MetricsIngestService Parameters](https://github.com/IBMStreams/streamsx.metrics)
#### Retrieves metrics (built-in and user-defined) and outputs these as tuples.

- `filterDocument` : JSON string describing which domains/instances/PEs/etc. to monitor. Look at the application project's `data/filterDocument.json` for a sample that monitors this starter kit's test applications.
- `connectionURL` : The JMX URL to retrieve metrics from.
- `user` : Username used to connect to the JMX service.
- `password` : Password used to connect to the JMX service.

### [MetricsMonitorService Parameters](https://github.com/nelsonong/streamsx.metricsmonitor.starterkit)
#### Evaluates incoming metric tuples against thresholdDocument rules and outputs an alert tuple if any rules are violated.

- `thresholdDocument` : JSON string defining the thresholds for incoming metrics. By default, there are no thresholds. Refer to this [guide](https://github.com/nelsonong/streamsx.metricsmonitor.starterkit/tree/master/com.ibm.streamsx.metricsmonitor) to set up your thresholds.
### [SlackService Parameters](https://github.com/IBMStreams/streamsx.slack)
#### Sends incoming tuple messages to a Slack channel.

- `slackUrl` : Slack WebHook URL to send messages to. Create a Slack WebHook URL here: [Incoming WebHooks](https://slack.com/apps/A0F7XDUAZ-incoming-webhooks).



## Test Applications
In the `simulate` folder includes 4 test applications that each simulate a practical use case for monitoring metrics. Read the README in the `simulate` folder for more information.



## Useful References

### Built-in metrics
IBM Streams already has some built-in metrics that it outputs by default (eg. nTuplesProcessed, nMemoryConsumption, nTupleBytesTransmitted, etc.). Find a full list of built-in metrics below.
- [List of built-in metrics](https://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.1/com.ibm.streams.dev.doc/doc/metricaccess.html)

### Custom metrics
Additionally, you can define your own custom metrics, either using SPL or Java. The **com.ibm.streamsx.metricsMonitor.CustomMetrics** demonstrates how to define metrics in both ways.
- [Defining metrics with SPL](https://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.1/com.ibm.streams.dev.doc/doc/metricaccess.html)
- [Defining metrics with Java](http://ibmstreams.github.io/streamsx.documentation//docs/4.1/java/java-op-dev-guide/#defining-custom-metrics)
