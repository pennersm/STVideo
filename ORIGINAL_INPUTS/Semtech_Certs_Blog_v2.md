Utility providers operate tens or even hundreds of thousands of field
devices, including meters, reclosures, operational technology, IT
systems, surveillance equipment, and sensors at remote sites. Given the
wide operational geography, cellular technology such as private LTE and
5G is proving to be the ideal access network to consolidate
communications.

However, many existing devices do not have their own SIM card or
cellular interface. In these situations mission critical organizations
have often embraced Semtech Airlink Routers to achieve connectivity over
cellular networks. This approach solves the connectivity problem very
well, but it also introduces new architectural questions that directly
impact security: endpoint identity, device-level visibility, carrier
dependency, IP planning, and operational scale.

Some of the key challenges with cellular field connectivity - with or
without private APN - are the following:

**1. Lack of Visibility**

Often the network owner lacks visibility into the devices and the
traffic they send. If there are more than one device, this challenge is
especially difficult to solve since the wireless router often NATs all
the traffic.

**2. Limited or no Threat Prevention**

In order to adhere to Zero Trust best practices, we must continuously
monitor the traffic traversing the network, especially traffic from
critical assets. Often organizations use firewalls to help with the
security of traffic to and from these wireless routers, but lack
comprehensive defense against known and unknown malware, malicious DNS
queries or attacks, malicious URLs and other related threats.

**3. SIMs and carrier IPs are not enough as endpoint identity:**

A SIM, APN, or carrier-assigned IP connects the router, but it may
change or be spoofed and can therefore not be used as solid proof of
identity. Instead, an inseparable identity criteria tightly bound to the
box is needed.

**4. Carrier design can become carrier lock-in**

Utility IT departments need to coordinate address ranges, routing,
private APNs, NAT behavior, redundancy, and failover with each carrier.
Different carriers may not offer the same design, coverage,
availability, or private addressing models. And private APNs have a
cost.

Changing carriers or adding a second SIM shall not become a network
redesign but a simple, transparent transport change.

**5. Manual security does not scale**

In cases where VPNs are used, per-router VPN settings, certificates,
tunnel status, routes, renewals, revocation, and firewall policy cannot
be handled manually across thousands of field routers. Either operations
would slow down, or teams fall back to shared secrets, inconsistent
templates, or stale configuration.

**The Solution: A VPN Overlay – Make Cellular the Transport, Not the
Architecture**

The separation of concerns seems natural: Cellular providers supply
radio access and transport, the utility shall own the end to end
traffic. To achieve this, the architecture uses identity-bound secure
access: a certificate-based IPSec VPN approach that makes cellular the
transport layer, while the utility keeps control of identity,
addressing, segmentation, visibility, and security policy.

Semtech Airlink Cellular routers support the EST (Enrollment over Secure
Transport) protocol, enabling seamless interactions with Palo Alto
Networks PKI solutions and corresponding certificate enrollment at
scale.

<img src="media/media/image3.png"
style="width:6.5in;height:2.91667in" />

By abstracting field connectivity from the underlying cellular carrier,
the architecture delivers following benefit to utility
providers<span class="mark">:</span>

1.  **Complete Visibility**

As the architecture above shows, traffic is sent to a centralized NGFW
for IPSec tunnel termination and traffic inspection. Using App-ID, the
NGFW is able to ensure that only valid traffic is sent to and from the
connected devices. Any anomalous traffic can be alerted on to ensure
know spurious devices or traffic are on the network.

2.  **AI Enabled Threat Prevention**

Operational Technology (OT) traffic is secured through our Precision AI™
engine, a system that blends machine learning, deep learning, and
generative AI to deliver autonomous, real-time protection. Built
directly into their Next-Generation Firewalls (NGFW) this AI-driven
approach provides non-intrusive, passive discovery to analyzing behavior
rather than relying solely on static signatures. Precision AI enables
inline prevention of zero-day attacks and evasive command-and-control
(C2) threats targeting cyber-physical systems.

**3. Identity-Driven Router Authentication**

The IPSec endpoints are not trusted merely because traffic came from a
certain carrier IP address. A SIM could be moved and an IP address could
change or be spoofed. Fully automated Certificate enrollment based on
protocols like EST (Enrollment over Secure Transport) ties the router HW
to the identity of the box: The issued certificate is inseparably bound
to the router’s serial number, and the VPN uses that certificate to
identify the specific router — independent of SIM, carrier, or IP
address.

**4. Carrier independent IP planning**

The cellular connection can use whatever carrier IP, SIM, APN, or mobile
network is available. Inside the IPSec tunnel, the utility preserves its
own end-to-end addressing plan for the actual devices behind the router.
A router can use one carrier, change carrier, or use multiple SIMs for
redundancy, while application traffic and security policy between field
devices and the data center remain unchanged.

**Lower Opex, Better Control and Stronger Security by Automation**

This architecture pays back operationally. It reduces carrier
dependency, manual configuration, troubleshooting effort, and the risk
of inconsistent security design.

The main operational benefits are:

- **Granular Application control and threat prevention:** Every protocol
  can be dissected and individual message types be blocked or allowed
  only in one direction. Threats like message-floods, exploits or
  malicious traffic are detected at one central point.

- **Carrier changes become transport changes:** A new SIM, carrier, or
  mobile-side IP address does not require the utility to redesign its
  field addressing or security policy, private APNs are not a
  requirement for end-to-end IP-planning\>

- **Less manual configuration means fewer errors:** Routers enroll
  automatically, receive the right configuration, build the VPN
  presenting the correct identity without field teams manually handling
  secrets or tunnel parameters..

- **Certificate lifecycles are manageable:** Certs can be issued,
  renewed, revoked, and tracked through enrollment records, revocation
  lists and online status checks

- **Troubleshooting becomes easier:** Operations teams can distinguish
  between carrier transport issues, router issues, endpoint issues, and
  application/security policy issues.

A VPN from the Airlink cellular modem/router to the utility data center
is therefore not just encryption. It gives the utility a controlled
architecture where identity, visibility, segmentation, application
inspection, and operations are managed independently of the carrier
network while allowing the utility to focus on its core mission of
delivering safe, reliable, and efficient power while maintaining
complete ownership and security of its operational data.

For an example of a joint solution leveraging the technology above,
check out our [<u>Joint Solution
Brief</u>](https://technologypartners.paloaltonetworks.com/English/listing/semtech)
with Semtech Corporation and their Airlink routers.
