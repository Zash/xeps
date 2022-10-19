---
abstract: This documents describes a mechanism for communicating stanza
  size limits across streams in order to help avoid reaching those
  limits.
author:
- "Kim Alvefur <zash@zash.se> <xmpp:zash@zash.se>"
number: xxxx
revision:
- date: 2021-08-20
  initials: ka
  remark:
  - Early draft
  version: 0.0.1
- date: 2021-08-25
  initials: ka
  remark:
  - more work
- date: 2021-08-28
  initials: ka
  remark:
  - more words
- date: 2022-06-01
  initials: ka
  remark:
  - word tweaks
  - element name and namespace un-TDB'd
shortname: NOT_YET_ASSIGNED
sig: Standards
status: ProtoXEP
title: Stanza size limit discovery
type: Standards Track
---

# Introduction {#intro}

This documents describes a mechanism for communicating the stanza size
limit that is in effect on a particular stream, in order to allow the
other party to avoid reaching those limits.

## Problem statement

Where stanza size limits have been deployed, very often this leads to
problems with large stanzas causing connection outages, most often
&xep0084; and &xep0053; result stanzas.

If stanza size limit violations are met with stream errors then this may
lead to temporary connection outage, which may a few seconds to recover
from.

Especially vCard and Avatar stanzas may be very large and sometimes
exceed the stanza size limit imposed.

# Requirements {#reqs}

-   Enable discovery of the stanza size limit in use on a stream.

# Glossary

OPTIONAL.

# Use Cases {#usecases}

-   An XMPP client could attempt to apply more compression if it sees
    that an avatar it is about to upload would be too large.
-   A PubSub server could limit the number of items in an `<items/>`
    query to ensure it can be delivered.

# Business Rules {#rules}

If after serialization to XML a stanza is too large, like, don't send
it. Synthesize an error condition, most likely a (modify,
policy-violation), and pretend the remote entity replied with this.

# Implementation Notes {#impl}

Something about margins, due to variations in XML serialization, added
attributes (e.g. the `from` attribute stamped by servers) or elements
(delay tags)

Because the stanza size limit is known ahead of time, entities can check
this against stanzas they are about to send and take appropriate action,
such as preemptively pretending that the stanza was rejected by the
receiving entity.

A client could for example try to apply more compression to an avatar or
ask the user to select a smaller picture.

# Accessibility Considerations {#access}

OPTIONAL.

Not relevant?

# Internationalization Considerations {#i18n}

OPTIONAL.

Not relevant?

# Determining support

The responding entity advertises the stanza size limit it enforces by
including it as an integer in a stream feature element `limit` in the
namespace `urn:xmpp:stanza-size`. An example of stream features prior to
authentication follows:

``` {.xml .example}
<stream:features>
  <mechanisms xmlns="urn:ietf:params:xml:ns:xmpp-sasl">
    <mechanism>SCRAM-SHA-1</mechanism>
    <mechanism>PLAIN</mechanism>
  </mechanisms>
  <limit xmlns="urn:xmpp:stanza-size">10000</limit>
</stream:features>
```

Entities may wish to have higher limits after authentication and would
advertise it the same way after the stream restart:

``` {.xml .example}
<stream:features>
  <bind xmlns="urn:ietf:params:xml:ns:xmpp-bind">
    <required/>
  </bind>
  <limit xmlns="urn:xmpp:stanza-size">262144</limit>
</stream:features>
```

When the receiving entity indicates that it supports stanza size limits,
the initiating entity MAY indicate its own limit by sending a stream
element:

``` {.xml .example}
<limit xmlns="urn:xmpp:stanza-size">262144</limit>
```
# Security Considerations {#security}

REQUIRED.

Very large stanzas may incur memory and processing costs on the
receiving entity. Advertising the actual limits could inform an attacker
of how large a stanza to construct in order to maximize e.g. DoS
effectiveness. Best combined with network level rate limits on raw
bytes.

Also see https://xmpp.org/rfcs/rfc6120.html#rfc.section.13.12

TBD Recommendations for limits?

# IANA Considerations {#iana}

None.

# XMPP Registrar Considerations {#registrar}

The XMPP Registrar is asked to include the `<limit/>` stream feature
`<limit xmlns="urn:xmpp:stanza-size">ineger</limit>` in the relevant
registry.

# Design Considerations {#design}

RECOMMENDED.

Design? I just typed words and code into my computer!

# Open Issues

-   How should Bi-directionality of streams, especially when &xep0288; is used.
-   Should the information be included in &xep0030; ?

# XML Schema {#schema}

REQUIRED for protocol specifications.

```
type: integer
minimum: 10000
xml:
  name: limit
  namespace: urn:xmpp:stanza-size
```
