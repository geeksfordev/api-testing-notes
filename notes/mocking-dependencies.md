# Mocking dependencies

Most endpoints don't work alone. They call a database, a payment provider, an auth service or another internal API. To test them reliably, you need those dependencies to behave the same way every time.

## Why mock at all

* **Speed:** real dependencies are slow, mocks respond instantly.
* **Stability:** a flaky third-party API shouldn't fail your test suite.
* **Edge cases:** it's hard to make a real payment provider return a timeout on demand. A mock can.
* **Cost:** some APIs charge per call.

## Common ways to mock

### Hand-written stubs

You write a fake version of the dependency in code. Full control, but every stub has to be written and maintained by hand, and it drifts from reality over time.

### Mock servers

A standalone server that returns predefined responses for matching requests. Good for teams sharing the same mocks, but someone still has to define every response.

### Recorded mocks

You capture the real responses once, while the app talks to the real dependencies, then replay them in tests. The mocks match reality because they came from reality.

## What I've learned

Hand-written mocks are fine for a handful of cases. Past that, they become a second codebase nobody wants to maintain. Recorded mocks have been the biggest time saver for me, which is what the next note is about.
