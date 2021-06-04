---
abstract: This specification describes extended error conditions for
  server-to-server failure reasons.
author:
- "Kim Alvefur <zash@zash.se> <xmpp:zash@zash.se>"
dependencies:
- XMPP Core
number: xxxx
revision:
- date: 2021-06-04
  initials: ka
  remark:
  - Add stuff
  version: 0.0.2
- date: 2021-02-26
  initials: ka
  remark:
  - First draft.
  version: 0.0.1
approver: Council
shortname: NOT_YET_ASSIGNED
sig: Standards
status: ProtoXEP
title: Extended server-to-server error conditions
type: Standards Track
---

# Introduction {#intro}

XMPP Core defines only two stanza errors for when the error relates to a
server-to-server connectivity failure, namely `<remote-server-not-found/>`{.xml} and
`<remote-server-timeout/>`{.xml}. Especially since the introduction of
mandatory encryption, the possible reasons why a s2s connection could
not be established can be numerous.

TODO: Limit scope to TLS/certificate errors or more general?

## TL;DR

``` xml
<message type="error" id="mGO0" from="juliet@remotehost.example" to="romeo@localhost.localdomain">
  <error type="wait" by="localhost.localdomain">
    <remote-server-timeout xmlns="urn:ietf:params:xml:ns:xmpp-stanzas"/>
    <text xmlns="urn:ietf:params:xml:ns:xmpp-stanzas" xml:lang="en">Remote server's certificate has expired</text>
    <certificate-expired xmlns="urn:xmpp:TBD-EDITOR-FIXME:s2s-error"/>
  </error>
</message>
```

# Requirements {#reqs}

-   Provide entities with more detailed information about what went
    wrong with delivery of a stanza.

# Glossary

OPTIONAL.

# Use Cases {#usecases}

Is it useful to have machine-readable data telling you your message
could not be delivered because the remote server's certificate expired?
I think so.

# Defined Extended Conditions

TODO: Does this need a registry?

`<certificate-expired/>`{.xml}
:   The remote server's certificate has expired.

`<self-signed-certificate/>`{.xml}
:   The remote server uses a self-signed certificate (and the local
    server does not allow this).

`<certificate-not-trusted/>`{.xml}
:   Remote server's certificate is not trusted by the local server, i.e.
    because it is not issued by a trusted certificate authority.

`<certificate-name-mismatch/>`{.xml}
:   Remote server's certificate is not valid for the server name as used
    in the `@to` stream attribute and the hostpart of the JID in the
    stanza that the delivery error relates to.

`<certificate-invalid/>`{.xml}
:   Remote server's certificate could not be validated for some other
    reason. TODO: Leave this out?

# Business Rules {#rules}

These would all accompany a `<remote-server-timeout/>`{.xml} error, with
an `<error>` `@type` attribute of `wait`.

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

One Namespace please.

# Design Considerations {#design}

RECOMMENDED.

# XML Schema {#schema}

REQUIRED for protocol specifications.
