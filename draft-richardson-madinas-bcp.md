---
title: Best Current Practices for consistent identity in a privacy preserving way
abbrev: MADINAS BCP
docname: draft-richardson-madinas-bcp-latest

stand_alone: true

ipr: trust200902
area: Internet
wg: madinas Working Group
kw: Internet-Draft
cat: std

pi:    # can use array (if all yes) or hash here
  toc: yes
  sortrefs:   # defaults to yes
  symrefs: yes

author:

- ins: M. Richardson
  name: Michael Richardson
  org: Sandelman Software Works
  email: mcr+ietf@sandelman.ca

normative:
  BCP14: RFC8174
  RFC8995:

informative:
  RFC7030:

--- abstract

This document describes the best current practices to identify devices in a post Randomized and Changing MAC address environment.

--- middle

# Introduction

{{?I-D.ietf-madinas-use-cases}} explains the history of L2 addresses.
The unchanging nature of the L2 MAC addresses has created an unwanted public association between devices and users.
A response to this has been deployment of Randomized and Changing MAC addresses (RCM).
The various ways in which can be done has been summarized in {{?I-D.ietf-madinas-mac-address-randomization}}.

This document concerns itself with a variety of use cases in the form of specific protocols which are affected by RCM.
In each use case, the affects of different device policies is discussed.
In some cases the affects are not significant and no change is recommended.
In other cases, the affects are significant to end users experience, or to even damaging to device operation, and deployment of alternate protocols are recommended.

The recommendations for alternate protocols are critical and there is often a very difficult market situation as before the alternate protocol can be deployed both a client and server need to be present.
Neither party benefits until both parties move.
A particularly negative market situation can be when client and server implementers come to non-interoperable choices in what protocol they will implement.

# Terminology

{::boilerplate bcp14bcp}

{{?I-D.ietf-madinas-mac-address-randomization, Section 8}} defines the following terms:

* Per-Vendor OUI MAC address (PVOM)
* Per-Device Generated MAC address (PDGM)
* Per-Boot Generated MAC address (PBGM)
* Per-Network Generated MAC adress (PNGM)
* Per-Period Generated MAC address (PPGM)

# Protocol Specific Situations

## Parental Controls on dependant devices

TBD

## Paid Internet Services

TBD

# Privacy Considerations

YYY

# Security Considerations

ZZZ

# IANA Considerations

# Acknowledgements

Hello.

# Changelog


--- back

