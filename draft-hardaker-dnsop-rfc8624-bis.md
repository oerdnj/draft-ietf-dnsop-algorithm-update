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

informative:
  RFC4034:
  RFC5155:
  RFC5702:
  RFC5933:
  RFC6605:
  RFC6781:
  RFC6979:
  RFC6986:
  RFC7091:
  RFC7344:
  RFC7583:
  RFC8032:
  RFC8078:
  RFC8080:

--- abstract

   [EDITOR NOTE: This document does not change the status (MUST, MAY,
   RECOMMENDED, etc) of any of the algorithms listed in RFC8624; that is
   the work of future documents.  Instead, this document moves
   the canonical list of algorithms from RFC8624 to an IANA registry.
   This is done for two reasons: 1) to allow the list to be updated more
   easily, and, much more importantly, 2) to allow the list to be more
   easily referenced.]  The DNSSEC protocol makes use of various
   cryptographic algorithms to provide authentication of DNS
   data and proof of non-existence.  To ensure interoperability between
   DNS resolvers and DNS authoritative servers, it is necessary to
   specify a set of algorithm implementation requirements and usage
   guidelines to ensure that there is at least one algorithm that all
   implementations support.  This document updates RFC8624 by moving the
   canonical source of algorithm implementation requirements and usage
   guidance for DNSSEC from RFC8624 to an IANA registry.

--- middle

# Introduction

   DNS Security Extensions (DNSSEC) [RFC4034] is used to provide
   authentication of DNS data.  The DNSSEC signing algorithms are
   defined by various RFCs, including [RFC4034], [RFC5155], [RFC5702],
   [RFC5933], [RFC6605], [RFC8080].  To ensure interoperability, a set
   of "mandatory-to-implement" DNSKEY algorithms are defined in
   [RFC8624].  To make the current status of the algorithms
   more easily accessible and understandable, this document moves the
   canonical status of the algorithms from RFC8624 to the IANA DNSSEC
   algorithm registries.  [ Editor: This is similar to the process used
   for the TLS ciphersuites - https://www.iana.org/assignments/tls-
   parameters/tls-parameters.xhtml#tls-parameters-4 ]

##  Terminology

   TBD

##  Updating Algorithm Implementation Requirements and Usage Guidance

   The field of cryptography evolves continuously.  New, stronger
   algorithms appear, and existing algorithms are found to be less secure
   then originally thought.  Therefore, algorithm implementation
   requirements and usage guidance need to be updated from time to time
   to reflect the new reality.  The algorithm choices must be
   conservative to minimize the risk of algorithm compromise.

##  Updating Algorithm Requirement Levels

   The mandatory-to-implement algorithm of tomorrow should already be
   available in most implementations of DNSSEC by the time it is made
   mandatory.  This document attempts to identify and introduce those
   algorithms for future mandatory-to-implement status.  There is no
   guarantee that algorithms in use today will become mandatory to implement
   in the future.  Published algorithms are continuously subjected to
   cryptographic attack and may become too weak, or even be completely
   broken, before this document is updated.

   [ [TODO (WK): This section needs to be updated. ]] This document
   provides recommendations with respect to mandatory-to-implement
   algorithms, algorithms so weak that they cannot be recommended, and
   algorithms defined in RFCs that are not on the standards track.  Any
   algorithm listed in the [DNSKEY-IANA] and [DS-IANA] registries that
   are not mentioned in this document MAY be implemented.  For
   clarification and consistency, an algorithm will be specified as MAY
   in this document only when it has been downgraded from a MUST or a
   RECOMMENDED to a MAY.

   [TODO (WK): Ditto! ] Although this document's primary purpose is to
   update algorithm recommendations to keep DNSSEC authentication secure
   over time, it also aims to do so in such a way that DNSSEC
   implementations remain interoperable.  DNSSEC interoperability is
   addressed by an incremental introduction or deprecation of
   algorithms.

   [RFC2119] considers the term SHOULD equivalent to RECOMMENDED, and
   SHOULD NOT equivalent to NOT RECOMMENDED.  The authors of this
   document have chosen to use the terms RECOMMENDED and NOT
   RECOMMENDED, as this more clearly expresses the recommendations to
   implementers.

   It is expected that the deprecation of an algorithm will be performed
   gradually.  This provides time for various implementations to update
   their implemented algorithms while remaining interoperable.  Unless
   there are strong security reasons, an algorithm is expected to be
   downgraded from MUST to NOT RECOMMENDED or MAY, instead of to MUST
   NOT.  Similarly, an algorithm that has not been mentioned as
   mandatory-to-implement is expected to be introduced with a
   RECOMMENDED instead of a MUST.

   Since the effect of using an unknown DNSKEY algorithm is that the
   zone is treated as insecure, it is recommended that algorithms
   downgraded to NOT RECOMMENDED or lower not be used by authoritative
   nameservers and DNSSEC signers to create new DNSKEY's.  This will
   allow for deprecated algorithms to become less and less common over
   time.  Once an algorithm has reached a sufficiently low level of
   deployment, it can be marked as MUST NOT, so that recursive resolvers
   can remove support for validating it.

   Recursive nameservers are encouraged to retain support for all
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

#  DS and CDS Algorithms

   Initial recommendation columns of implementation recommendations
   for DS/CDS algorithms.

   |--------|-----------------|-------------------|-------------------|
   | Number | Mnemonics       | DNSSEC Delegation | DNSSEC Validation |
   |--------|-----------------|-------------------|-------------------|
   | 0      | NULL (CDS only) | MUST NOT [*]      | MUST NOT [*]      |
   |--------|-----------------|-------------------|-------------------|
   | 1      | SHA-1           | MUST NOT          | SHOULD NOT        |
   |--------|-----------------|-------------------|-------------------|
   | 2      | SHA-256         | MUST              | MUST              |
   |--------|-----------------|-------------------|-------------------|
   | 3      | GOST R 34.11-94 | MUST NOT          | MUST NOT          |
   |--------|-----------------|-------------------|-------------------|
   | 4      | SHA-384         | MAY               | RECOMMENDED       |
   +--------+-----------------+-------------------+-------------------+

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

   This document makes no requests of IANA.

#  Acknowledgements

   This document borrows text from RFC 4307 by Jeffrey I.  Schiller of
   the Massachusetts Institute of Technology (MIT) and the 4307bis
   document by Yoav Nir, Tero Kivinen, Paul Wouters and Daniel Migault.
   Much of the original text has been copied verbatim.

   We wish to thank Michael Sinatra, Roland van Rijswijk-Deij, Olafur
   Gudmundsson, Paul Hoffman and Evan Hunt for their imminent feedback.

   Kudos to Roy Arends for bringing the DS rollover issue to the
   daylight.

--- back

# ChangeLog

## Changes since RFC8624

   The following changes were made since RFC8624:

   *  Deprecated validation of all SHA-1 algorithms to SHOULD NOT.

   *  Deprecated validation all listed GOST algorithms to MUST NOT.

   *  Merged in RFC9157 updates.

   *  Added Wes Hardaker as an author
