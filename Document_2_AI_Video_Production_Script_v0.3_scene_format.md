# Document 2 – AI Video Production Script

Status: Version 0.3 (First Scene Format Proposal)  
Target audience: Network / Security / OT Engineers  
Target duration: ~60 minutes  
Source of truth: Semtech Integration Guide  
Narrative food: `ORIGINAL_INPUTS/Semtech_Certs_Blog_v2.md`

## Working Intent

This document is the structure-first production script for the video. It is not yet the final narration and it is not intended to replace the Integration Guide. The goal of this version is to make the content structure understandable enough for sales, engineering, and marketing review before investing time in exact wording, screen timing, callouts, and tool-specific production details.

The video should move from business and architecture context into concrete configuration. It should explain why the design exists, then show how certificates, EST enrollment, AirLink configuration, NGFW configuration, routing, policy, and troubleshooting fit together. The intended style is engineer-to-engineer: clear, technically credible, and practical, without turning the video into a generic marketing animation.

The source guide remains the technical source of truth. This script can reorder the material for better video flow, but it must not invent a different solution or change the integration logic.

---

## Scene Format

Each scene should eventually use the following structure. During structure freeze, not every field needs to be final, but the format should remain stable.

**Scene ID**  
Stable scene number. Do not renumber casually once structure is agreed.

**Status**  
Outline / Draft / Ready for Review / Ready for Recording / Final.

**Estimated Duration**  
Target runtime for this scene.

**Scene Purpose**  
What this scene must achieve in the viewer's mind.

**Narrative Intent**  
What the voiceover should communicate, without becoming final word-for-word narration too early.

**Visual Plan**  
What should appear on screen: animation, diagram, product GUI, screen recording, CLI, screenshot, or text overlay.

**On-Screen Actions**  
Concrete clicks, screen recordings, commands, or movements, if applicable.

**Callouts**  
Highlights, zooms, labels, arrows, warnings, or emphasis markers.

**Draft Narration**  
A first complete spoken version. This can later be refined for Descript, Wondershare, or another production tool.

**Production Notes**  
Anything that helps the editor or reviewer: pacing, dependencies, things to confirm, assets needed, or alternative takes.

**Exit / Transition**  
How the scene hands off to the next scene.

---

# Module 1 – Introduction (6 min)

## 1.1 Welcome

**Status**  
Draft format proposal.

**Estimated Duration**  
45–60 seconds.

**Scene Purpose**  
Open the video with a clear statement of what will be built and why the viewer should care. The viewer should immediately understand that this is not a generic product overview, but a practical engineering walkthrough of a joint Semtech AirLink and Palo Alto Networks integration.

**Narrative Intent**  
The scene should introduce Semtech as the connectivity side and Palo Alto Networks as the security side. It should set the expectation that the video will show how to create a certificate-authenticated IPSec overlay from a field router into a Palo Alto Networks NGFW, using CyberArk / ZT-PKI for the certificate lifecycle elements used in the current integration.

The tone should be direct and practical. Avoid long corporate messaging. The first minute should answer: what are we building, which systems are involved, and what result should the engineer expect by the end of the video?

**Visual Plan**  
Start with a clean title card using the solution name and the three main building blocks: Semtech AirLink, Palo Alto Networks NGFW, and CyberArk / ZT-PKI. Then transition into a very simple line diagram: field device → AirLink router → cellular / internet transport → Palo Alto Networks NGFW → service network.

**On-Screen Actions**  
No product GUI yet. Use a title card, then a simple animated architecture sketch. Keep movement minimal: components fade in from left to right, ending with a highlighted IPSec tunnel between AirLink and NGFW.

**Callouts**  
- “Semtech AirLink: field connectivity”
- “Palo Alto Networks NGFW: security enforcement”
- “CyberArk / ZT-PKI: certificate lifecycle”
- “Certificate-authenticated IPSec tunnel”

**Draft Narration**  
Welcome. In this video, we will walk through a joint Semtech and Palo Alto Networks solution for securing field connectivity.

The goal is to connect devices behind a Semtech AirLink router to services behind a Palo Alto Networks Next-Generation Firewall using a certificate-authenticated IPSec tunnel. The cellular or WAN connection provides transport, but the actual trust model is based on device identity, certificates, and firewall policy.

We will use the current CyberArk / ZT-PKI workflow to prepare the certificate enrollment pieces, configure the AirLink router, configure the Palo Alto Networks firewall, and then validate that the tunnel and traffic flow are working end to end.

**Production Notes**  
This scene should look polished but not overproduced. Use it to establish credibility and direction. Do not yet explain EST, PKI theory, routing, or detailed product configuration. Those come later.

If this video is shown to sales or marketing first, this scene should be understandable without deep firewall knowledge. If shown to engineers, it should still feel technically precise and not like a brochure.

**Exit / Transition**  
Next we will look at the problem this architecture solves for utilities and other distributed industrial environments.

---

## 1.2 Solution Overview

This scene explains the problem space: utility and industrial providers have large numbers of remote sites and field devices, but many of those devices do not have their own cellular identity or native security stack. AirLink routers solve the connectivity problem, but the security architecture still needs visibility, reliable endpoint identity, scalable onboarding, and consistent policy enforcement.

The solution uses cellular as transport, not as the security architecture itself. The actual trust model is built around certificate-based router identity, IPSec tunnel establishment, centralized firewall inspection, and policy control independent of carrier IPs, SIMs, APNs, or private addressing models.

## 1.3 Architecture

This scene presents the high-level architecture without going deep into routing yet. A wired or local field device connects behind the AirLink router, the AirLink establishes an IPSec tunnel over whichever cellular or WAN transport is available, and the Palo Alto Networks NGFW terminates the tunnel and inspects the decapsulated traffic.

The main architectural message is separation of concerns. Cellular provides reachability; certificates provide identity; IPSec provides encrypted transport; and the NGFW provides visibility, segmentation, logging, and threat prevention for the actual application traffic.

## 1.4 Products Used

This scene lists the products and systems involved, strictly aligned with the Integration Guide. The viewer should understand that three administrative domains are involved: the CyberArk / ZT-PKI environment for certificate issuance and EST parameters, the Semtech AirLink router for field-side connectivity and EST enrollment, and the Palo Alto Networks NGFW for IPSec termination and security enforcement.

The scene should also clarify what is intentionally out of scope. Basic internet access, initial AirLink activation, base NGFW networking, and customer-specific routing policies are assumed to exist or be prepared separately.

## 1.5 Overall Workflow

This scene gives the viewer the process map before the detailed configuration begins. The workflow starts with certificate and EST preparation, then moves to AirLink enrollment and IPSec configuration, then to the firewall-side IKE/IPSec configuration, routing, security policy, validation, and troubleshooting.

This scene should make the dependency chain obvious: define EST secrets, define the certificate request format, prepare the AirLink, let the AirLink enroll for a certificate, configure IPSec identities and selectors, provision the NGFW objects, and finally bring the tunnel up once both sides can authenticate each other.

---

# Module 2 – Identity & Certificate Lifecycle (15 min)

## 2.1 Why Certificates

This scene explains why the solution uses certificates instead of shared passwords or pre-shared keys. Certificates scale better because each router receives its own identity, and the private key can remain bound to the device rather than being copied around as a shared secret.

The key message is that the firewall should not trust a router only because traffic came from a certain carrier IP address or APN. The router must prove its own identity during IKE authentication, and that identity should survive carrier changes, SIM changes, and dynamic addressing.

## 2.2 Digital Signatures

This scene explains the minimum certificate theory needed for the rest of the video. A private key signs or proves possession, a public key can be shared, and a certificate is a signed statement from a trusted CA that binds identity information to that public key.

The scene should avoid becoming a PKI lecture. It only needs to prepare the viewer for the practical fields used later: subject, subject alternative name, certificate authority, certificate chain, private key, and certificate signing request.

## 2.3 PKI

This scene introduces the PKI as the system that issues, tracks, renews, and potentially revokes certificates. It should explain that certificate lifecycle is not only about the first certificate, but also about expiry, renewal, policy, trust chains, and operational control.

For this solution, PKI matters because the AirLink routers need automated enrollment at scale while the NGFW currently uses a manual CSR signing flow. The viewer should understand why both methods still rely on the same trust concept: a certificate issued under the correct CA policy.

## 2.4 EST

This scene explains EST, Enrollment over Secure Transport, as the protocol used by the AirLink router to request and renew certificates. The focus should be practical: EST gives the router a repeatable way to contact the certificate service, authenticate the request, submit certificate request data, and obtain a signed certificate.

The scene should mention that initial enrollment and re-enrollment may use different authentication mechanisms. The first enrollment can use API credentials, while later renewal can use certificate-based authentication once the device already owns a valid certificate.

## 2.5 CyberArk / ZT-PKI Overview

This scene gives a short orientation to the current CyberArk / ZT-PKI role in the workflow. ZT-PKI provides the CA policy, the policy label used by EST, the API credentials used for enrollment, and the CA chain needed by both sides to validate issued certificates.

This should be framed as the current implementation state, not a permanent product roadmap statement. The scene can mention that this part may evolve due to the Palo Alto Networks / CyberArk integration, but the underlying concepts remain the same: policy, credentials, CA chain, certificate issuance, and lifecycle management.

## 2.6 Verify CA Label

This scene shows where the CA Label or policy identifier is found in the ZT-PKI GUI. The label is important because it tells the EST endpoint which CA policy should handle the router certificate request.

The viewer should understand that this is not a random string to invent during setup. It comes from the assigned CA policy and must match the customer or project environment used for the integration.

## 2.7 Generate API Key

This scene shows how to generate the API key and key ID used for AirLink EST enrollment. These credentials are used by the AirLink during initial certificate enrollment, so they must be copied immediately and stored carefully during the configuration process.

The production script should emphasize the operational detail: the key is shown only once. The video should visually highlight the API Key ID and API Key fields, then transition to using those values later in the AirLink EST credentials section.

## 2.8 EST CA Chain

This scene shows how to download the CA chain that belongs to the issuing CA. The AirLink and NGFW both need the correct CA chain so they can validate certificates issued by the ZT-PKI environment.

The practical message is that the CA chain used for validating issued device certificates is different from the public TLS chain used to validate the HTTPS connection to the EST service. This distinction should be made clearly because confusing those two chains is a common setup problem.

## 2.9 TLS CA Chain

This scene explains and shows the download of the TLS CA certificates needed by the AirLink to trust the EST server endpoint itself. Unlike a browser or standard operating system, the AirLink may not already have the required public trust store for the EST service.

The viewer should understand the difference between trusting the transport and trusting the issued certificate identity. The TLS CA chain protects the HTTPS/EST connection to the service, while the EST CA chain validates the certificates issued for the AirLink and NGFW identities.

## 2.10 AirLink EST Preparation

This scene transitions from the PKI side into the AirLink configuration. At this point the viewer has the required values: EST service URL, CA label, API key information, EST CA chain, and TLS CA chain.

The purpose is to prepare the router so it can request its own identity certificate. The scene should make clear that this certificate will later be used directly in the IPSec tunnel authentication configuration.

## 2.11 Upload CA Certs

This scene shows the AirLink certificate area and uploads the required CA chains. The TLS CA chain allows the router to trust the EST service connection, while the EST CA chain allows it to validate certificates issued by the project CA.

The video should visually distinguish the two uploads and name them clearly. A short warning should be included that the certificate status must show as valid before continuing.

## 2.12 EST Credentials

This scene configures the EST credential object in the AirLink using the API Key ID and API Key generated earlier. The router stores these credentials and refers to them when making the initial certificate enrollment request.

The scene should include one important operational note: after saving, credentials are not shown again in clear text. If the configuration later becomes a template, the credential object name should not include router-specific information unless that is intentionally part of the customer design.

## 2.13 CSR

This scene defines the certificate request generated by the AirLink. The important identity value is the subject alternative name, which must carry the router serial number in the expected DNS format because it becomes part of the IPSec identity matching later.

The video should connect the CSR fields to the future IPSec configuration. The viewer should understand that the certificate is not just a generic file; it contains identity content that the NGFW and AirLink will use to recognize each other.

## 2.14 Successful Enrollment

This scene shows the result of successful EST enrollment on the AirLink. The certificate status should become valid, and the certificate details should show populated validity and subject information.

The checkpoint at the end of Module 2 is simple: the AirLink now owns a valid certificate identity. From this point on, the video can stop explaining certificate theory and start using that identity for IPSec authentication.

---

# Module 3 – AirLink IPSec (15 min)

## 3.1 Connecting to the AirLink

This scene shows the available ways to access the AirLink configuration interface, including local access and ALMS. The viewer should understand that ALMS can render the router configuration remotely once the router is registered and online.

The purpose is not to teach full AirLink onboarding. It only establishes where the upcoming IPSec and certificate settings are configured and how engineers can reach the same screens in their environment.

## 3.2 Networks

This scene defines the local and remote networks used by the IPSec tunnel. On the AirLink side, the local network is the field-side segment behind the router; the remote network is the datacenter or service network reachable behind the NGFW.

The video should explain why each AirLink local subnet must be unique unless the NGFW design explicitly handles overlapping ranges through separate routing contexts. This is the point where the IPSec selectors begin to connect with the later NGFW tunnel and routing configuration.

## 3.3 Authentication IDs

This scene explains the local and remote authentication IDs used by IPSec. The AirLink local ID should match the router certificate identity, typically the SAN DNS value containing the AirLink serial number; the remote ID should match the NGFW certificate identity.

The important message is exact matching. These values do not need to be resolvable DNS names, but they must match the certificate contents and the peer configuration exactly, including spelling and case.

## 3.4 IPSec Parameters

This scene walks through the main AirLink IPSec tunnel settings: client mode, LAN mode, peer address or FQDN, local and remote subnets, certificate authentication, and selected WAN interface. The aim is to show which fields are structural and which fields are customer-specific.

The video should avoid reading a long table field by field. Instead, it should group the parameters into identity, peer reachability, traffic selectors, tunnel mode, and operational behavior.

## 3.5 Crypto

This scene explains the AirLink IKE and ESP crypto settings and why they must match the firewall-side profiles. The viewer should understand that mismatched proposals or timers can cause tunnels to fail immediately or drop later during rekey.

The key operational detail is that some AirLink defaults differ from PAN-OS defaults. The solution therefore defines matching profiles on the NGFW side rather than expecting every router to be configured differently.

## 3.6 Tunnel

This scene creates or reviews the AirLink IPSec tunnel object using the certificate and network settings prepared earlier. The video should show the final tunnel definition as a single coherent object that combines identity, peer, subnets, and crypto.

The scene should close by saving the configuration and making it clear that the AirLink is the initiating side. The NGFW will be configured as the passive responder side in the next module.

## 3.7 Tunnel Initiation

This scene shows what happens after the AirLink tunnel is enabled. The router should begin attempting IKE negotiation toward the configured peer, even if the NGFW is not yet fully configured.

The checkpoint is not a green tunnel yet. At this stage, expected evidence is that IKE attempts are leaving the AirLink and reaching the NGFW public interface, which becomes the bridge into the firewall configuration module.

---

# Module 4 – NGFW Configuration (15 min)

## 4.1 Certificate Overview

This scene explains the NGFW certificate requirement. The firewall also needs an identity certificate so the AirLink can authenticate the peer during IKE negotiation.

Unlike the AirLink, the NGFW flow in this guide is manual: generate a CSR on the firewall, sign it in ZT-PKI, and import the resulting certificate back into the firewall. The key message is that the private key stays on the firewall during this process.

## 4.2 Certificate Profile

This scene creates the NGFW certificate profile used to validate AirLink certificates. The certificate profile references the CA chain downloaded from ZT-PKI and tells PAN-OS which issuing CA should be trusted for peer authentication.

The scene should keep production guidance simple. For the validated integration, the profile is configured for broad compatibility; customer-specific restrictions such as CRL or additional policy checks can be discussed as production hardening topics later.

## 4.3 Generate CSR

This scene generates the NGFW certificate signing request in PAN-OS. The request defines the firewall identity, including the subject and subject alternative name that the AirLink will later use as the remote authentication ID.

The viewer should understand that exporting the CSR does not export the private key. The private key remains on the NGFW, while only the public request is sent to the CA for signing.

## 4.4 Issue Certificate

This scene returns to ZT-PKI to manually issue the NGFW certificate using the CSR. The CSR is pasted or uploaded into the request workflow, parsed, and signed under the correct organization and CA policy.

This is the only deliberate interface jump inside the NGFW certificate story. It should be shown as part of one continuous lifecycle: create request on NGFW, sign request in ZT-PKI, download signed certificate, and return to NGFW.

## 4.5 Import Certificate

This scene imports the signed NGFW certificate back into PAN-OS using the same certificate name as the pending CSR. If the import is successful, the pending request becomes a usable certificate and appears correctly chained to the CA certificates.

The video should make this a hard checkpoint. If the firewall does not recognize the certificate and chain correctly, IPSec authentication will not work and the viewer should not continue to IKE configuration yet.

## 4.6 Crypto Profiles

This scene creates or verifies the IKE and IPSec crypto profiles on the NGFW. The profile values must match the AirLink configuration, including encryption, integrity, Diffie-Hellman group, PFS, and timers.

The script should call out the naming convention if automation expects a specific profile name. It should also explain why rekey timing matters in passive-mode deployments, where the firewall should not expire keys before the AirLink initiates renewal.

## 4.7 IKE Gateway

This scene configures the IKE Gateway, which is the central NGFW object for authenticating the AirLink and accepting the IKE negotiation. The gateway uses dynamic peer addressing, passive mode, the NGFW local certificate, and the certificate profile used to validate the AirLink certificate.

The viewer should understand that one IKE Gateway is typically created per AirLink router in this basic design. Naming should map clearly to the AirLink identity, usually the serial number, because automation and operations depend on predictable object relationships.

## 4.8 Tunnel Interface

This scene creates the PAN-OS tunnel interface that terminates the decapsulated IPSec traffic. The interface is assigned to the correct logical router and security zone so traffic can be routed and controlled after decryption.

The scene should briefly explain why the tunnel interface is not just a cosmetic object. It is the L3 handoff point for routed traffic, zone assignment, MTU/MSS tuning, and future operational controls such as DPD or dynamic routing if used.

## 4.9 IPSec Tunnel

This scene creates the IPSec tunnel object and maps together the IKE Gateway, IPSec crypto profile, tunnel interface, and proxy selectors. The local selectors represent datacenter or service networks; the remote selectors represent the AirLink-side local network.

The checkpoint at the end of Module 4 is that the tunnel should be able to establish once committed and once the AirLink continues initiating. If IKE succeeds but IPSec remains down, likely causes include selector mismatch, certificate mismatch, or crypto mismatch.

---

# Module 5 – Traffic Integration (5 min)

## 5.1 Logical Routers

This scene explains the logical router design at a high level. The underlay network handles transport and incoming IKE/IPSec traffic, while the service-side logical router handles decapsulated application traffic from the tunnel.

The purpose is segmentation and operational clarity. Keeping transport and service traffic separate makes it easier to support different carriers, overlapping transport designs, and clean policy boundaries.

## 5.2 Routing

This scene adds the routes needed to send traffic between the service network and the AirLink local network through the correct tunnel interface. The NGFW needs a route toward the AirLink subnet via the tunnel, while the AirLink LAN mode typically installs the corresponding route toward the service network.

The viewer should understand that a green tunnel alone does not guarantee useful traffic flow. Routing must connect the decapsulated tunnel interface to the service network in both directions.

## 5.3 Security Policy

This scene defines the security policies that allow and inspect traffic between AirLink-connected devices and datacenter services. The policy should distinguish underlay IKE/IPSec traffic from decapsulated application traffic inside the tunnel.

The video should connect this back to the value proposition: once traffic is visible to the NGFW, App-ID, logging, threat prevention, segmentation, and identity-informed policy can be applied. The policy examples should remain simple and aligned with the validated integration.

## 5.4 Validation

This scene validates the end-to-end result. The viewer should see the tunnel status, IKE/IPSec SA state, and a simple traffic test between a device behind the AirLink and a service behind the NGFW.

The success criteria should be explicit: certificates are valid, IKE is established, IPSec child SA is mature, routes point through the tunnel, security policy allows the traffic, and logs show the expected application traffic.

---

# Module 6 – Troubleshooting (4 min)

## 6.1 EST

This scene covers the most common EST enrollment failure categories. These include wrong CA label, wrong API credentials, wrong EST URL, missing TLS CA trust, missing EST CA chain, or CSR values rejected by policy.

The goal is not to troubleshoot every possible certificate platform issue. The video should give engineers a fast mental checklist for determining whether the failure is transport trust, authentication, policy, or certificate request content.

## 6.2 Certificates

This scene focuses on certificate identity and chain problems. Common failures include wrong SAN value, mismatched local or remote authentication ID, missing CA chain, certificate imported under the wrong name, or the NGFW not associating the signed certificate with the pending CSR.

The viewer should understand that certificate problems often appear later as IKE authentication problems. Therefore, certificate validation should happen before debugging crypto or routing.

## 6.3 IKE

This scene covers IKE-level troubleshooting on PAN-OS. Engineers should check whether IKE packets arrive, whether an IKE SA exists, and whether logs show authentication, proposal, or identity errors.

The video should show the essential CLI checks and remind viewers that in passive mode the NGFW responds to AirLink initiation rather than actively dialing a dynamic peer. If no IKE traffic arrives, the issue is likely reachability, NAT, public IP, peer address, or upstream filtering.

## 6.4 IPSec

This scene covers cases where IKE succeeds but the IPSec tunnel or child SA does not mature. Likely causes include proxy selector mismatch, crypto mismatch, missing routes, AirLink firewall behavior, or unavailable local/remote networks.

The key diagnostic message is that a successful IKE negotiation only proves peer authentication and phase-one agreement. It does not prove that the traffic selectors, tunnel interface, routing, and policy are correct.

## 6.5 Routing

This scene covers routing problems after the tunnel is up. Engineers should verify the route toward the AirLink local network via the tunnel interface, the return path from the AirLink toward the service network, and the logical router assignments.

The video should emphasize that routing and security policy are separate checks. A tunnel can be up, routes can be correct, and traffic can still be blocked by policy—or the policy can be correct while routing sends packets elsewhere.

## 6.6 MTU/MSS

This scene explains MTU and MSS issues in cellular and tunneled environments. Multiple layers of encapsulation can reduce the effective path MTU and cause larger packets to fail, especially when fragmentation is blocked.

The script should show the basic test method with ping payload sizes and the simple calculation from successful payload size to MTU and MSS. The fix should point to tunnel interface MTU/MSS settings rather than changing physical interface MTU unnecessarily.

## 6.7 CLI

This final troubleshooting scene collects the practical PAN-OS commands used to inspect IKE and IPSec state, follow logs, clear stale SAs, and force renegotiation where applicable. It should feel like a quick field checklist rather than a full CLI training.

The video should close with the message that engineers should troubleshoot in order: certificate validity, IKE reachability, IKE authentication, IPSec selectors, routing, security policy, and MTU/MSS. That order prevents wasting time on routing when the real issue is identity, or debugging certificates after traffic is already flowing.
