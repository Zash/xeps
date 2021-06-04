---
abstract: This specification provides an example of the format for XMPP
  Extension Protocols (XEPs).
author:
- "Kim Alvefur <zash@zash.se> <xmpp:zash@zash.se>"
dependencies:
- XMPP Core
number: xxxx
revision:
- date: 2021-02-26
  initials: ka
  remark:
  - First draft.
  version: 0.0.1
approver: Council
shortname: NOT_YET_ASSIGNED
sig: Standards
status: ProtoXEP
title: XEP Template
type: Standards Track
---

# Introduction {#intro}

Want more detailed s2s errors, especially wrt TLS and certificate
issues.

## TL;DR

``` xml
<message type="error" id="mGO0" from="juliet@remotehost.example" to="romeo@localhost.localdomain">
  <error type="wait" by="localhost.localdomain">
    <remote-server-timeout xmlns="urn:ietf:params:xml:ns:xmpp-stanzas"/>
    <text xmlns="urn:ietf:params:xml:ns:xmpp-stanzas" xml:lang="en">Remote server's certificate has expired</text>
    <certificate-expired xmlns="urn:xmpp:TBD-EDITOR-FIXME:s2s-cert-issues"/>
  </error>
</message>
```

# Requirements {#reqs}

STRONGLY RECOMMENDED.

# Glossary

OPTIONAL.

# Use Cases {#usecases}

STRONGLY RECOMMENDED.

# Business Rules {#rules}

OPTIONAL.

# Implementation Notes {#impl}

OPTIONAL.

# Accessibility Considerations {#access}

OPTIONAL.

# Internationalization Considerations {#i18n}

OPTIONAL.

# Security Considerations {#security}

REQUIRED.

# IANA Considerations {#iana}

REQUIRED.

# XMPP Registrar Considerations {#registrar}

REQUIRED.

# Design Considerations {#design}

RECOMMENDED.

# XML Schema {#schema}

REQUIRED for protocol specifications.
