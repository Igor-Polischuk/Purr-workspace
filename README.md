# Purr public debug workspace

A ready-to-open Purr workspace for learning REST and GraphQL, inspecting HTTP behavior, and practicing Git and local-secret transfer. The Purr name is **Git workspace**. It contains 51 documented requests, eight folders, two pinned GraphQL schemas and two optional environments. No API account is required for the general examples.

## Open and start

1. Clone or copy this folder. In Purr desktop choose **New workspace → Import → Choose folder instead** and select the folder containing `purr.yaml`.
2. Open **00 Start here → 01 First request**, read **Docs**, then **Send**. Expect HTTP 200 and `status: ok`.
3. Send **02 Variables and query parameters**. Compare enabled and disabled rows with the response.
4. Visit the numbered folders below. Each request has steps and expected results in its Docs tab.

A fresh clone contains definitions, not response history, cookies or local secret values. Keep the workspace ID and resource IDs when transferring it. Purr does not open two different folders with the same workspace ID in one profile; use a second installation/profile for a clone-transfer exercise.

## Suggested learning path

| Folder | Practice |
| --- | --- |
| 00 Start here | Send a request, inspect headers and timeline, encode Unicode query values |
| 01 DummyJSON | Pagination, search, simulated CRUD and a dynamic variable dependency |
| 02 PokeAPI | Read-only API, nested JSON, lists and missing resources |
| 03 Countries GraphQL | Variables, filters, fragments, aliases and multiple operations |
| 04 GraphQLPlaceholder | Related objects, integer inputs and simulated mutations |
| 05 HTTPbin | JSON, form and XML bodies; image, HTML and XML responses; status, redirects, delay and cookies |
| 06 Local secrets lab | Missing references, local provisioning and manual encrypted transfer |
| 07 Git and environments lab | Stable files for clean merges, conflicts and environment changes |

All general requests work from workspace defaults. **Larger pages** changes pagination; **Alternate inputs** changes Pokemon, country and product search. **03 Environment comparison** shows effective values. Return to no environment to use the defaults again.

## Follow a dynamic dependency

Open **01 DummyJSON → 04 Dynamic product lookup**. The URL uses `selected_product_id`, a dynamic variable extracted from **03 Search products** using `$.products[0].id`. Sending the dependent request resolves the source automatically. A successful value is cached for 120 seconds. Inspect the dependency in Variables and change `search_term`. An empty result cannot provide an ID; this is a useful failure case. Created or updated DummyJSON products are simulated and are not durable records.

## Explore GraphQL schemas

Both connections include public SDL snapshots retrieved on 2026-10-20. Requests are linked to their connection for completion and schema-aware diagnostics. Open the connection and use Reload when you want a fresh introspection snapshot. Countries supplies `ID` codes such as `UA`; GraphQLPlaceholder uses `Int` IDs such as `1`.

**Multiple named operations** defaults to Continents; select Languages to run the other operation. **Invalid field expected error** deliberately references an unknown field. Repair it by replacing `fieldThatDoesNotExist` with `name`. The other negative example returns `data.country: null`, which is different from a transport failure. GraphQLPlaceholder mutation examples are provided for manual use; treat their data as simulated rather than persistent.

## Practice local secrets manually

The public project defines two missing sensitive variables. Their YAML contains references only. Provision them in **Workspace settings → Secrets and encryption → Manage secrets**:

| Variable | Synthetic value |
| --- | --- |
| demo_token | purr-demo-token |
| demo_password | purr-demo-password |

These strings are intentionally public fixtures, not credentials to any account. The bearer and API-key examples send and echo the dummy token. The Basic example checks username `purr-demo` and the dummy password. Never substitute production credentials into these echo requests.

1. Before provisioning, send a secrets-lab request and inspect the missing-secret message.
2. Save the synthetic values locally and send again.
3. Export only the selected demo secrets to a password-protected `.purrsecrets` file, outside this folder.
4. On a separate installation/profile, open a clone with the same workspace identity and confirm that values are missing.
5. Import the package through **Secrets and encryption → Import secrets**, preview the matching declarations and apply the selected values.
6. Retry the request. Optionally test a wrong package password or Keep/Replace behavior with an existing synthetic value.

Git carries declarations, not the local values. This workspace does not include a prepared secret package, recovery keys or imported values. Keep transfer files outside the repository even though `.gitignore` excludes common sensitive file types.

## Practice Git manually

No Git repository, remote, branches or conflicts are set up by this workspace content. When you are ready, place the folder in your own test repository and commit a baseline.

For a clean merge, edit **Independent change target** on one branch and another request on the other branch. For a conflict, edit the `color` query parameter of **Conflict practice target** to different values on two branches, save and commit each, then merge. Review the conflict in Purr and verify the final request and YAML. Keep IDs unchanged when editing existing resources.

To compare incoming changes with an unsaved editor, keep a local edit open in Purr and update the same canonical request from a separate Git operation. Purr can then present the incoming saved version alongside the unsaved work. Use a disposable branch for this exercise.

## HTTP behavior and limits

The HTTPbin cookie pair is ordered: **Set demo cookie**, then **Read demo cookie**. Only these examples opt into sending the workspace cookie jar; the other fixtures avoid inherited cookies and authentication. Cookie values and response history stay local. Status 404, status 500, timeout and the invalid GraphQL field are intentional negative cases. An unavailable service, proxy HTML or rate-limit response is a different outcome; retry later rather than changing the expected result to match it. Use these APIs for manual learning, not load testing.

Each request has its own explicit auth and headers so unrelated workspace defaults cannot silently alter it. The secrets lab is optional; it does not block the other folders. Pinned schemas are public source snapshots, not user data. Standard workspace export includes canonical resources and referenced assets; copy this README and `.gitignore` separately if your export omits ancillary files.

## API references

- [DummyJSON documentation](https://dummyjson.com/docs)
- [PokeAPI documentation and fair use](https://pokeapi.co/docs/v2)
- [Countries GraphQL endpoint](https://countries.trevorblades.com/)
- [GraphQLPlaceholder playground](https://graphqlplaceholder.vercel.app/graphql)
- [HTTPbin endpoint reference](https://httpbin.org/)
- [Postman Echo](https://postman-echo.com/)

Public APIs and their returned data remain subject to their providers' terms and availability.
