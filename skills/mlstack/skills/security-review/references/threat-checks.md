# Threat checks

Select classes that cross a real boundary in this target. Trace the strongest
existing control before making a finding. These prompts adapt Cloudflare's
attack classes; they are a coverage aid, not a list of automatic violations.

## Identity, authorization, and isolation

- Trace identity from authentication through each resource operation. Check
  ownership and tenant scope on reads, writes, lists, batch actions, and jobs.
- Compare alternate routes to the same effect. Check field overrides, role
  changes, revocation, stale caches, delegated scopes, and service identities.
- Inspect session, token, recovery, linking, redirect, and callback rules where
  they apply. Verify issuer, audience, expiry, signature, and replay controls.
- Follow private data into caches, search, analytics, exports, backups, restore,
  deletion, and retention. A later lifecycle step must preserve current access.

## Input to sink

- Follow values, keys, headers, and stored data into queries, commands,
  templates, raw HTML, logs, parsers, and deserializers. Match escaping or
  parameterization to the exact sink and context.
- Check path containment, symlinks, archives, temporary files, and check/use
  races. Confirm the final opened object satisfies the claimed boundary.
- Trace outbound URLs through redirects, address resolution, proxies, and
  credentials. Confirm destination restrictions survive each step.
- For native targets, inspect lengths, integer conversions, ownership,
  lifetime, concurrency, and privileged interfaces reachable by untrusted data.

## Web and clients

- Check DOM insertion, origin and message validation, CSRF, CORS, cookie scope,
  browser storage, webview bridges, extensions, and service workers in scope.
- Compare HTTP parsing and cache identity across proxy and origin. Identify
  an actual disagreement before claiming request smuggling or cache poisoning.
- Inspect public errors and side effects for unauthorized data disclosure.

## Business state and resources

- Test the model against skipped steps, replay, rollback, partial failure,
  concurrency, negative quantities, overflow, rounding, expiry, and missing config.
- Follow who pays for attacker-triggered CPU, memory, disk, queues, network,
  database work, or model calls. Identify the absent bound and shared impact.
- Check transaction, idempotency, and retry semantics around consequential effects.

## Secrets, dependencies, and deployment

- Check secret handling in source, logs, errors, generated assets, CI artifacts,
  URLs, and client responses. Keep secret values out of reports.
- Inspect cryptographic use against the required property: unpredictability,
  authenticity, confidentiality, key ownership, and safe failure behavior.
- Inspect dependency resolution, lockfiles, install hooks, untrusted PR workflows,
  release permissions, artifact promotion, signing, and updates. Trace how an
  attacker-controlled artifact reaches a trusted execution or release step.
- For cloud and containers, inspect IAM, workload identity, mounts, metadata,
  ingress, network policy, and secret exposure. Distinguish checked configuration
  from assumptions about the live environment.

## AI and tools

- Separate user authority from retrieved text, documents, memory, and tool output.
  Trace whether untrusted content can select an action or change its arguments.
- Check tool identity, schema, capability scope, approval binding, and whether
  authorization applies to the exact action and current arguments.
- Follow model output into commands, queries, HTML, files, or external messages.
  Model output needs the same sink-specific controls as other untrusted input.
- Check persistent poisoning, cross-user memory, retrieval scope, data leakage,
  runaway tool loops, and operator-owned spend.

## Cross-boundary chains

Check whether one component's output gives less assurance than the next
component assumes. Include normalization, truncation, serialization, stale
state, restore, retries, and delegation. Establish every prerequisite and
effect in a claimed chain; a plausible narrative is not evidence.
