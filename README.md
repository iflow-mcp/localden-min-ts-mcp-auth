# min-ts-mcp-auth
Minimal implementation of MCP server auth with TypeScript.

## Security Notes

This demo always validates the access token audience (resource indicator) returned by the introspection endpoint.

Checks performed during introspection:

1. Token is successfully introspected (HTTP 200 from the authorization server).
2. `active` flag (RFC 7662) is not `false`.
3. `aud` claim (string or array) is present and at least one value matches the server's base URL (RFC 8707 resource indicator semantics).
4. Scopes are parsed into an array for later use (no specific scopes required by default).

Not implemented (could be added):
* Local JWT signature verification via JWKS (currently relies on remote introspection).
* Explicit `iss`, `typ`, `nbf`, `exp` enforcement (only `exp` is returned and stored, not validated inline).
* Caching / throttling of introspection requests.

Use this code for experimentation only; harden before production.
