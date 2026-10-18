# Turning real traffic into tests

Notes from a month of using record and replay on a Python service that had almost no tests.

## The short version of how it works

A recording tool sits next to the app and saves each incoming request and response as a test case, plus every database query and downstream call as a mock. Later it replays the requests, serves the mocks in place of the real dependencies, and reports anything that differs.

## The tool I use

I use [Keploy](https://keploy.io), which is open source and records at the network level, so the service code didn't need a single change. For a Flask app the two commands look like this:

```bash
keploy record -c "python3 app.py"
keploy test -c "python3 app.py" --delay 10 --path "./tests"
```

## What I learned

### Record the boring paths first

My first instinct was to record edge cases. It's more useful to start with the ten requests the app handles most often. Those cover the code paths that break most visibly.

### Noisy fields are the first thing that bites

Timestamps, generated IDs and tokens change on every run, so a naive comparison fails constantly. Keploy flags these noisy fields and ignores them, which saved me from writing my own filtering rules.

### Re-record after intentional changes

When I change a response on purpose, the old recording becomes wrong. I re-record that endpoint in the same pull request, so the test suite always matches the current behaviour.

### Keep recordings in the repo

The test cases and mocks are plain files. Committing them next to the code means reviewers see behaviour changes in the diff, and CI can replay them without any external setup.

### Coverage went up without new test files

The service went from a handful of hand-written tests to decent coverage of its main endpoints in an afternoon. That never would have happened if I'd had to write each test by hand.

## Where it doesn't help

It's built for APIs and integration testing. UI and browser flows still need a separate tool.

If you want the longer explanation, Keploy has a good write-up on [record-and-replay API testing](https://keploy.io/api-testing).

*Disclosure: I work at Keploy.*
