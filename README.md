# Front MCP server

Find support contacts and explicitly add a new email contact without sending a message.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `FRONT_API_TOKEN`



Credential help: https://raw.githubusercontent.com/frontapp/front-api-specs/main/core-api/core-api.json

## Provider setup

Use your own Front API token with contact read/write permissions. Contacts and handles must belong to authorized customer records. This connector does not send messages.

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call front_list_contacts '{"limit":10}'
```

## Use with an MCP client

Launch `node /absolute/path/front-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| front_list_contacts | Read | Read one bounded page of contacts. |
| front_create_contact | Explicit approval required | Create an email contact with explicit handles; no message is sent. |

## Concrete workflow

Find support contacts and explicitly add a new email contact without sending a message.

1. front_list_contacts
2. front_create_contact

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Activate with PipMCP](https://pipmcp.com/github/start?app=front&integration=front-mcp&utm_source=github&utm_campaign=github-front-mcp&utm_content=readme) when you want the hosted service.  Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/front/).

## Provenance and maintenance

- https://raw.githubusercontent.com/frontapp/front-api-specs/main/core-api/core-api.json

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.
