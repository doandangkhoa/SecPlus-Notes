## 1. The Problem with Traditional Networks
Traditional network security often relies on a "castle-and-moat" approach:
*   **Perimeter Focus:** Heavy security at the firewall.
*   **Internal Vulnerability:** Once inside the firewall, the network is **relatively open**.
*   **Lack of Controls:** Users and systems can move from device to device without checks.
*   **The Risk:** This allows **unauthorized individuals** and **malicious software** to move freely, potentially accessing sensitive resources.

---

## 2. What is Zero Trust?
**Zero Trust** is a security model based on the principle: **"Never trust, always verify."**
*   **Core Philosophy:** Nothing is trusted by default, regardless of location (inside or outside the network).
*   **Universal Verification:** Every user, device, and process must authenticate and prove identity for **every** access request.
*   **Key Components:**
    *   **Multi-Factor Authentication (MFA)** for all logins.
    *   **Encryption** for data at rest and in transit.
    *   **Micro-segmentation** (additional firewalls and controls).
    *   **Strict Policies** and continuous monitoring.

---

## 3. Functional Planes of Operation
To implement Zero Trust, security devices (physical, virtual, or cloud) are broken into two distinct planes:

| Plane             | Function        | Responsibilities                                                                                                                                       |
| :---------------- | :-------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Data Plane**    | The **Doer**    | Processes actual traffic in real-time.<br>• Forwards frames and packets.<br>• Handles NAT and routing.<br>• Moves data across the network.             |
| **Control Plane** | The **Manager** | Manages the rules and configuration.<br>• Sets policies and rules.<br>• Defines forwarding and routing tables.<br>• Configures how data *should* move. |

*   **Example:** On a physical switch, the ports where data flows are the **Data Plane**. The software configuration (IP settings, trunking rules, ACLs) resides in the **Control Plane**.
*   **Application:** This separation applies to switches, routers, firewalls, and cloud-based security controls.

---

## 4. Advanced Identity & Access Controls
Zero Trust requires smarter, context-aware authentication rather than simple password checks.

### Adaptive Identity
Security controls are dynamically applied based on the **context** of the request, not just the user's identity.
*   **Context Variables Analyzed:**
    *   **Geolocation:** Is the user accessing from a location matching their usual pattern? (e.g., IP in China accessing US data).
    *   **User Role:** Employee vs. Contractor, Full-time vs. Part-time.
    *   **Connection Type:** Secure corporate Wi-Fi vs. Public hotspot.
    *   **Device Health:** Is the device patched and compliant?
*   **Outcome:** If risk is high, the system automatically requires **stronger authentication** (e.g., step-up MFA).

### Limiting Entry Points
*   Restrict network access to controlled methods only (e.g., physical building access or specific VPNs).
*   Eliminate unsecured entry vectors to reduce the attack surface.

### Policy-Driven Access Control
*   Aggregates all data points (identity, location, behavior) to make a single, intelligent decision.
*   Ensures the entity requesting access is truly who they claim to be.

---

## 5. Security Zones
Zero Trust categorizes the network into **Security Zones** to manage trust relationships based on the communication path.

### Zone Types
| Zone | Description | Trust Level |
| :--- | :--- | :--- |
| **Untrusted Zone** | Public internet, external networks. | **No Trust** |
| **Trusted Zone** | Corporate offices, internal secure areas. | **High Trust** |
| **Internal Zone** | Data centers, critical servers. | **Controlled Trust** |

### Policy Logic
*   **Explicit Denial:** Traffic from an *Untrusted Zone* to a *Trusted Zone* is automatically denied unless explicitly allowed.
*   **Implicit Trust:** Traffic between a *Trusted Zone* (e.g., office) and an *Internal Zone* (e.g., data center) may be trusted by default, but still monitored.
*   **Granularity:** Organizations can create separate zones for departments or specific VPN groups to enforce strict rules between them.

---

## 6. The Zero Trust Enforcement Model
To enforce policies, the architecture relies on three interacting components:
![](../../Images/Pasted%20image%2020260501224240.png)
### 1. Policy Enforcement Point (PEP) - *The Gatekeeper*
*   **Role:** All traffic must pass through the PEP.
*   **Action:** It blocks traffic, gathers context (identity, location, device), and forwards it for a decision. **It does not make the decision.**

### 2. Policy Decision Point (PDP) / Policy Engine - *The Brain*
*   **Role:** The logical decision maker.
*   **Action:** Receives data from the PEP, compares it against **predefined security policies**, and decides:
    *   **Grant** access
    *   **Deny** access
    *   **Revoke** access

### 3. Policy Administrator - *The Messenger*
*   **Role:** Connects the decision to the enforcement.
*   **Action:** Takes the decision from the PDP and sends instructions (and access tokens/credentials) to the PEP to either open or close the gate.


---

## 7. The Zero Trust Workflow
Here is the step-by-step flow of a typical Zero Trust request:

1.  **Request:** A user (Subject) in an **Untrusted Zone** attempts to access a resource via the **Data Plane**.
2.  **Interception:** The **Policy Enforcement Point (PEP)** catches the traffic.
3.  **Data Collection:** The PEP gathers identity and context data and sends it to the **Policy Administrator**.
4.  **Evaluation:** The Policy Administrator forwards the data to the **Policy Engine (PDP)**.
5.  **Decision:** The Engine checks the request against policies and outputs a decision (Allow/Deny).
6.  **Instruction:** The decision is sent back to the **Policy Administrator**, which generates necessary tokens.
7.  **Enforcement:** The Administrator sends the instruction to the **PEP**.
8.  **Result:**
    *   **If Allowed:** PEP permits traffic to flow into the **Trusted Zone** to the Enterprise Resource.
    *   **If Denied:** PEP blocks the traffic immediately.

---

## Summary
Zero Trust transforms security from a static perimeter defense to a dynamic, identity-centric model. By:
1.  Separating **Data** and **Control Planes**.
2.  Using **Adaptive Identity** and **Contextual Analysis**.
3.  Defining strict **Security Zones**.
4.  Automating decisions via the **PEP-PDP-Administrator** loop.

Organizations can prevent lateral movement by attackers and ensure that **every single access request** is verified, regardless of where it originates.