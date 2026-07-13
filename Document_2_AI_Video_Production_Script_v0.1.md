# Document 2 – AI Video Production Script

Status: Version 0.1 (Structure Freeze Draft)\
Target audience: Network / Security / OT Engineers\
Target duration: ~60 minutes\
Source of truth: Semtech Integration Guide

## Module 1 – Introduction (6 min)

- 1.1 Welcome
  who is Semtech, who is Palo Alto, what is a joint solution from both
mpe-qa: better proposals would be nce for a welcome  


- 1.2 Solution overview
  problems that utilities face and we address, see it e.g. in the blog "ORIGINAL_INPUTS/Semtech_Certs_Blog_v2.md"

- 1.3 Architecture
  keep it high level in terms of routing  
  focus on the connectivity aspect (end-to-end from wired client is fully visible, underlying transport due to tunneling is transparent )
  IPSec architecture brings security, visibility and connection of network endpoint with a real manageable identity aka certificate

- 1.4 Products used
strictly as per guide

- 1.5 Overall workflow
ITEMS: define EST secrets; define cert request format; stage template, boot airlink and fetch template; Airlink enrolls for cert and gets it with credentials
       AIrlink has IPSec config in template as well -> connect to NGFW
       NGFW has IKE GW and IPSec tunnel already provisioned (separate automation flow)
       Tunnel will come "up" once both sides identify each other


## Module 2 – Identity & Certificate Lifecycle (15 min)

- 2.1 Why certificates
scalability, reliability (private keys are not so easy to steal as passwords; scope of protection: Certificate/key is bound to identity and not a free key that can be used from anywhere)


- 2.2 Digital signatures
to start with: what is actually a certifictae = digital signature under identity content from a truest CA (explain all terms & pieces)

- 2.3 PKI
certificate lifecycle, expiry/re-enroll/revocation, automation of lifecycle actions

- 2.4 EST
as a protocol, RFC etc, basic functions, keep it simple. Dont go deeper than mentioning there are 2 different authentication mechanisms that need to be implemented and supported by the client

- 2.5 CyberArk overview
very quick product roadmap so viewers understand the current product sutuation. It is implict this will be temporary (due to Palo acquisition of cyberark) and we will later replace this piece with a NGTS info.

- 2.6 Verify CA Label


- 2.7 Generate API Key

- 2.8 EST CA Chain

- 2.9 TLS CA Chain

- 2.10 Airlink EST

- 2.11 Upload CA Certs

- 2.12 EST Credentials

- 2.13 CSR

- 2.14 Successful Enrollment

## Module 3 – Airlink IPSec (15 min)
- 3.1 Connecting to the Airlink
       incl role of ALMS

- 3.2 Networks
        network, interface and IP address objects in Airlink pre-define
- 3.3 Authentication IDs
        taken from cert
- 3.4 IPSec parameters

- 3.5 Crypto

- 3.6 Tunnel

- 3.7 Tunnel initiation

## Module 4 – NGFW Configuration (15 min)

- 4.1 Certificate overview

- 4.2 Certificate profile

- 4.3 Generate CSR

- 4.4 Issue certificate

- 4.5 Import certificate

- 4.6 Crypto profiles

- 4.7 IKE Gateway

- 4.8 Tunnel interface

- 4.9 IPSec tunnel

## Module 5 – Traffic Integration (5 min)

- 5.1 Logical routers

- 5.2 Routing

- 5.3 Security policy

- 5.4 Validation

## Module 6 – Troubleshooting (4 min)

- 6.1 EST

- 6.2 Certificates

- 6.3 IKE

- 6.4 IPSec

- 6.5 Routing

- 6.6 MTU/MSS

- 6.7 CLI
