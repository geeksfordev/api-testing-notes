# Tools I use

My current toolbox for API work, and when I reach for each one.

## Exploring an endpoint

### cURL

Still my first move for a single request. It's already in every terminal, and a saved shell history doubles as a rough log of what I tested.

### A GUI API client

When I need to build a complicated request, save it, or share it with someone, a desktop API client is easier than a long cURL command.

## Testing and regressions

### Keploy

For turning the requests I check by hand into repeatable tests and mocks. Details are in [Turning real traffic into tests](traffic-to-tests.md), and the project lives at [keploy.io](https://keploy.io).

### My language's test framework

Unit tests still live in Go's `testing` package or Jest, depending on the project.

## Comparing options

If you're choosing tools for your own team, this [list of API testing tools](https://keploy.io/blog/community/api-testing-tools) is a useful starting point. It covers both open-source and commercial options.

*Disclosure: I work at Keploy.*
