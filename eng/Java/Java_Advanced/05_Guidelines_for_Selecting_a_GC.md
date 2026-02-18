# Guidelines for Selecting a GC

<br>

- If application performance is the most important factor and pause times over 1 second are acceptable
  - Let the VM choose the collector on its own
  - The VM will likely choose well on its own, but if you want to select manually, enable the `XX:+UseParallelGC` option
- If response time is more important than overall throughput and pause times must be under 1 second
  - Try using a Concurrent Collector
    - Enable the `XX:+UseConcMarkSweepGC` option or the `XX:+UseG1GC` option
- If performance is still insufficient
  - Try adjusting the heap size and generation sizes
