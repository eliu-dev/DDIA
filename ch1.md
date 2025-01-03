# Reliability, Scalability, and Maintainability

## Reliability
Reliability is the ability for a database to work correctly (performing its intended function at the right level) even in the face of adversity

Some concepts from other sources include (e.g., Leetcode System Design):

- High Availability: the ability of a system to remain operational.
- Reliability: the ability of a system to remain consistent.
- Resilience: the ability of a system to recover from failures.
- Fault-tolerance: the ability of a system to continue operating even if some components fail.

### Faults
Things that can go wrong are caled **faults**. 

- Hardware faults can come in the form of downtime caused by machine failure, power outage, or network failure.
- Software faults can come in the form of bugs (e.g., edge case inputs, race conditions, etc.), runaway processes, dependency failures, or cascading failures..
- Human faults can come in the form of configuration errors, data entry errors, or other mistakes.


## Scalability

As the system grows in data volume, traffic, or complexity, it should be able to the growth. Scabality is about the ability to handle **load**.

### Load
Load is described by an appropriate **load parameter**, which is a measure of the expected performance on a relevant activity that the system has to handle (e.g., requests per second, tweets per second, I/O, etc.).

### Performance Characteristics
A few key performance characteristics include:

- **Latency** (aka **response time**): the time it takes for a single request to be processed.
- **Throughput**: the number of requests that can be processed per unit of time.
- **Capacity**: the maximum load that the system can handle.

The performance **distribution** should be used to account for variation in load (e.g., p95, p99, and p999). The distribution can then be used for **service level objectives (SLOs)** that may be contractually enforced by **service level agreements (SLAs)**.

#### Tail Latency Amplification
Tail latency refers to the latency of the slowest requests. It is particularly important for backend systems because even if the processes for handling a user requests are parallelized, the slowest request will determine the latency of the entire system if the system has to wait for all requests to complete.

**Tip**: Forward decay is a technique for measuring tail latency by using a small sample size and then extrapolating the results to the entire population. T-digest is a more accurate method for measuring tail latency that measures latency by dividing the data into buckets and then using a weighted average to estimate the tail latency.

### Scabaility Solutions

- **Scaling Up (aka Vertical Scaling)**: increasing the resources of a single machine (e.g., CPU, memory, disk, etc.).
- **Scaling Out (aka Horizontal Scaling or Shared-Nothing Architecture)**: distributing load by increasing the number of instances (e.g., adding more machines).

Systems are described as **elastic** if they can scale up or scale out to handle load.

## Maintainability

The system should be easy to understand, modify, and extend. People should be able to work on the system productively.

- **Operability**: make it easy for teams to keep the system running smoothly. An operable system includes making it easy to
    - Monitor system health
    - Track down problems
    - Update the system (including security patches)
    - Understand how different systems interact
    - Anticipate future problems
    - Establish CI/CD for productivity and safety
    - Perform complex maintenance and migration tasks
    - Maintain security when changes are made
    - Preserve institutional knowledge when individuals leave
- **Simplicity**: make it easy for new engineers to understand the system by reducing complexity.
- **Evolvability (aka Extensibility, Modifiability, or Plasticity)**: make it easy for engineers to make changes to the system and adapt it to new scenarios.



