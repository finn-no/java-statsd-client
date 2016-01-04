statsd-lmax-disruptor-client
==================

A statsd client library implemented in Java.
Allows for Java applications to easily communicate with statsd.
Built with LMAX disruptor for performance.

NOTE: In some instances, this implementation can lose events silently.

This version is forked from the upstream [java-dogstatsd-client](https://github.com/indeedeng/java-dogstatsd-client) project.

This version ensures compatibility with vanilla statsd.

Downloads
---------
You need to build the project off the release tag and upload it to your own maven repository.

```xml
<dependency>
    <groupId>no.finn</groupId>
    <artifactId>statsd-lmax-disruptor-client</artifactId>
    <version>2.0.9</version>
</dependency>
```

Usage
-----
```java
import com.timgroup.statsd.StatsDClient;
import com.timgroup.statsd.NonBlockingStatsDClient;

public class Foo {

  private static final StatsDClient statsd = new NonBlockingStatsDClient(
    "my.prefix",                          /* prefix to any stats; may be null or empty string */
    "statsd-host",                        /* common case: localhost */
    8125,                                 /* port */
    new String[] {"tag:value"}            /* DataDog extension: Constant tags, always applied */
  );

  public static final void main(String[] args) {
    statsd.incrementCounter("foo");
    statsd.recordExecutionTime("bag", 25);
    statsd.recordGaugeValue("bar", 100);

    statsd.recordGaugeValue("baz", 0.01); /* DataDog extension: support for floating-point gauges */
    statsd.recordHistogram("qux", 15)     /* DataDog extension: histograms */
    statsd.recordHistogram("qux", 15.5)   /* ...also floating-point */
  }
}
```

