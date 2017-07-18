## Test applications
Simply import any of these tests into your workspace and launch them. See below for the threshold objects to add to trigger the alerts for the test applications.

### MemoryLeak
This application simulates a memory leak, when launched. In other words, its memory consumption is increasing 100% of the time. If left running for too long, a `java.lang.OutOfMemoryError: Java heap space` error will get thrown.

Add the following to your thresholdDocument.json to detect when the increasePercentage of the *nResidentMemoryConsumption* metric goes above 80%:
```javascript
{
  "metricName" : "nResidentMemoryConsumption",
  "thresholds" :
  {
    "increasePercentage" : ">=80%,10000",
  },
  "filters" :
  {
    "jobName" : "com.ibm.streamsx.metricsMonitor.MemoryLeak.*",
  },
},
```

### LowTupleRate
This application simulates a sudden drop in tuple flow, when launched. Tuples will flow for 20 seconds, then suddenly stop.

Add the following to your thresholdDocument.json to detect when the rate of the *nTuplesProcessed* metric goes below 1:
```javascript
{
  "metricName" : "nTuplesProcessed",
  "thresholds" :
  {
    "rate" : "<=10,20000",
  },
  "filters" :
  {
    "jobName" : "com.ibm.streamsx.metricsMonitor.LowTupleRate.*",
  },
},
```

### HighCongestion
This application simulates high congestion, when launched. Make sure to launch in with Legacy fusion scheme, as congestionFactor is a PE connection metric. Legacy fusion scheme will ensure that this test app puts all operators in their own PEs.

Add the following to your thresholdDocument.json to detect when the value of the *congestionFactor* metric goes above 90:
```javascript
{
  "metricName" : "congestionFactor",
  "thresholds" :
  {
    "value" : ">90",
    "rollingAverage" : ">=80,20000",
  },
  "filters" :
  {
    "jobName" : "com.ibm.streamsx.metricsMonitor.HighCongestion.*",
  },
},
```

### CustomMetrics
This application provides sample code to demonstrates how to define custom metrics (with SPL and Java).

It contains a **Beacon_Op** that outputs random numbers (between 0-100) to:
- **SPLCustomMetricsSink**
  - Custom SPL Sink. View *Main.spl* to see how to define custom metrics using the `createCustomMetrics()` and `setCustomMetricValue()` functions.
- **JavaCustomMetricsSink** :
  - Java Primitive Operator. View *impl/java/src/JavaCustomMetricsSink.java* to see how to define custom metrics using functions from the Java Operator API (more information in *Useful References* section below).
  
The two sinks output *SPLDefinedMetric* and *JavaDefinedMetric*, respectively. Add the following to your thresholdDocument.json to monitor for when either goes above 80:
```javascript
{
  "metricName" : "SPLDefinedMetric",
  "thresholds" :
  {
    "value" : ">=80",
  },
  "filters" :
  {
    "jobName" : "com.ibm.streamsx.metricsMonitor.CustomMetrics.*",
  },
},
{
  "metricName" : "JavaDefinedMetric",
  "thresholds" :
  {
    "value" : ">=80",
  },
  "filters" :
  {
    "jobName" : "com.ibm.streamsx.metricsMonitor.CustomMetrics.*",
  },
},
```
