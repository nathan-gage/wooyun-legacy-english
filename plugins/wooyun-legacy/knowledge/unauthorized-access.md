# Unauthorized Access Vulnerability Knowledge Base

> Manual English version of the WooYun unauthorized access knowledge base.
> Original scope: missing authentication, missing authorization, IDOR, privilege bypass, and management-console exposure.

Unauthorized access appears when the server fails to prove who the caller is or what the caller may access. The WooYun cases show that endpoint discovery, object ID manipulation, default credentials, middleware consoles, and weak route guards repeatedly expose sensitive operations.

## 1. Categories

| Category | Description |
|---|---|
| Missing authentication | Endpoint works without login |
| Missing object authorization | Logged-in user accesses another user's object |
| Vertical privilege bypass | Normal user reaches admin or operator functions |
| Hardcoded bypass | Fixed token, encrypted parameter, or static key grants access |
| Path or route bypass | Alternate path avoids an auth filter |
| Middleware exposure | Console or service exposed with weak/default auth |
| Batch operation bypass | Unauthorized IDs included in arrays or bulk requests |

## 2. Endpoint Discovery

Look for endpoints in:

```text
JavaScript bundles
mobile app traffic
API documentation
Swagger/OpenAPI pages
source maps
admin route names
legacy paths
backup source code
```

Common paths:

```text
/admin
/manage
/backend
/api/user/*
/api/order/*
/api/address/*
/api/export/*
/swagger-ui.html
/actuator
/jmx-console
/console
```

## 3. IDOR Testing

Test object identifiers in all locations:

```text
URL:        /api/order/1001
Query:      ?orderId=1001
Body:       {"orderId":1001}
Nested:     {"user":{"id":1001}}
Array:      {"ids":[1001,1002,1003]}
Header:     X-User-ID: 1001
Cookie:     uid=1001
Encoded:    Base64, hex, URL encoding
GraphQL:    node(id:"...")
```

For each object type, create at least two accounts and verify view, edit, delete, export, and action operations across accounts.

## 4. Vertical Privilege Testing

1. Capture an admin request.
2. Replay it as a normal user.
3. Remove or downgrade role parameters.
4. Try direct route access without UI navigation.
5. Test whether role checks are enforced in the controller and service layer, not only the menu.

## 5. Unauthenticated Access Testing

For each endpoint:

- Remove cookies and tokens.
- Replace tokens with expired, malformed, or different-user tokens.
- Switch HTTP methods.
- Try alternate path forms such as `/api/../admin`, double slashes, encoded slashes, and case changes if the stack is path-sensitive.
- Test export, download, and batch endpoints separately; they are often missed.

## 6. Default and Weak Credentials

Unauthorized access frequently combines with weak credentials on middleware, admin consoles, network devices, and OA systems.

Examples to check in authorized tests:

```text
admin/admin
admin/admin123
admin/123456
test/test
tomcat/tomcat
root/root
```

Use rate limits and explicit authorization. Do not brute force beyond the agreed scope.

## 7. Defensive Patterns

- Authenticate every sensitive endpoint.
- Authorize every object access at the service layer.
- Use tenant IDs from the server-side session, not from the client.
- Check permissions on batch items one by one.
- Deny by default and explicitly allow required actions.
- Protect admin and middleware consoles behind VPN, SSO, MFA, and network allowlists.
- Add authorization tests for every new endpoint.

## 8. Report Template

```text
Title: Unauthorized access to [object/action]
Actor: [unauthenticated, normal user, tenant A]
Target: [admin function, tenant B object, other user data]
Endpoint: [URL and method]
Manipulation: [removed auth, changed ID, replayed request]
Impact: [view, modify, delete, export, privilege escalation]
Root cause: [missing authn/authz check]
Remediation: [server-side permission check, deny by default, tests]
```

## 9. Key Lessons

- Hiding buttons is not authorization.
- Object IDs in any request location are security-sensitive.
- Batch APIs need per-item authorization.
- Internal or admin APIs often become reachable through JavaScript, mobile apps, or documentation.
