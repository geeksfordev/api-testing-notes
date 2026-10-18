# API testing basics

API tests check that an endpoint does what it promises: the right status code, the right response body, and the right side effects. They sit between unit tests and full end-to-end tests, which makes them the best value for most backend teams.

## The main types

### Functional tests

Send a request, check the response. Does `POST /orders` return `201` and the created order? Does it return `400` when a required field is missing?

### Integration tests

Check that the endpoint works with its real collaborators: the database, a cache, another service. These catch the bugs unit tests miss, like a wrong column name or a changed response from a downstream API.

### Regression tests

Re-run the same checks after every change to make sure nothing that worked before is now broken. Most production incidents I've seen were regressions, not new features failing.

### Contract tests

Check that the shape of a request or response hasn't changed in a way that breaks consumers.

## What to check on every endpoint

* Status code for the happy path and the main error paths
* Response body structure and key values
* Headers that matter (auth, caching, content type)
* Side effects: was the row written, was the event published?
* Response time, at least roughly

## The hard part

Writing the first test is easy. Keeping hundreds of them realistic and up to date as the API changes is where most teams give up. The next two notes cover how I deal with that.
