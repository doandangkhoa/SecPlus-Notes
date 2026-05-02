## 1. Overview
While the Change Management process defines *what* needs to change, the **Change Control process** from a technician's perspective focuses on *how* to implement these changes safely. Managing updates for tens, hundreds, or thousands of devices is significantly more complex than updating a single home device.

## 2. Application Control: Allow Lists vs. Deny Lists
Technicians often implement changes to application security lists to mitigate risks from malware or known vulnerabilities.

| Type | Description | Flexibility |
| :--- | :--- | :--- |
| **Allow List** | Only explicitly named applications can run. Everything else is blocked. | High Security, Low Flexibility |
| **Deny List** | All applications can run *except* those specifically named. | High Flexibility, Lower Security |

*   **Example:** Antivirus software acts as a massive deny list, blocking specific malicious code while allowing everything else.

## 3. Adhering to Scope and Documentation
*   **Strict Adherence:** A change control document defines a specific scope (e.g., a 2-hour window to upgrade printer drivers). Technicians **must not** perform unrelated changes just because time is available.
*   **Scope Expansion:** If the primary change requires an additional step (e.g., modifying a config file to make the driver upgrade work), technicians may be authorized to perform this if it is simple and documented.
*   **Documentation:** A well-documented process is essential so that everyone understands the protocol for expanding scope when necessary.

## 4. Managing Downtime and Windows
*   **Scheduling:** Changes are typically scheduled during **non-production hours** (overnight) to minimize impact.
*   **24/7 Environments:** For systems that must run continuously, a **primary/secondary system** approach is used:
    1.  Switch users to the secondary system.
    2.  Update the primary system.
    3.  Switch users back seamlessly.
    4.  **Fallback:** If issues arise, simply switch users back to the untouched secondary system.
*   **Communication:** Users must be notified of potential outages via email or a centralized change control calendar.

## 5. Rebooting and Service Restarts
Rebooting is often a critical final step to verify system recovery and apply changes.
*   **Types of Restarts:**
    *   Full OS reboot (power cycle).
    *   Restarting specific services (e.g., via Windows Services, Task Manager, or Linux daemons).
    *   Closing and restarting user applications.
*   **Benefit:** Testing the reboot process ensures the system can recover properly from unexpected power outages.

## 6. Handling Legacy Applications
Legacy applications are often unsupported, undocumented, and critical to operations.
*   **Challenge:** No one in the organization understands how they work or supports them.
*   **Solution:**
    1.  Document the installation and operation of the legacy app.
    2.  Bring it into the normal support cycle.
    3.  Build internal expertise to manage idiosyncrasies of older OS/app combinations.

## 7. Managing Dependencies
Updates often have **dependencies**, requiring a specific order of operations.
*   **Scenario:** Updating Firewall Management Software might require updating the Firewalls themselves first.
*   **Impact:** A simple update can cascade into multiple system updates, complicating the change control window.

## 8. Documentation and Version Control
Since "the only constant is change," documentation must be dynamic.
*   **Live Documentation:** Network diagrams, IP addresses, and procedures must be updated immediately after a change.
*   **Version Control:** Essential for tracking:
    *   Router configurations.
    *   OS patches.
    *   Registry changes.
    *   Application versions.
*   **Rollback:** Version control allows teams to revert to a previous known-good state if a change causes failure.
*   **Tools:** Utilize built-in versioning in OS/Apps or third-party management systems to track changes between "Point A and Point B."