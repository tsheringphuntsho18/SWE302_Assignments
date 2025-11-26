# Testing Analysis

## Packages Containing Tests

- [`common`](common/unit_test.go)
- [`users`](users/unit_test.go)

## Packages Without Tests

- [`articles`](articles/) (no `*_test.go` files present)
- Root package (no `*_test.go` files for `hello.go` or other root files)

## Failing Tests and Reasons

- Some tests in [`common`](common/unit_test.go) and [`users`](users/unit_test.go) failed due to validator version compatibility issues.
- In [`users/unit_test.go`](users/unit_test.go), expectedtests that expect specific database errors (such as "no such table: follow_models" or "UNIQUE constraint failed: user_models.email") failed because of the database schema or constraints do not match expectations.
- Tests relying on regular expressions for JWT tokens or error messages failed because of the output format changes or if the JWT generation logic is updated.
- The `articles` package has no tests, so no failures are possible there.

**Note:** The test suite is incomplete by design for the assignment, and some failures are expected.