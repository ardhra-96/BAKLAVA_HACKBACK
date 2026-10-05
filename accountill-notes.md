# Accountill Codebase Observations

## Claim 1
- Claim: Backend authentication middleware is never mounted on any Express route or controller, leaving all API endpoints publicly accessible without authorization.
- Evidence: server/index.js:32
- Confidence: Confirmed

## Claim 2
- Claim: The `getClients` controller endpoint retrieves and paginates all client records across the entire database without tenant scoping or user ID filtering.
- Evidence: server/controllers/clients.js:45
- Confidence: Confirmed

## Claim 3
- Claim: Server-side PDF generation writes to a single static file path on disk, causing concurrent requests to overwrite each other's generated invoices.
- Evidence: server/index.js:57
- Confidence: Confirmed

## Claim 4
- Claim: The invoice data model embeds client contact details directly as a subdocument snapshot rather than referencing `ClientModel` through an ObjectId foreign key.
- Evidence: server/models/InvoiceModel.js:17
- Confidence: Confirmed

## Claim 5
- Claim: The `/customers` route mounts `ClientList` as its top-level page component rather than directly mounting `Clients`.
- Evidence: client/src/App.js:40
- Correction: The agent previously assumed `/customers` rendered `Clients.js` directly based on file naming, but `App.js` routes to `ClientList.js`, which then nests `Clients.js` as an unrouted child table component.
- Confidence: Confirmed
