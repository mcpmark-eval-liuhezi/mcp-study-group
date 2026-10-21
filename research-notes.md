# Model Context Protocol — Study Group Notes

Session 1 groundwork: what MCP is, how it works, and why it matters. All facts below come from the official documentation pages listed in **Sources** — each page was opened and read directly, not summarized from search snippets.

## What is MCP

The Model Context Protocol (MCP) is an **open-source standard for connecting AI applications to external systems**. Using MCP, AI applications like Claude or ChatGPT can connect to data sources (e.g. local files, databases), tools (e.g. search engines, calculators), and workflows (e.g. specialized prompts) — enabling them to access key information and perform tasks.

- The official analogy: think of MCP like a **USB-C port for AI applications**. Just as USB-C provides a standardized way to connect electronic devices, MCP provides a standardized way to connect AI applications to external systems.
- It replaces fragmented one-off integrations with a single protocol: build one MCP server per system, and any MCP-capable application can use it.
- Benefits by audience: **developers** reduce development time and complexity; **AI applications/agents** gain access to an ecosystem of data sources, tools, and apps; **end-users** get more capable assistants that can access their data and act on their behalf.
- MCP is a broad ecosystem, not a single-vendor lock-in — it is an open protocol supported across a wide range of clients and servers: AI assistants like Claude and ChatGPT, and development tools like Visual Studio Code, Cursor, and MCPJam ("build once and integrate everywhere").
- **Who is behind it:** MCP is an open-source project. Per the official specification-and-documentation repository on GitHub, the Model Context Protocol was created by David Soria Parra (@dsp) and Justin Spahr-Summers (@jspahrsummers). The project publishes the specification, the protocol schema, official SDKs for multiple languages, reference server implementations, and development tools such as the MCP Inspector, all maintained publicly under the `modelcontextprotocol` GitHub organization, with the official documentation built at modelcontextprotocol.io.

## Architecture

MCP follows a **client–server architecture**. The key participants are:

- **MCP host** — the AI application (e.g. Claude Desktop, Claude Code, VS Code) that coordinates and manages one or multiple MCP clients.
- **MCP client** — a component created by the host that maintains a dedicated connection to one MCP server and obtains context from that server for the host to use. One client is created per server: when VS Code connects to the Sentry server and then to the local filesystem server, it instantiates a separate MCP client object for each.
- **MCP server** — a program that provides context to MCP clients, regardless of where it runs. A server launched by the host as a subprocess using the stdio transport is "local"; a server running on a remote platform using Streamable HTTP (e.g. the official Sentry server) is "remote".

The protocol has two layers:

- **Data layer** — the JSON-RPC 2.0 based exchange protocol defining message structure and semantics: capability and version discovery, and the core primitives (tools, resources, prompts) plus notifications and progress tracking.
- **Transport layer** — the communication mechanisms and channels between clients and servers: transport-specific connection establishment, message framing, and authorization.

### Transports

A transport is a **binding**: it defines how messages are framed and delivered, while the message patterns are identical on every transport. MCP uses JSON-RPC (UTF-8 encoded) for messages, and the standard bindings are:

- **stdio** — newline-delimited messages over the standard streams of a client-launched subprocess. Best for local servers: optimal performance with no network overhead; typically serves a single client.
- **Streamable HTTP** — each message is an HTTP POST to a single MCP endpoint, with replies arriving as a JSON object or a request-scoped SSE stream. Used by remote servers; supports HTTP authentication (bearer tokens, API keys, custom headers), with OAuth recommended.

Clients and servers may also implement custom transports (e.g. over Unix domain sockets or TCP), provided they preserve the JSON-RPC message format, the message patterns, and the per-request metadata model. Cancellation works differently per binding: a `notifications/cancelled` notification on stdio versus closing the response stream on Streamable HTTP.

### What servers expose: the three primitives

MCP defines three core primitives that **servers** expose to clients:

- **Tools** — executable functions that AI applications can invoke to perform actions (file operations, API calls, database queries). They are **model-controlled**: the model can discover and invoke them automatically based on context and user prompts. Discovery via `tools/list`; execution via `tools/call`.
- **Resources** — data sources that provide contextual information (file contents, database records or schemas, API responses), each uniquely identified by a URI (common schemes include `https://`, `file://`, `git://`). They are **application-driven**: the host application decides how to incorporate them (tree/list UI, search, or automatic inclusion). Discovery via `resources/list`; retrieval via `resources/read`; servers may also support subscriptions and parameterized resource templates.
- **Prompts** — reusable templates that structure interactions with language models (system prompts, few-shot examples), optionally with arguments for customization. They are **user-controlled**: the user explicitly selects them (e.g. as slash commands). Discovery via `prompts/list`; retrieval via `prompts/get`.

Concrete example from the docs: an MCP server that provides context about a database can expose **tools** for querying the database, a **resource** containing the database schema, and **prompts** for common analysis tasks.

## Use cases

1. **Personalized AI assistants** — agents connect to Google Calendar and Notion via MCP servers, so a single assistant can read your schedule and notes and act on them.
2. **Design-to-code workflows** — Claude Code can use a Figma design through MCP to generate an entire web app.
3. **Enterprise data chatbots** — enterprise chatbots connect to multiple databases across an organization, letting users analyze data through chat.
4. **Creative and physical tooling** — AI models can create 3D designs in Blender and print them out using a 3D printer.
5. **Developer tooling** — an IDE acting as an MCP host (e.g. VS Code) connects to servers such as Sentry and the local filesystem, pulling error data and project files into the assistant's context.

## Sources

Pages actually opened and read for these notes (not search snippets). Where a URL failed to load (404), the official page substituted for it is listed with a note.

- [What is the Model Context Protocol (MCP)?](https://modelcontextprotocol.io/docs/getting-started/intro) — Official introduction; contributed the plain-language definition, the USB-C analogy, benefits by audience, and the ecosystem of supported clients.
- [Architecture overview](https://modelcontextprotocol.io/docs/concepts/architecture) — Contributed the host/client/server participant model, the data vs. transport layer split, and the three server primitives with the database example. (Substituted for `https://modelcontextprotocol.io/docs/getting-started/architecture`, which returned 404.)
- [Transports](https://modelcontextprotocol.io/docs/concepts/transports) — Contributed transports-as-bindings, stdio and Streamable HTTP, JSON-RPC message encoding, cancellation semantics, and custom transports.
- [Tools](https://modelcontextprotocol.io/docs/concepts/tools) — Contributed the tools primitive: model-controlled interaction, `tools/list` / `tools/call`, tool definitions, and result content types. (Substituted for `https://modelcontextprotocol.io/docs/concepts/core-concepts`, which returned 404.)
- [Resources](https://modelcontextprotocol.io/docs/concepts/resources) — Contributed the resources primitive: application-driven interaction, URI-identified data, `resources/read`, resource templates, subscriptions, and common URI schemes.
- [Prompts](https://modelcontextprotocol.io/docs/concepts/prompts) — Contributed the prompts primitive: user-controlled interaction, `prompts/get`, arguments, and message content types.
- [Model Context Protocol — specification & documentation repo (GitHub)](https://github.com/modelcontextprotocol/modelcontextprotocol) — Contributed the "who is behind it" facts (creators David Soria Parra and Justin Spahr-Summers) and the project's published artifacts (spec, schema, SDKs, reference servers, MCP Inspector). (Substituted for `https://modelcontextprotocol.io/docs/clients`, which returned 404; client-side behavior was instead covered by the architecture and primitives pages.)
