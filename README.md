# Performance tests

A collection of performance tests against our APIs using JMeter.

## Running a test

To run a test use the following command:

```bash
$ jmeter -n -t wordContextTest.jmx -l results.jtl -e -o results
```

Here `wordContext.jmx` is the file with the performance test. After the tests has finished you can see the HTML report by opening `results/index.html`.

For all the tests it is possible to specify the number of users and the duration of the test using the `threads` and `duration` parameters like this:

```bash
$ jmeter -n -t wordContextTest.jmx -l results.jtl -e -o results -Jthreads=200 -Jduration=600
```

## Tests

Here is a description of the tests in the repo

### Word Context Test

This is a performance test of the word context API. Each request to the API will be for a word taken from the CSV file `word_context_dataset.csv`. To run the test:

```bash
$ jmeter -n -t wordContextTest.jmx -e -o results -l result.jtl -Jthreads=200 -Jduration=600
```

This is going to run the test with 200 concurrent users for 10 mins.

### Project By Slug Test

This is a performance test of the projectBySlug API. Each request to the API will be for a project taken from the CSV file `projects_dataset.csv`. To run the test:

```bash
$ jmeter -n -t projectBySlugTest.jmx -e -o results -l result.jtl -Jthreads=200 -Jduration=600
```

This is going to run the test with 200 concurrent users for 10 mins.

### All Projects Balances Test

A test which requests the balances of all projects. This test should be hitting only cachable fields, but for a large amount of projects. To run the test:

```bash
$ jmeter -n -t allProjectsBalancesTest.jmx -e -o results -l result.jtl -Jthreads=100 -Jduration=600
```

This is going to run the test with 100 concurrent users for 10 mins.
