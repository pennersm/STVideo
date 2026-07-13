# Document 2 – AI Video Production Script

Status: Version 0.4 (Module 1 Scene Drafts)  
Target audience: Network / Security / OT Engineers  
Target duration: ~60 minutes  
Source of truth: Semtech Integration Guide  
Narrative food: `ORIGINAL_INPUTS/Semtech_Certs_Blog_v2.md`

## Working Intent

This document is the structure-first production script for the video. It is not yet the final narration and it is not intended to replace the Integration Guide. The goal of this version is to make the content structure understandable enough for sales, engineering, and marketing review before investing time in exact wording, screen timing, callouts, and tool-specific production details.

The video should move from business and architecture context into concrete configuration. It should explain why the design exists, then show how certificates, EST enrollment, AirLink configuration, NGFW configuration, routing, policy, and troubleshooting fit together. The intended style is engineer-to-engineer: clear, technically credible, and practical, without turning the video into a generic marketing animation.

The source guide remains the technical source of truth. This script can reorder the material for better video flow, but it must not invent a different solution or change the integration logic.

---

# Module 1 – Introduction (6 min)

## 1.1 Welcome

**Status**  
Draft.

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

**Status**  
Draft.

**Estimated Duration**  
75–90 seconds.

**Scene Purpose**  
Explain the problem that makes this integration relevant. The viewer should understand why field connectivity alone is not enough and why utility or industrial environments need scalable identity, visibility, and policy enforcement for remote devices.

**Narrative Intent**  
The scene should describe a distributed utility or industrial environment with many remote assets, such as meters, sensors, reclosers, surveillance equipment, OT devices, and IT systems. Many of these devices do not have their own SIM, cellular interface, security stack, or manageable identity, so they depend on an AirLink router for connectivity.

The key message is that the cellular network solves reachability, but not the full security problem. Carrier IPs, APNs, NAT behavior, and SIMs are useful transport mechanisms, but they are not enough to provide end-to-end visibility, reliable router identity, threat prevention, or scalable operations.

**Visual Plan**  
Use a distributed field-site animation. Show several remote field devices behind AirLink routers, then show them connecting over cellular or WAN transport into a central security point. Introduce visual problem labels: “limited device visibility,” “carrier-dependent addressing,” “manual VPN scale,” and “identity tied to router certificate.”

**On-Screen Actions**  
No GUI actions. Use a simple animated problem-to-solution sequence: first show many remote sites, then show transport complexity, then overlay a certificate-authenticated IPSec tunnel toward the NGFW.

**Callouts**  
- “Connectivity is not the same as security”
- “SIM / APN / IP address ≠ strong endpoint identity”
- “Certificate identity survives carrier changes”
- “Centralized visibility and policy”

**Draft Narration**  
Utility and industrial providers often operate large numbers of remote field sites. Those sites may contain meters, sensors, operational technology, surveillance equipment, or other systems that need reliable connectivity back to a service network or datacenter.

Semtech AirLink routers solve the field connectivity problem very well. They provide cellular or WAN access for devices that may not have their own cellular interface or SIM. But once that connectivity exists, the security architecture still needs to answer several questions: which router is this, what devices are behind it, what traffic is moving, and which policy should be applied?

In this solution, cellular remains the transport layer. The security model is built above it, using certificate-based AirLink identity, IPSec tunnel establishment, centralized firewall inspection, and policy control independent of carrier IP addressing or APN design.

**Production Notes**  
This scene can borrow heavily from the Semtech certificates blog narrative. Keep the customer problem concrete and credible. Do not overstate that SIMs are useless; instead, position SIMs and APNs as transport and subscription mechanisms, not complete security identity.

**Exit / Transition**  
Now that the problem is clear, we can look at the architecture that separates transport from security and identity.

---

## 1.3 Architecture

**Status**  
Draft.

**Estimated Duration**  
75–90 seconds.

**Scene Purpose**  
Show the overall architecture at a level that engineers can understand before seeing configuration screens. The viewer should understand the end-to-end path from a field device through the AirLink, through the IPSec tunnel, into the NGFW, and onward to services.

**Narrative Intent**  
The scene should emphasize separation of concerns. Cellular or WAN transport provides reachability; certificates provide identity; IPSec provides encrypted overlay transport; and the Palo Alto Networks NGFW provides tunnel termination, segmentation, visibility, logging, and threat prevention for the decapsulated application traffic.

This scene should stay high level and avoid deep routing detail. The important idea is that the firewall sees and controls the actual traffic between field devices and service networks, while the underlying carrier network becomes transparent transport.

**Visual Plan**  
Use a clean architecture diagram with three zones: field site, transport network, and customer service network. Show a device behind the AirLink, an IPSec tunnel across the transport network, the NGFW as termination and inspection point, and services behind the firewall.

Use a second overlay to show identity: AirLink certificate identity on one side, NGFW certificate identity on the other, and mutual authentication during IKE.

**On-Screen Actions**  
No GUI actions. Animate in layers:
1. physical / transport connectivity,
2. certificate identities,
3. IPSec overlay,
4. inspected application traffic through the NGFW.

**Callouts**  
- “Transport: cellular / WAN”
- “Identity: certificates”
- “Overlay: IPSec”
- “Inspection: NGFW policy and logs”
- “Application traffic visible after decapsulation”

**Draft Narration**  
At a high level, the architecture separates connectivity from security.

A local device connects behind the Semtech AirLink router at the field site. The AirLink uses whatever cellular or WAN transport is available to reach the Palo Alto Networks firewall. Across that transport, the AirLink establishes an IPSec tunnel to the NGFW.

The tunnel is authenticated with certificates. The AirLink proves its identity using its router certificate, and the firewall presents its own certificate identity back to the AirLink. Once the tunnel is established, the NGFW terminates IPSec, decapsulates the traffic, and applies routing, zones, security policy, visibility, and threat prevention to the actual application traffic.

**Production Notes**  
This is likely one of the most important scenes for sales review. The diagram must be simple enough to understand quickly, but technically accurate enough for engineers. Avoid detailed logical router design here; that belongs later in Module 5.

**Exit / Transition**  
With the architecture in mind, the next step is to identify the products and systems that participate in the workflow.

---

## 1.4 Products Used

**Status**  
Draft.

**Estimated Duration**  
60–75 seconds.

**Scene Purpose**  
List the products and administrative systems used in the integration. The viewer should know which platform is responsible for which part of the workflow before the detailed scenes begin.

**Narrative Intent**  
The scene should align strictly with the Integration Guide and avoid adding products that are not part of the validated workflow. The three central systems are CyberArk / ZT-PKI for certificate policy, API credentials, CA chains, and manual certificate issuance; Semtech AirLink for field connectivity, EST enrollment, and IPSec client configuration; and Palo Alto Networks NGFW for certificate validation, IKE/IPSec termination, routing, and security policy.

The scene should also define assumptions. Basic NGFW network reachability, AirLink internet access, ALMS registration where used, and customer-specific routing design are assumed rather than taught from scratch.

**Visual Plan**  
Use a three-column product responsibility table. Each column should contain the product name, a simple icon, and the key responsibilities. Keep it visual and concise rather than a dense bullet list.

**On-Screen Actions**  
No live GUI yet. Show each product responsibility column appearing one by one. End with a small “Prerequisites” area that lists access to ZT-PKI, AirLink GUI or ALMS, PAN-OS GUI, and planning data such as local and remote networks.

**Callouts**  
- “ZT-PKI: certificate policy and enrollment data”
- “AirLink: EST client and IPSec initiator”
- “NGFW: IPSec responder and security enforcement”
- “Planning data required before configuration”

**Draft Narration**  
Three main systems participate in this integration.

The first is CyberArk / ZT-PKI, which provides the certificate policy, the CA label used by EST, the API credentials for initial enrollment, the CA chains, and the manual certificate issuance flow used for the firewall certificate.

The second is the Semtech AirLink router. It provides field connectivity, performs EST enrollment for its own certificate, and initiates the IPSec tunnel toward the firewall.

The third is the Palo Alto Networks Next-Generation Firewall. It validates the AirLink certificate, presents its own certificate identity, terminates the IPSec tunnel, routes the decapsulated traffic, and applies security policy.

Before starting, you need access to these systems and the planning data for the field-side networks, service-side networks, and certificate identities.

**Production Notes**  
This scene should be easy to replace later if product naming changes after Palo Alto / CyberArk integration evolves. Keep the wording “current workflow” around CyberArk / ZT-PKI to avoid locking the video too tightly to temporary branding.

**Exit / Transition**  
Now we can walk through the overall workflow from certificate preparation to tunnel validation.

---

## 1.5 Overall Workflow

**Status**  
Draft.

**Estimated Duration**  
90–120 seconds.

**Scene Purpose**  
Give the viewer a complete process map before the detailed implementation starts. This scene should prevent the rest of the video from feeling like random product hopping between ZT-PKI, AirLink, and NGFW.

**Narrative Intent**  
The scene should explain the dependency order. First, prepare the certificate and EST information in ZT-PKI. Then configure the AirLink so it can trust the EST service, authenticate with EST credentials, generate its CSR, and obtain its certificate. After that, configure AirLink IPSec using the certificate identity and the required local and remote networks.

Then the firewall side is prepared: certificate profile, NGFW certificate, crypto profiles, IKE Gateway, tunnel interface, IPSec tunnel, routing, and security policy. The final step is validation and troubleshooting in the correct order.

**Visual Plan**  
Use a horizontal workflow timeline or swimlane diagram with three lanes: ZT-PKI, AirLink, and NGFW. Show the scenes grouped by dependency instead of by original document order. Use a marker for “AirLink has certificate,” another marker for “AirLink initiates IKE,” and another marker for “Tunnel established.”

**On-Screen Actions**  
No GUI actions. Animate the workflow from left to right:
1. ZT-PKI parameters and CA material,
2. AirLink EST enrollment,
3. AirLink IPSec initiation,
4. NGFW certificate and IKE/IPSec configuration,
5. routing and policy,
6. validation.

**Callouts**  
- “Step 1: Prepare PKI and EST material”
- “Step 2: Enroll AirLink certificate”
- “Step 3: Configure AirLink IPSec”
- “Step 4: Configure NGFW responder”
- “Step 5: Route, secure, validate”

**Draft Narration**  
The full workflow has several steps, but the dependency chain is straightforward.

We begin in the certificate platform. There we identify the CA policy, collect the CA label, generate the API key used for initial enrollment, and download the certificate chains needed for trust.

Next, we move to the AirLink. The router is configured to trust the EST service, use the enrollment credentials, generate a certificate request, and obtain its own certificate. That certificate becomes the AirLink identity used later for IPSec.

After the AirLink has a certificate, we configure its IPSec tunnel settings: local and remote networks, authentication IDs, peer address, and crypto parameters. The AirLink then starts initiating IKE toward the firewall.

On the NGFW, we prepare the firewall certificate, certificate profile, crypto profiles, IKE Gateway, tunnel interface, and IPSec tunnel. Finally, we add routing and security policy, validate the tunnel and traffic flow, and use a structured troubleshooting process if anything fails.

**Production Notes**  
This scene is a candidate for being reused as a chapter menu in the production tool. If the production tool supports chapter markers, use this workflow to create them. Keep the visual simple and avoid showing the full 21-step guide table.

**Exit / Transition**  
We will start with the identity and certificate lifecycle, because the IPSec tunnel depends on both peers being able to prove who they are.

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
