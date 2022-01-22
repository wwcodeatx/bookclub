# CH 1. Reliable, Scalable, and Maintainable Applications

## Summary

Most applications are data-intensive, instead of compute-intensive. There are lots of building blocks - databases, caches, search indexes, stream/batch processing, etc. They all have different access patterns, implementations and performance characteristics, that satisfies different requirements. Your application is combining these building blocks, and becomes another data system. The fundamentals of what we are trying to achieve are:

- reliable: the system should continue to work correctly even when things go wrong
- scalable: as the system grows (in data volume, traffic or complexity) there should be reasonable way of dealing with the growth
- maintainable: over time, many different people will work on the system, and they should be able to work on it productively

### Reliability

The system should continue to work **correctly** even when things go wrong, or be fault-tolerant, or resilient.

Faults can be:

- hardware fault
- software errors
- Human errors

For hardware fault, add redundancy, or use software fault-tolerant techniques.

For software and human errors, carefully thinking about assumptions and interactions in the system, design system to minimize errors, allow quick recovery like restart processes, thorough testing, and increase observability.

### Scalability

The system should be able to cope with increased load. The process:

1. describing load: use load parameter, can be request per second, active users, r/w in databases, hit rate in databases, etc. Use
2. describing performance: load parameter - resource (CPU, memory, network) - performance (in percentile)
3. approach to cope with load: scaling up & scale out

### Maintainability

Legacy code is just hard. We should still try:

- Operability: visibility, automation, avoid single point of failure, good documentation, good default but easy to modify, self-healing
- Simplicity: use good abstraction
- Evolvability/ Extensibility/ Modifiability

## Discussions

### About documentation
Documentation also helps simplification. Because when you have to explain it to other people, it has to make sense, and be understandable.

One problem of documentation is, they are not invalidate. People delete outdated code, but rarely deletes documents. One possible solution is to verison your documentations, like [GitBook](https://www.gitbook.com/)

It's important to document the "Why". The "how" documentation may be stale, but the "why" always stands.

### About scaling out vs scaling up
Scaling up is to add hardware to existing resources - like adding more memory, hard drive space, or switching to a more powerful CPU.
Scaling out is to add more resources - like adding another server, or a few more data store nodes.

Scaling up is in general easier. Also, most relational database is very hard to scale out. So consider scaling up first.

To plan scaling: it's important to not introduce complexity, not over-engineer, but plan ahead. For example, to scale out, the service must be stateless. So if a client calls server 1 first, there's no data stored locally, and the client can call server 2 next time. This is a good consideration when planning a system.

### About SLA
SLA stands for service level agreement. It's often describe in percentile. It should never define a P100 SLA, as extreme accidents can happen. There can be multiple SLAs on the same metrics, for example, P90 and P99 latency SLAs.


