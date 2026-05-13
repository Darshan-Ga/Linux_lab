# Lab 01: Securing Sensitive Assets (Course 2: Play It Safe)

## 🎯 Objective
To apply the **Principle of Least Privilege** by hardening file permissions on a sensitive security report, mitigating the risk of unauthorized data disclosure.

## 🛠️ Scenario
During a mock security audit, I identified a sensitive file (`internal_risk_assessment.txt`) that had world-readable permissions. In a professional environment, this would be a major vulnerability. My goal was to restrict access to only the authorized owner.

## 💻 Technical Execution

### 1. Identify the Vulnerability
I checked the current status of the asset using the long listing command:
`ls -l internal_risk_assessment.txt`
* **Observation:** `-rw-r--r--` (This indicates that the Group and Others have Read access).

### 2. Remediate (Hardening)
Using the **Absolute (Numeric) Method**, I updated the permissions to ensure total confidentiality:
`chmod 600 internal_risk_assessment.txt`
* **Owner (6):** Read + Write access.
* **Group (0):** No access.
* **Others (0):** No access.

### 3. Verification
I verified the change to ensure the security control was active:
`ls -l internal_risk_assessment.txt`
* **Result:** `-rw-------` (Confidentiality successfully enforced).

## 🛡️ Alignment with NIST RMF
This lab aligns with the **Protect** function of the NIST Cybersecurity Framework. By identifying the asset and applying technical controls (permissions), I reduced the attack surface of the system.
