# Validation notes

The bridge tests in `service.spec.ts` use Vitest and the DeepSeek Harness workspace packages. The upstream project is a package in the DSH monorepo and its `tsconfig.json` references monorepo-relative project paths; this standalone GitHub port does not pretend those workspace references resolve outside a matching Harness checkout.

Run the tests from a compatible DSH workspace with the repository's supported package manager and test configuration. Before release, verify:

- ping responds with HTTP 200 and CORS headers match configuration;
- OPTIONS preflight responds with HTTP 204;
- the SSE endpoint responds with `text/event-stream`;
- session create/prompt/result/cancel work against the target Harness runtime;
- malformed JSON and unknown session IDs fail safely;
- browser-extension interoperability is checked against the matching Better DeepSeek release.

No runtime integration test is claimed by the source-only port commit.
