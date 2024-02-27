---
title: "DNSSEC Cryptographic Algorithms"
abbrev: title
docname: draft-hardaker-dnsop-rfc8624-bis-01
category: info
ipr: trust200902

stand_alone: yes
pi: [toc, sortrefs, symrefs, docmapping]

author:
  -
    ins: W. Hardaker
    name: Wes Hardaker
    org: USC/ISI
    email: ietf@hardakers.net
  -
    ins: W. Kumari
    name: Warren Kumari
    org: Google
    email: warren@kumari.net

normative:
  RFC2119:
  RFC8174:
  RFC8624:
  DNSKEY-IANA:
    author:
      name: IANA
    target: "https://www.iana.org/assignments/dns-sec-alg-numbers/dns-sec-alg-numbers.xhtml"
    title: Domain Name System Security (DNSSEC) Algorithm Numbers
  DS-IANA:
    author:
      name: IANA
    target: "http://www.iana.org/assignments/ds-rr-types"
    title: Delegation Signer (DS) Resource Record (RR) Type Digest Algorithms
  TLS-ciphersuites:
    author:
      name: IANA
    target: "https://www.iana.org/assignments/tls-parameters/tls-parameters.xhtml#tls-parameters-4"
    title: Transport Layer Security (TLS) Parameters

informative:
  RFC4034:
  RFC5155:
  RFC5702:
  RFC5933:
  RFC6605:
  RFC6781:
  RFC7583:
  RFC8080:

--- abstract

   [EDITOR NOTE: This document does not change the status (MUST, MAY,
   RECOMMENDED, etc) of any of the algorithms listed in [RFC8624]; that is
   the work of future documents.  Instead, this document moves
   the canonical list of algorithms from [RFC8624] to an IANA registry.
   This is done for two reasons: 1) to allow the list to be updated more
   easily, and, much more importantly, 2) to allow the list to be more
   easily referenced.]

   The DNSSEC protocol makes use of various cryptographic algorithms to provide
   authentication of DNS data and proof of non-existence.  To ensure
   interoperability between DNS resolvers and DNS authoritative servers, it is
   necessary to specify both a set of algorithm implementation requirements and
   usage guidelines to ensure that there is at least one algorithm that all
   implementations support.  This document updates [RFC8624] by moving the
   canonical source of algorithm implementation requirements and usage guidance
   for DNSSEC from [RFC8624] to an IANA registry.  Future extensions
   to this registry can be made under new, incremental update RFCs.

--- middle

# Introduction

   DNS Security Extensions (DNSSEC) [RFC4034] is used to provide
   authentication of DNS data.  The DNSSEC signing algorithms are
   defined by various RFCs, including [RFC4034], [RFC5155], [RFC5702],
   [RFC5933], [RFC6605], [RFC8080].  To ensure interoperability, a set
   of "mandatory-to-implement" DNSKEY algorithms are defined in
   [RFC8624].  To make the current status of the algorithms
   more easily accessible and understandable, this document moves the
   canonical status of the algorithms from [RFC8624] to the IANA DNSSEC
   algorithm registries.  [ Editor: This is similar to the process used
   for the [TLS-ciphersuites] registry, where the canonical list of
   ciphersuites is in the IANA registry, and the RFCs reference the IANA
   registry. ]

   This document simply moves the canonical list of algorithms from [RFC8624] to
   the IANA registry, and defines the registry policies for updating
   the registry. It does not change the
   status of any of the algorithms listed in [RFC8624]; this is left to
   future documents.

##  Terminology

   TBD

   [RFC2119] considers the term SHOULD equivalent to RECOMMENDED, and
   SHOULD NOT equivalent to NOT RECOMMENDED.  The authors of this
   document have chosen to use the terms RECOMMENDED and NOT
   RECOMMENDED, as this more clearly expresses the recommendations to
   implementers.

##  Updating Algorithm Implementation Requirements and Usage Guidance

   The field of cryptography evolves continuously.  New, stronger
   algorithms appear, and existing algorithms may be found to be less
   secure then originally thought.  Therefore, algorithm
   implementation requirements and usage guidance need to be updated
   from time to time in order to reflect the new reality.
   Cryptographic algorithm choices implemented in and required by
   software must be conservative to minimize the risk of algorithm
   compromise.

##  Updating Algorithm Requirement Levels

   By the time a DNSSEC cryptographic algorithm is made mandatory-to-implement,
   it should already be available in most implementations. This document
   attempts to identify and introduce those algorithms for future
   mandatory-to-implement status.  There is no guarantee that algorithms in use
   today will become mandatory to implement in the future.  Published
   algorithms are continuously subjected to cryptographic attack and may become
   too weak, or even be completely broken, before this document is updated.

   It is expected that the deprecation of an algorithm will be performed
   gradually.  This provides time for implementations to update
   their implemented algorithms while remaining interoperable.  Unless
   there are strong security reasons, an algorithm is expected to be
   downgraded from MUST to NOT RECOMMENDED or MAY, instead of directly
   from MUST to MUST NOT.  Similarly, an algorithm that has not been
   mentioned as mandatory-to-implement is expected to be first introduced
   as RECOMMENDED instead of a MUST.

   Since the effect of using an unknown DNSKEY algorithm is that the
   zone is treated as insecure, it is recommended that algorithms
   downgraded to NOT RECOMMENDED or lower not be used by authoritative
   nameservers and DNSSEC signers to create new DNSKEY's.  This will
   allow for deprecated algorithms to become used less and less over
   time.  Once an algorithm has reached a sufficiently low level of
   deployment, it can be marked as MUST NOT, so that recursive resolvers
   can remove support for validating it.

   Validating recursive resolvers are encouraged to retain support for all
   algorithms not marked as MUST NOT.

##  Document Audience

   The recommendations of this document mostly target DNSSEC
   implementers, as implementations need to meet both high security
   expectations as well as high interoperability between various vendors
   and with different versions.  Interoperability requires a smooth
   transition to more secure algorithms.  This perspective may differ
   from that of a user who wishes to deploy and configure DNSSEC
   with only the safest algorithm.  On the other hand, the comments and
   recommendations in this document are also expected to be useful for
   such users.

##  Conventions Used in This Document

   The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
   "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this
   document are to be interpreted as described in [RFC2119] [RFC2119]
   [RFC8174] when, and only when, they appear in all capitals, as shown
   here.

# Adding "Recommended" Column to IANA tables

   Per this document, "Recommended" columns have been added to the
   following DNSSEC algorithm tables registered with IANA:

   |-------------------------------------------------------------------------|
   | Table                               | Column added                      |
   |-------------------------------------------------------------------------|
   | DNSKEY algorithms                   | Recommended for DNSSSEC Signing   |
   | DNSKEY algorithms                   | Recommended for DNSSSEC Validation|
   | Delegation Signer Digest Algorithms | Recommended                       |
   |-------------------------------------------------------------------------|

   Adding a Recommended parameter of "Y" to a registry or updating a
   parameter to "Recommended" status requires Standards Action.  Not
   all parameters defined in Standards Track documents need to be
   marked as "Recommended".  If an item is not marked as "Recommended"
   (i.e., "N"), it does not necessarily mean that it is flawed;
   rather, it indicates that the item either has not been through the
   IETF consensus process, has limited applicability, or is intended
   only for specific use cases.

   The following sections state the initial values to be populated
   into these rows, with values transcribed from [RFC8624].

#  DNSKEY Algorithm Recommendation Column Values

   Initial recommendation columns of implementation recommendations
   for DNSKEY algorithms.

    |--------|--------------------|-----------------|-------------------|
    |        |                    | Recommended for | Recommended for   |
    | Number | Mnemonics          | DNSSEC Signing  | DNSSEC Validation |
    |--------|--------------------|-----------------|-------------------|
    | 1      | RSAMD5             | MUST NOT        | MUST NOT          |
    |--------|--------------------|-----------------|-------------------|
    | 3      | DSA                | MUST NOT        | MUST NOT          |
    |--------|--------------------|-----------------|-------------------|
    | 5      | RSASHA1            | MUST NOT        | SHOULD NOT        |
    |--------|--------------------|-----------------|-------------------|
    | 6      | DSA-NSEC3-SHA1     | MUST NOT        | MUST NOT          |
    |--------|--------------------|-----------------|-------------------|
    | 7      | RSASHA1-NSEC3-SHA1 | MUST NOT        | SHOULD NOT        |
    |--------|--------------------|-----------------|-------------------|
    | 8      | RSASHA256          | MUST            | MUST              |
    |--------|--------------------|-----------------|-------------------|
    | 10     | RSASHA512          | NOT             | MUST              |
    |        |                    | RECOMMENDED     |                   |
    |--------|--------------------|-----------------|-------------------|
    | 12     | ECC-GOST           | MUST NOT        | MUST NOT          |
    |--------|--------------------|-----------------|-------------------|
    | 13     | ECDSAP256SHA256    | MUST            | MUST              |
    |--------|--------------------|-----------------|-------------------|
    | 14     | ECDSAP384SHA384    | MAY             | RECOMMENDED       |
    |--------|--------------------|-----------------|-------------------|
    | 15     | ED25519            | RECOMMENDED     | RECOMMENDED       |
    |--------|--------------------|-----------------|-------------------|
    | 16     | ED448              | MAY             | RECOMMENDED       |
    |--------|--------------------|-----------------|-------------------|

                                    Table 1

#  DS and CDS Algorithms

   Initial recommendation columns of implementation recommendations
   for DS/CDS algorithms.

    |--------|-----------------|-------------------|-------------------|
    | Number | Mnemonics       | DNSSEC Delegation | DNSSEC Validation |
    |--------|-----------------|-------------------|-------------------|
    | 0      | NULL (CDS only) | MUST NOT \[*\]    | MUST NOT \[*\]    |
    |--------|-----------------|-------------------|-------------------|
    | 1      | SHA-1           | MUST NOT          | SHOULD NOT        |
    |--------|-----------------|-------------------|-------------------|
    | 2      | SHA-256         | MUST              | MUST              |
    |--------|-----------------|-------------------|-------------------|
    | 3      | GOST R 34.11-94 | MUST NOT          | MUST NOT          |
    |--------|-----------------|-------------------|-------------------|
    | 4      | SHA-384         | MAY               | RECOMMENDED       |
    +--------+-----------------+-------------------+-------------------+

                                    Table 2


#  Security Considerations

   The security of cryptographic systems depends on both the strength of
   the cryptographic algorithms chosen and the strength of the keys used
   with those algorithms.  The security also depends on the engineering
   of the protocol used by the system to ensure that there are no non-
   cryptographic ways to bypass the security of the overall system.

   This document concerns itself with the selection of cryptographic
   algorithms for the use of DNSSEC, specifically with the selection of
   "mandatory-to-implement" algorithms.  The algorithms identified in
   this document as MUST or RECOMMENDED to implement are not known to be
   broken at the current time, and cryptographic research so far leads
   us to believe that they are likely to remain secure into the
   foreseeable future.  However, this isn't necessarily forever, and it
   is expected that new revisions of this document will be issued from
   time to time to reflect the current best practices in this area.

   Retiring an algorithm too soon would result in a zone signed with the
   retired algorithm being downgraded to the equivalent of an unsigned
   zone.  Therefore, algorithm deprecation must be done very slowly and
   only after careful consideration and measurement of its use.

#  Operational Considerations

   DNSKEY algorithm rollover in a live zone is a complex process.  See
   [RFC6781] and [RFC7583] for guidelines on how to perform algorithm
   rollovers.

   DS algorithm rollover in a live zone is also a complex process.
   Upgrading algorithm at the same time as rolling the new KSK key will
   lead to DNSSEC validation failures, and users MUST upgrade the DS
   algorithm first before rolling the Key Signing Key.

#  Implementation Report

##  DNSKEY Algorithms

   The following table contains the status of support in the open-source
   DNS signers and validators in the current released versions as of the
   time writing this document.  Usually, the support for specific
   algorithm has to be also included in the cryptographic libraries that
   the software use.

    |--------------------|------|------|---------|----------|---------|
    | Mnemonics          | BIND | Knot | OpenDNS | PowerDNS | Unbound |
    |                    |      | DNS  |         |          |         |
    |--------------------|------|------|---------|----------|---------|
    | RSAMD5             | Y    | N    | Y       | N        | N       |
    |--------------------|------|------|---------|----------|---------|
    | DSA                | Y    | N    | Y       | N        | Y       |
    |--------------------|------|------|---------|----------|---------|
    | RSASHA1            | Y    | Y    | Y       | Y        | Y       |
    |--------------------|------|------|---------|----------|---------|
    | DSA-NSEC3-SHA1     | Y    | N    | Y       | N        | Y       |
    |--------------------|------|------|---------|----------|---------|
    | RSASHA1-NSEC3-SHA1 | Y    | Y    | Y       | Y        | Y       |
    |--------------------|------|------|---------|----------|---------|
    | RSASHA256          | Y    | Y    | Y       | Y        | Y       |
    |--------------------|------|------|---------|----------|---------|
    | RSASHA512          | Y    | Y    | Y       | Y        | Y       |
    |--------------------|------|------|---------|----------|---------|
    | ECC-GOST           | N    | N    | Y       | Y        | Y       |
    |--------------------|------|------|---------|----------|---------|
    | ECDSAP256SHA256    | Y    | Y    | Y       | Y        | Y       |
    |--------------------|------|------|---------|----------|---------|
    | ECDSAP384SHA384    | Y    | Y    | Y       | Y        | Y       |
    |--------------------|------|------|---------|----------|---------|
    | ED25519            | Y    | Y    | N       | Y        | Y       |
    |--------------------|------|------|---------|----------|---------|
    | ED448              | N    | N    | N       | Y        | Y       |
    |--------------------|------|------|---------|----------|---------|

                                  Table 3

#  IANA Considerations

   TODO: That's the whole point of this document, right? :-P

  The IANA is requested to update the [DNSKEY-IANA] and [DS-IANA] registries
  as follows:

  * Add "Recommended for DNSSSEC Signing" and "Recommended for DNSSSEC
    Validation" columns to the DNS Security Algorithm Numbers registry
    ([DNSKEY-IANA]) and populate these columens with the values from Table 1.

  * Add a "Recommended" column to the DS and CDS Algorithms registry ([DS-IANA])
    and populate this column with the values from Table 2.

  * Update the registration policy for the [DNSKEY-IANA] registry to be
    "Standards Action or IESG Approval". {Ed: I'm not sure if this is the right
    policy, and this requires a good discussion with the WG. The purpose of
    much of this document is so that we can introduce TheNextBestAlgorithm by
    documenting TheNextBestAlgorithm in a new RFC and having it updating the
    IANA registry, instead of having to update RFC8624-bis-bis-bis-bis. We
    also, obviously, don't want someone to do something silly and mark an
    algorithm as "Recommended" without a good reason. This implies Standards
    Track. On the other hand we want to allow the ISE to add new algorithms
    (like the latest GOST algorithm), and, rightly or wrongly, the ISE doesn't
    publishes Std Track RFCs. Standards Action or IESG Approval seems like a
    reasonable compromise, but I'm not sure if it's the right one. We hope to
    present this to the WG at IEFT119 and get feedback.}


#  Acknowledgements

  This document is based on, and extends, RFC 8624, which was authored by
  Paul Wouters, and Ondrej Sury.


--- back

# ChangeLog

## Changes since RFC8624

   The following changes were made since RFC8624:

   *  Deprecated validation of all SHA-1 algorithms to SHOULD NOT.

   *  Deprecated validation all listed GOST algorithms to MUST NOT.

   *  Merged in RFC9157 updates.

   *  Added Wes Hardaker, Warren Kumari as authors.
