###### Written by Tyler Weiss
### Assignment
This assignment involves analyzing a specific CVE for Zoom from 2/14/24 to understand real-world cybersecurity threat intelligence (CTI). You’ll gather information on this CVE, focusing on the vulnerability, advisories, remediation steps, and relevant data.

For this assignment:
1. Find and take screenshots of the CVE details, the official advisory, the recommended fixes, and any extra useful information.
2. Write a brief explanation of CTI’s role and importance in cybersecurity.
3. Craft an executive summary about the CVE for management, keeping it clear and non-technical, followed by a section with more technical details for those interested.
#### Step 1
Find and take screenshots of the CVE details, the official advisory, the recommended fixes, and any extra useful information.

Zoom Desktop Client for Windows, Zoom VDI Client for Windows, and Zoom Meeting SDK for Windows - Improper Input Validation
CVE-2024-24691

Official Zoom Security Bulletin
https://www.zoom.com/en/trust/security-bulletin/zsb-24008/
CVSS: 9.6 
Severity: Critical
The critical vulnerability affects the following Zoom products and versions:
- Zoom Desktop Client for Windows before version 5.16.5
- Zoom VDI Client for Windows before version 5.16.10 (excluding 5.14.14 and 5.15.12)
- Zoom Meeting SDK for Windows before version 5.16.5
- Zoom Rooms Client for Windows before version 5.17.0
Users can help keep themselves secure by applying the latest updates available at https://zoom.us/download.
![[Pasted image 20240411190806.png]]

NIST CVE Database
https://nvd.nist.gov/vuln/detail/CVE-2024-24691
![[Pasted image 20240411190908.png]]
![[Pasted image 20240411191002.png]]

CWE-20 MITRE Improper Input Validation
https://cwe.mitre.org/data/definitions/20.html
![[Pasted image 20240411192904.png]]

Tenable CVE Database
https://www.tenable.com/cve/CVE-2024-24691
![[Pasted image 20240411191811.png]]
Tenable References:
https://www.theregister.com/2024/02/15/zoom_privilege_escalation/
https://www.hivepro.com/threat-advisory/critical-flaw-in-zoom-windows-apps-allows-privilege-elevation/
https://www.bleepingcomputer.com/news/security/zoom-patches-critical-privilege-elevation-flaw-in-windows-apps/?&web_view=true
https://www.bleepingcomputer.com/news/security/zoom-patches-critical-privilege-elevation-flaw-in-windows-apps/
https://www.securityweek.com/zoom-patches-critical-vulnerability-in-windows-applications/
https://www.zoom.com/en/trust/security-bulletin/ZSB-24008/

Rapid7 Vulnerability Database
https://www.rapid7.com/db/vulnerabilities/zoom-zoom-cve-2024-24691/
![[Pasted image 20240411193422.png]]

CVE Details Database
Exploitability Score: 2.8
Impact Score: 6.0
Attack Vector: Network
Attack Complexity: Low
Privilege Requirements: None
User Interaction: Required
Confidentiality: High
Integrity: High
Availability: High
https://www.cvedetails.com/cve/CVE-2024-24691/
![[Pasted image 20240411194837.png]]

#### Step 2
Write a brief explanation of Cybersecurity Threat Intelligence's (CTI) role and importance in cybersecurity.

CTI is crucial to for businesses and cyber professionals to make informed decisions and reduce the risk of cyber attacks. The sharing of threat information allows cyber professionals to identify possible undetected intrusions, protect against and mitigate future threats, prioritize patching of vulnerable systems, share/create solutions and create awareness of the threat landscape. Threat feeds can also inform and provide Indicators of Compromise (IoC), Indicators of Attack (IoC), malicious URLs and IP addresses, malware signatures and other important  that can be used and deployed to protect networks, systems and applications. In short the sharing of CTI provides the knowledge base necessary to protect our current cyber environments.
#### Step 3
Craft an executive summary about the CVE for management, keeping it clear and non-technical, followed by a section with more technical details for those interested.

A Zoom vulnerability, that effects Windows clients where Zoom is installed, may enable privilege escalation for unauthenticated users via network access meaning a threat actor could attain higher level privileges such as administrator rights by using non-valid input through Zoom software. This vulnerability is labeled as Critical, being uncomplicated to execute and severely effecting all Zoom Clients on Windows systems,  requiring minimal user interaction. This update was reported by Zoom security researchers at their Offensive Security Division. No successful exploits have yet been detected in the wild. To resolve the issue download and install the update from Zoom found at https://zoom.us/download. Limited other details have been disclosed regarding this threat.

Zoom Desktop Client for Windows, Zoom VDI Client for Windows, and Zoom Meeting SDK for Windows - Improper Input Validation
Solution: Applying the latest updates available at https://zoom.us/download.

CVSS: 9.6 
CVE-2024-24691
Severity: Critical

The critical vulnerability affects the following Zoom products and versions:
- Zoom Desktop Client for Windows before version 5.16.5
- Zoom VDI Client for Windows before version 5.16.10 (excluding 5.14.14 and 5.15.12)
- Zoom Meeting SDK for Windows before version 5.16.5
- Zoom Rooms Client for Windows before version 5.17.0

Exploitability Score: 2.8
Impact Score: 6.0
Attack Vector: Network
Attack Complexity: Low
Privilege Requirements: None
User Interaction: Required
Confidentiality: High
Integrity: High
Availability: High

CWE-20 MITRE Improper Input Validation:
https://cwe.mitre.org/data/definitions/20.html
