# Performance Testing Project with JMeter + PerfMon

This repository showcases a performance testing study conducted using **Apache JMeter** for load generation and the **PerfMon Metrics Collector** plugin for comprehensive server-side monitoring.

---

## 🧱 Project Overview

This project focuses on simulating user load on a target application (in this case, Google Search) and analyzing both client-side response times and server-side resource utilization.

### Test Plan - Google

The core of the project is the JMeter Test Plan, structured to simulate realistic user behavior. It includes:

*   **Thread Groups**: To define different user types or scenarios (e.g., "Google Navigation" and "Google Search").
*   **HTTP Requests**: To send requests to the target application.
*   **Listeners**: To visualize and analyze test results.

Below is a snapshot of the JMeter Test Plan structure and the "View Results Tree" listener, showing successful HTTP requests for a search query (e.g., "pizza").

![JMeter View Results Tree - Google Search](jmeter%20google%202.png)

---

## 🎯 Key Components and Analysis

### Client-Side Analysis: View Results Tree

The "View Results Tree" listener in JMeter provides a detailed view of individual requests, including their status, response data, and request headers. This helps in verifying the correctness of the requests and responses during the test execution.

### Server-Side Monitoring: PerfMon Metrics Collector

To understand the impact of the load on the server, the PerfMon Metrics Collector plugin was used. This plugin allows for real-time monitoring of server resources such as CPU, Memory, and Disk I/O.

The following metrics were collected from the `localhost` server on port `4444`:

*   **CPU Utilization**
*   **Memory Usage**
*   **Disks I/O**

The graph below illustrates the collected server metrics over time. Notice the stability of memory and CPU, with a distinct spike in Disks I/O, indicating specific disk-intensive operations during the test.

![PerfMon Metrics Collector Graph](response%20timegraph.png)

---

## 💡 Insights and Best Practices

*   **Correlation**: The ability to correlate client-side response times (from JMeter listeners) with server-side resource usage (from PerfMon) is crucial for identifying performance bottlenecks.
*   **Resource Utilization**: Monitoring CPU, Memory, and Disk I/O helps in understanding if the server infrastructure can handle the simulated load.
*   **Identifying Spikes**: Unexpected spikes in resource usage (like the Disks I/O spike observed) can point to specific application behaviors or database interactions that require further investigation and optimization.

---

## 🚀 Running the Tests

To run this performance test project, you will need **Apache JMeter** and the **PerfMon Metrics Collector** plugin installed.

> **⚠️ Important:** You must keep **two separate terminal sessions (bash)** open: one for the ServerAgent and another for running JMeter.

### 1. Start the ServerAgent

Before running the tests, you must start the **ServerAgent** on the target server (or your local machine if testing locally) to collect performance metrics.

```bash
# Navigate to your ServerAgent directory
cd path/to/ServerAgent-2.2.3/

# Start the PerfMon Agent
java -jar ./CMDRunner.jar --tool PerfMonAgent
```

### 2. Run JMeter

You can run the test plan using the JMeter GUI for editing or in non-GUI mode for the actual load test execution.

**GUI Mode (Windows):**
```bash
# Navigate to your JMeter bin directory
cd path/to/apache-jmeter-5.6.3/bin

# Start JMeter
./jmeter.bat
```

**Non-GUI Mode (Recommended for Load Tests):**
```bash
# Run the test and save results to a .jtl file
./jmeter.bat -n -t ../path/to/your/testplan.jmx -l ../path/to/results.jtl
```

---

## 🔧 Tools Used

*   **Apache JMeter**: Open-source load testing tool.
*   **JMeter PerfMon Metrics Collector**: Plugin for server-side resource monitoring.
*   **Java**: Required for running JMeter.

---

## 📌 Notes

*   The test plan (`testplan.jmx`) would contain the detailed configuration for thread groups, samplers, and listeners.
*   The PerfMon Server Agent must be running on the server being monitored for data collection.
*   Analyzing the `.jtl` results file (generated in non-GUI mode) with JMeter's built-in listeners or external tools provides comprehensive performance reports.
