# Queues Management Application

### Simulate arrivals. Balance queues. Explore concurrent processing.

A Java desktop application for simulating clients distributed across multiple service queues. Each queue runs on its own worker thread, while a configurable scheduling strategy decides where arriving clients are assigned.

**Java 25 · Swing · Multithreading · Concurrent Collections · Strategy Pattern**

---

## Overview

The application generates clients with random arrival and service times, routes them to parallel service queues, and displays the simulation as it progresses. It records queue snapshots in a log file and reports average waiting time, average service time, and the busiest simulation moment.

The project brings together thread-based processing, concurrent data structures, atomic counters, and a Swing interface to illustrate queue management under different scheduling policies.

## Features

| Feature | Description |
| --- | --- |
| Configurable simulation | Set the client count, queue count, duration, and arrival and service time ranges. |
| Random client generation | Generate integer arrival and service times within inclusive bounds, then sort clients by arrival time. |
| Parallel queues | Process each queue on a separate worker thread. |
| Two scheduling policies | Choose the shortest queue or the queue with the smallest remaining workload. |
| Live monitoring | Follow pending clients and queue contents in a scrolling log. |
| File logging | Save simulation snapshots and final statistics to `log.txt`. |
| Summary statistics | Inspect average waiting time, average service time, and peak occupancy time. |
| Early completion | Finish before the time limit when all clients have arrived and every queue is empty. |

## Technology

- **Java 25** — the included IntelliJ configuration targets JDK 25.
- **Swing and AWT** — simulation inputs, policy selection, log display, and statistics.
- **`Runnable` and `Thread`** — simulation orchestration and independent queue workers.
- **`LinkedBlockingQueue<Task>`** — concurrent FIFO storage for each server.
- **`AtomicInteger`** — atomic updates to a server's remaining workload counter.
- **Java file I/O** — text-based simulation logging.

The project uses standard Java libraries and has no external dependencies, database, Maven configuration, or Gradle configuration.

## Using the Simulator

Enter the simulation settings, choose a policy, and click **Start**. The center panel displays snapshots as the simulation progresses; the bottom panel shows statistics when the run ends.

| Input | Meaning | Example |
| --- | --- | --- |
| Number of clients | Total number of generated clients | `10` |
| Number of queues | Number of parallel service workers | `2` |
| Simulation time | Final simulation tick to process | `30` |
| Minimum arrival time | Earliest possible client arrival | `0` |
| Maximum arrival time | Latest possible client arrival | `10` |
| Minimum service time | Shortest generated service duration | `1` |
| Maximum service time | Longest generated service duration | `4` |
| Selection policy | Rule used to assign arriving clients | `SHORTEST_TIME` |

Use positive client and queue counts, positive service times, nonnegative arrival times, and minimum values no greater than their corresponding maximums. Choose a time limit long enough for the generated workload to finish if you want a complete-run summary.

The fields initially contain `0`; replace them with valid settings before starting. Run one simulation at a time.

### Reading the output

Clients are displayed as:

```text
(id, arrivalTime, remainingServiceTime)