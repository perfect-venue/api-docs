# Perfect Venue API Docs

This repo hosts the OpenAPI spec and Redoc-generated site for the Perfect Venue REST API.

## What to Edit

- `openapi/openapi.yaml` contains the site introduction, authentication guide, rate limits, tag descriptions, changelog, servers, and top-level path references.
- `openapi/paths/*.yaml` contains endpoint-level documentation.
- `openapi/components/schemas/*.yaml` contains shared request and response schemas.
- `docs/index.html` is the Redoc HTML template.
- `index.html` is the generated static docs site.

## Local Development

Install dependencies:

```bash
npm install
```

Preview the docs:

```bash
npm start
```

Lint the OpenAPI spec:

```bash
npm test
```

Build the bundled spec:

```bash
npm run build:spec
```

Build the static site:

```bash
npm run build:site
```

## Documentation Standards

The docs should help a partner build a working integration without needing product context from the Perfect Venue team.

When adding or changing endpoints, include:

- The job the endpoint is meant to solve.
- Required setup or IDs the caller needs before making the request.
- A realistic request example.
- A realistic success response shape.
- Common validation or permission errors.
- Pagination, filtering, sorting, and retry behavior when relevant.

Prefer concrete examples over abstract descriptions. Use stable placeholder values such as `VENUE_ID`, `CONTACT_ID`, `EVENT_ID`, and `ACCESS_TOKEN` in examples.

## Recommended Implementation Flow

Partner integrations usually follow this order:

1. Have a Perfect Venue user authorize the OAuth application, then store the access token and refresh token.
2. Call `GET /venues` to discover venue IDs and venue-specific configuration.
3. Create or map contacts with `POST /contacts`, or use inline contact creation when creating an event.
4. Create events with `POST /events`.
5. Sync changes with `GET /events` filters and outbound webhooks.
6. Treat `PV-Webhook-Id` as an idempotency key when processing webhook deliveries.

Keep this flow easy to find in the generated docs when adding new capabilities.
