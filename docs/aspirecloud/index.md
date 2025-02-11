---
layout: default
title: Welcome to AspireGuide - AspireCloud
permalink: /aspirecloud/
---

## What is AspireCloud?

[AspireCloud](https://github.com/aspirepress/AspireCloud) is an open source project that functions as a CDN and a set of API endpoints for distributing WordPress assets (themes, plugins, core) to users of the [AspirePress Update](/aspireupdate/) plugin.

The following is the architecture of AspireCloud federation/defederation model. In Phase 1, the federation concept is not yet supported.

```mermaid
---
config:
  theme: base
---
flowchart TD
    Server2D["AspireCloud at AspirePress"] <-- federates with ---> Server2A["AspireCloud at YourHostWPE.com"] & Server2C["AspireCloud at YourHostABC.com"]
    Server2D --- UserM(("WP Website A")) & UserN(("WP Website B")) & UserO(("WP Website C"))
    Server2A --- UserG(("WP Website D")) & UserH(("WP Website E"))
    Server2A <-- federates with ---> Server2C

    Server2C --- UserK(("WP Website F")) & UserL(("WP Website G"))

    Server2B["AspireCloud at CompanyQED.com"] --- User(("Website H"))
    Server2B x-- defederated with --x Server2D

    style Server2D fill:#A0b9f3,stroke:#333,rx:10,ry:10
    style Server2A fill:#A0b9f3,stroke:#333,rx:10,ry:10
    style Server2C fill:#A0b9f3,stroke:#333,rx:10,ry:10
    style Server2B fill:#A0b9f3,stroke:#333,rx:10,ry:10
```


## How to install AspireCloud
[Clone and Install AspireCloud](https://github.com/aspirepress/AspireCloud?tab=readme-ov-file#quick-start)

### Configuration
- A complete REST API for AspireCloud including federation/defederation
- An interoperability specification with other repository projects

