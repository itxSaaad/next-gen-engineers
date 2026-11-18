# 06 — API protocol comparison

No protocol is universally fastest or best. Choose based on client platforms, query shape, streaming needs, compatibility, operational skill, security, and observability. Keep authentication/authorization, validation, quotas, and versioning explicit whichever protocol is selected.

| Protocol/style | Useful properties | Costs and fit |
|---|---|---|
| REST over HTTP | Resources, standard HTTP semantics, broad tooling/cache support | CRUD and public/client APIs; endpoint responses can require multiple round trips |
| GraphQL | Typed schema; client selects fields and nested response shape | Needs query depth/complexity limits, resolver batching, cache strategy, and careful authorization; useful for varied UI data needs |
| SOAP | XML envelope, extensible messaging framework, formal enterprise contracts | More ceremony/tooling; maintain when required by existing enterprise integration |
| gRPC | Generated typed contracts with Protocol Buffers; unary and streaming RPCs | Strong internal service/client contracts and streaming; browser/proxy interoperability and debugging may need additional setup |

## Decision questions

- Does the desktop/browser client support the transport and streaming model?
- Is the API resource-oriented, client-shaped, or a fixed internal RPC contract?
- How will schema evolution and old client versions work?
- Can responses be cached safely, and where does authorization vary the cache key?
- How will developers inspect requests and operators trace failures?
- What rate/complexity limits prevent abusive or unexpectedly expensive queries?

## References

- [RFC 9110: HTTP semantics](https://datatracker.ietf.org/doc/html/rfc9110)
- [GraphQL: Learn](https://graphql.org/learn/)
- [gRPC introduction](https://grpc.io/docs/what-is-grpc/introduction/)
- [W3C SOAP 1.2](https://www.w3.org/TR/soap12/)
