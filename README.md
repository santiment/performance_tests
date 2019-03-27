# Performance tests

A collection of performance tests against our APIs using JMeter.

## Running a test

To run a test use the following command:

```bash
$ jmeter -n -t wordContext.jmx -l results.jtl -e -o results
```

Here `wordContext.jmx` is the file with the performance test. After the tests has finished you can see the HTML report by opening `results/index.html`.
