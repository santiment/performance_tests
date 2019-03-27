# Performance tests

A collection of performance tests against our APIs using JMeter.

## Running a test

To run a test use the following command:

```bash
$ jmeter -n -t wordContext.jmx -l results.jtl -e -o results
```

Here `wordContext.jmx` is the file with the performance test. After the tests has finished you can see the HTML report by opening `results/index.html`.

## Tests

Here is a description of the tests in the repo

### Word Context

This is a performance test of the word context API. Each request to the API will be for a word taken from the CSV file `word_context_dataset.csv`. You can specify the number of users and the duration of the test using the `threads` and `duration` parameters like this:


```bash
$ jmeter -n -t wordContext.jmx -e -o results -l result.jtl -Jthreads=200 -Jduration=600
```

This is going to run the test with 200 concurrent users for 10 mins.