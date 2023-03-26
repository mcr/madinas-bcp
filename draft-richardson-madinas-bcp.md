---
title: Best Current Practices for consistent network identity in a privacy preserving way
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
  CAPTIVE: RFC8952

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

The recommendations for alternate protocols are critical and there is often a very difficult market situation: before the alternate protocol can be deployed both a client and server need to be present.
Neither party benefits until both parties have deployed.
A particularly negative market situation can develop when client and server implementers come to non-interoperable choices in what protocol they will implement.

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

A common concern among parents of children is that the children do not access the Internet at inappropriate times.
For instance, network access may be restricted from 30 minutes before bedtime until 6am in the morning.

(There are also concerns that the devices used by the children should go through specific filtering, but that is a subset of the time-of-day access.  The time-of-day access is a binary on/off function, while the filtering is some continuous function with varying access between zero and one)

In order to restrict access to the child's device, the child's device needs to be identified.
In order to not restrict access to other devices, those devices also need to be identified.
Any device on the network which is not identifiable as being in either of these two categories has an ambiguous policy.

A child's device which uses a PVOM, PDGM or PNGM address will be seen to have a consistent layer-2 address by the network infrastructure.
The device can therefore be recognized and Internet access can be restricted at appropriate times.

The use of a Per-Boot (PBGM) or a Per-Period (PPGM) address policy will result in the child's device changing it's layer-two address periodically, and this requires that the network infrastructure have it's policy updated.

A child (particulary a teenager) may be motivated to overcome these restrictions.
They may be able to control their device, either through intentional "jail-breaking", or perhaps even due to some available malware that has the same effect.
Any protocol that allows the child to pick a new identity (for instance, impersonating a parent device) would allow the child to overcome the limitation.

On a network where all devices except the child's device have no limitation is easiest: all the child needs to is to pick a new randomly chosen layer-two address.
A network with a constant Pre-Shared Key (WPA-PSK) allows for any device knowing that PSK to join the network with essentially any layer-two address.

It is therefore necessary for all devices which are present in this child-restricted network to identify themselves in order for the network infrastructure to know that the relevant device is not a child's device.

This identification must be specific to each device, must not be forgeable, and must contain a credential that the network infrastructure can identify.

### Home Networks need to use WPA-Enterprise

An LDevID deployed to all devices meets all of the criteria.

* observation of the public certificate does not convey any special permissions
* the private key of the LDevID an be stored in a secure element, fTPM or other trusted executation environment
* it scales easily to many devices
* it allows for a specific device to be identified for special processing, or to be ejected from the network
* it does not require any external arrangement with external services, if the CA's key is managed by the home router itself.

There are some privacy concerns with EAP-TLS used in WPA-Enterprise.
Specifically, the client-certificate is visible in EAP-TLS 1.2 handshakes, and this could be used by an observer to coordinate which connection belongs to which personal device.

The most difficult part of this change is that it requires that home routers:

1. maintain a PKI with which to sign new certificates
2. have a mechanism to easily onboard new devices, along with a mechanism to deal with IoT devices which might be in the home.
3. have a way for the first user of the router to become the administrator
4. provide a way to backup the entire mechanism to guard against home router failure, flash replacement (such as when ISPs change), or other incompatible upgrades.

## Paid/Captive Internet Services

A common case for hotels, airports and coffee shops is that they have an unencrypted network id.
Guests connect to this network, but the network contains a captive portal {{CAPTIVE}} which "hijacks" all connections, and then demands a credential.
Often these credentials are somewhat trivial: a room number with a matching guest last name.
Some hotels demand far more complex logins, including use of loyalty system logins to enable access.

For the coffee shop and airport situations, it is uncommon for devices to spend a significant amount of time at that location.
The use of an unencrypted network makes it trivial for an attacker to do ARP or ND spoofing of the default router
They can then capture logins to the captive portal (having put up their own look-alike).

It is often also trivial in these networks to allow multicast traffic, and identifiable information can be found by using mDNS queries, or other port-scanning methods.
The access point can not defend against such attacks, since the official access point has been spoofed.


## Well known PSK Internet access

In some coffee shops, the network is encrypted, but there is a WPA-PSK which is written on the chalkboard.
They seldom change, allowing patrons who have previously sipped coffee in that location to easily return and instantly be connected again.

For the coffee shop, it is uncommon for devices to spend a significant amount of time at that location.
It is unlikely that a typical 12-hour Per-Period (PPGM) policy will run into this problem in a coffee shop.

But, the PSK methods are rather weak, as they PSK is well known, so not only can any attacker setup their own access point (grabbing all the traffic, and any PII they want), but


# Privacy Considerations

YYY

# Security Considerations

ZZZ

# IANA Considerations

# Acknowledgements

Hello.

# Changelog


--- back

