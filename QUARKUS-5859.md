# QUARKUS-5859 WebSocket Next Permission Checkers


#### Links to the Resources


#### Scope of the Testing

The primary goal is to **verify the correct functionality of WebSocket Next permission checkers**. This includes ensuring:

*   **Custom `PermissionChecker` implementations can be defined.**
*   **The `@PermissionChecker` annotation and its identifier work as expected.**
*   **`@PermissionsAllowed` annotation correctly references permission checkers on WebSocket endpoints.**
*   **Permission checkers are invoked during the WebSocket handshake or message processing.**
*   **Connection/action is allowed when the permission checker returns `true`.**
*   **Connection/action is denied when the permission checker returns `false`.**

Integration tests will focus on the interaction with security features.

##### Test Cases

*   **Basic Permission Checker Implementation:**
    *   Verify that a simple `@ApplicationScoped` bean implementing `PermissionChecker` can be created.
    *   Test the usage of `@PermissionChecker` with a unique identifier.
    *   Confirm that a `@ServerWebSocket` endpoint can reference a permission checker using `@PermissionsAllowed` with the correct identifier.
    *   Test that the permission checker's `check()` method is invoked upon connection attempt (handshake).
    *   Verify that a connection is established when the `check()` method returns `true`.
    *   Verify that a connection is rejected with the expected status code/message when the `check()` method returns `false`.

*   **Permission Checker with Arguments:**
    *   Test that permission checkers can receive relevant arguments such as the `ContainerRequestContext` (for handshake).
    *   Ensure the correct argument types are passed to the `check()` method.

*   **Integration with Authentication:**
    *   Test scenarios where the permission checker uses the `SecurityIdentity` to make authorization decisions (e.g., based on principal name).
    *   Verify that authentication is performed before the permission checker is invoked.

*   **Error Handling:**
    *   Test the behavior when an exception is thrown within the `PermissionChecker` implementation.

## Getting familiar with the feature
Getting familiar with
- Websocket next reference: https://quarkus.io/version/main/guides/websockets-next-reference

## Existing test coverage
QE TS already has tests for websocket-next.
These will be used as a base for new tests.

### Impact on test suite
Some test classes will be added in the module...

## Impact on resources
A new module will be created, requires additional test execution.
Tests will be executed on both JVM and native and on both baremetal and OCP.
Expected additional execution time in minutes for each case.

## Contacts
* Tester: Jose Carranza <jcarranz@redhat.com>