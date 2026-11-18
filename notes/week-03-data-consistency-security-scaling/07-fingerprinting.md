# 07 — Fingerprinting: integrity, deduplication, and device signals

The supplied outline said the screenshot included “fingerprinting” but that scope was unclear. This chapter separates two distinct meanings. They must not be conflated.

## Content fingerprinting

A cryptographic digest of bytes can detect accidental corruption or identify content that has not changed. Pair the digest with expected size, algorithm, and object/version context. Validate on both sides for large or chunked transfer. A hash can support deduplication but is not authorization or proof of who uploaded the object. Avoid treating a plain checksum as protection against a malicious actor who can change both data and checksum; use authenticated transport and a trusted integrity boundary.

## Request fingerprinting for idempotency

An idempotency key is the client's stable operation identity. A request fingerprint (method, route, principal scope, canonical payload) can detect accidental reuse of the same key for a different request. Store the result/status and enforce key scope, atomic uniqueness, and a retention period that covers retry windows. Avoid canonicalization ambiguities and don't use a content hash alone as the request ID.

## Device/browser fingerprinting

Device fingerprinting infers device identity from attributes. Attributes can change or be shared; it is not a definitive identity, authorization control, or standalone cheating detector. If used for abuse/risk signals, assess privacy, transparency, consent, data minimization, retention, false positives, and applicable policy with the responsible privacy/legal team. Prefer explicit device registration and server-side session controls for security-critical identity.

## Practice

For a 1 GB upload, specify hash algorithm, per-chunk and whole-object checks, what is persisted, and behavior on checksum mismatch. For an idempotency key reused with a different payload, define the server response. For device signals, state what decisions they can and cannot trigger.
