# `wasi-cloud-core`

A proposed [WebAssembly System Interface](https://github.com/WebAssembly/WASI) API.

### Current Phase

`wasi-cloud-core` is currently in [Phase 1](https://github.com/WebAssembly/WASI/blob/main/Proposals.md#phase-1---feature-proposal-cg).

### Champions

- [Dan Chiarlone](https://github.com/danbugs)
- [David Justice](https://github.com/devigned)
- [Jiaxiao Zhou](https://github.com/Mossaka)
- [Taylor Thomas](https://github.com/thomastaylor312)

### Phase 4 Advancement Criteria

`wasi-cloud-core` should have at least two implementations (i.e., from service providers, and or cloud providers), and, at the very minimum, pass the testsuite for Windows, Linux, and MacOS.

## Table of Contents [if the explainer is longer than one printed page]

- [Introduction](#introduction)

### Introduction

> Note: This proposal currently only contains the proposed WIT interfaces; more work is necessary to fully document the proposal.

`wasi-cloud-core` World aims to provide a generic way for WASI applications to interact with services. This world is created by including many other WASI worlds being proposed in the WASI community. The following is a list of the worlds that are currently being included in `wasi-cloud-core`.

- [wasi-keyvalue](https://github.com/WebAssembly/wasi-keyvalue)
- [wasi-messaging](https://github.com/WebAssembly/wasi-messaging)
- [wasi-http](https://github.com/WebAssembly/wasi-http)
- [wasi-runtime-config](https://github.com/WebAssembly/wasi-runtime-config)
- [wasi-sql](https://github.com/WebAssembly/wasi-sql)
- [wasi-blob-store](https://github.com/WebAssembly/wasi-blob-store)

This list of services provide a set of capabilities that are common to many applications. Examples: handling an HTTP request, responding to a pub/sub message, storing a key/value pair, etc. It targets a wide range of applications, from long-running services to "bursty workloads" like Edge functions, serverless functions or Cloud events.

This set of capabilities are derived from the best practices of building distributed applications. It is not intended to be a complete set of capabilities, but rather are needed by 80% of applications.
