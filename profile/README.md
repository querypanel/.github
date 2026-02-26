# QueryPanel

**AI-powered data visualization and natural language to SQL.** QueryPanel lets you build dashboards and analytics experiences that turn questions into charts—with tenant isolation, session context, and optional embedded customer dashboards.

---

## What we build

- **Natural language → SQL** — Attach your database (Postgres, ClickHouse), sync schema, and ask questions in plain language. The API returns SQL, parameters, and chart specs.
- **Tenant-safe by design** — Tenant isolation is enforced via prompt engineering and optional execution-time checks; no manual SQL patching.
- **Charts and dashboards** — Save charts, pin them to dashboards, and embed white-label experiences in your app with JWT auth.
- **One API for everyone** — The same backend serves admin tools, tenant backends, and embedded customer UIs.

---

## Repositories

### [node-sdk](https://github.com/querypanel/node-sdk) — `@querypanel/node-sdk`

Server-side TypeScript/Node SDK for the QueryPanel API. Use it from your backend (Next.js API routes, customer services, etc.) to:

- **Generate SQL from natural language** — `qp.ask("Top countries by revenue", { tenantId, database })`
- **Attach databases** — Postgres and ClickHouse adapters with schema sync and tenant field configuration
- **Sign JWTs** — RS256 with your org private key for embed and API auth
- **Manage charts and sessions** — Save charts, list history, pin active charts for dashboards, and keep conversation context with session IDs
- **Modify charts** — Change chart type, time granularity, or custom SQL and re-run

Runs on Node 18+, Deno, or Bun. No direct DB connection is sent to the API; execution stays in your process.

```bash
npm install @querypanel/node-sdk
```

```ts
import { QueryPanelSdkAPI } from "@querypanel/node-sdk";

const qp = new QueryPanelSdkAPI(apiUrl, privateKey, organizationId);
qp.attachPostgres("analytics", createClient, { tenantFieldName: "tenant_id" });
const result = await qp.ask("Revenue by country", { tenantId: "acme", database: "analytics" });
```

Full docs and examples: **[node-sdk README](https://github.com/querypanel/node-sdk)**.

---

### [react-sdk](https://github.com/querypanel/react-sdk) — `@querypanel/react-sdk`

React components for AI-powered data UIs. Use the same components in your admin app and in embedded customer dashboards.

- **QueryPanelProvider + useQueryPanel** — Ask questions, get results, modify charts with a single context
- **QueryInput, QueryResult** — Search input with chips, combined chart + SQL + data table
- **VegaChart, DataTable, ChartControls** — Building blocks for custom layouts
- **QuerypanelEmbedded** — Embed a deployed dashboard (your backend serves auth and proxy to QueryPanel API)
- **Theming** — Presets (`default`, `sunset`, `emerald`, `ocean`) and custom themes for white-labeling

The frontend talks to **your backend** or the QueryPanel API directly; it never calls the admin app for API work.

```bash
npm install @querypanel/react-sdk
```

```tsx
import { QueryPanelProvider, QueryInput, QueryResult, useQueryPanel } from "@querypanel/react-sdk";

<QueryPanelProvider config={{ askEndpoint: "/api/ask", colorPreset: "default" }}>
  <QueryInput onSubmit={ask} />
  <QueryResult result={result} onModify={modify} />
</QueryPanelProvider>
```

Full docs and components: **[react-sdk README](https://github.com/querypanel/react-sdk)**.

---

## Links

- **Product:** [querypanel.io](https://querypanel.io)
- **Node SDK:** [github.com/querypanel/node-sdk](https://github.com/querypanel/node-sdk)
- **React SDK:** [github.com/querypanel/react-sdk](https://github.com/querypanel/react-sdk)

---

We welcome issues and pull requests on our SDK and API repos.
