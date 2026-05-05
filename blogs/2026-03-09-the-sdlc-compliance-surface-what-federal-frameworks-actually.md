---
title: "The SDLC compliance surface: what federal frameworks actually require from your build pipeline"
url: "https://earthly.dev/blog/federal-compliance-sdlc-requirements/"
date: "2026-03-09T00:00:00-04:00"
author: "Vlad A. Ionescu"
feed_url: "https://earthly.dev/blog/feed.xml"
---
<p>Federal compliance frameworks collectively contain hundreds of controls. Most address infrastructure, physical security, personnel, and organizational risk management — areas far from the development team’s daily work. But a significant subset targets the SDLC directly: how software is built, tested, scanned, packaged, and deployed.</p>
<p>For platform teams at defense technology companies and federal software vendors, knowing <em>which</em> controls apply to the SDLC — and what they require in practice — determines what to automate. A companion article, <a href="https://earthly.dev/blog/building-software-for-government/">The compliance tax</a>, covers the operational cost of satisfying these requirements manually. This article is the technical counterpart: the specific controls, organized by framework, and what addressing them requires.</p>
<section class="notice--info" id="tldr">
<h3>TL;DR</h3>
<ul>
<li>EO 14028 / NIST SSDF (SP 800-218) maps most directly to SDLC practices — its 42 tasks describe pipeline security, supply chain integrity, and SBOM requirements almost verbatim.</li>
<li>DISA’s Container Image Guide and DevSecOps Playbook map nearly 1:1 to container hardening and pipeline testing categories.</li>
<li>CMMC Level 2 and FedRAMP share overlapping configuration management (CM), system integrity (SI), and risk assessment (RA) controls — several of which carry the maximum criticality weight and cannot be deferred via POA&amp;M.</li>
<li>Across all frameworks, the SDLC-relevant requirements cluster around recurring themes: SBOM generation, security scanning, container hardening, build provenance, secret management, VCS controls, testing, and continuous evidence collection.</li>
</ul>
</section>
<h2 id="the-landscape">The landscape</h2>
<p>The frameworks below differ in scope, specificity, and audience — but they overlap heavily in what they require from software development. A quick orientation before the detailed sections:</p>
<ul>
<li><strong>EO 14028 / NIST SSDF</strong> targets software <em>producers</em> selling to the federal government. It prescribes secure development practices and is the closest thing to a direct SDLC specification among the frameworks covered here.</li>
<li><strong>DISA STIGs</strong> are prescriptive, technology-specific requirements. The Container Image Guide and Application Security STIG contain the most SDLC-relevant controls.</li>
<li><strong>CMMC / NIST 800-171</strong> targets defense contractors handling CUI (Controlled Unclassified Information). Its 110 practices span 14 control families; the SDLC-relevant subset concentrates in Configuration Management, System Integrity, and Audit.</li>
<li><strong>FedRAMP</strong> targets cloud service providers selling to federal agencies. Of its 323 Moderate-baseline controls, the SDLC-relevant ones cluster in the SA, SR, CM, RA, and SI families.</li>
<li><strong>FISMA</strong> and <strong>ITAR</strong> have peripheral SDLC relevance — FISMA governs agency security programs, ITAR controls data access by nationality.</li>
</ul>
<p>The overlap between these frameworks is substantial. SBOM requirements appear in EO 14028, FedRAMP, and CMMC. Vulnerability scanning is required by every framework that touches the pipeline. Container hardening requirements in the DISA STIGs align with NIST 800-53 controls that both CMMC and FedRAMP reference. The sections below catalog the SDLC-relevant requirements framework by framework, then synthesize the cross-cutting themes at the end.</p>
<h2 id="eo-14028-and-the-nist-secure-software-development-framework">EO 14028 and the NIST Secure Software Development Framework</h2>
<p>Executive Order 14028 (May 2021) mandated baseline security requirements for all software sold to the federal government. The implementation framework is the NIST SSDF (<a href="https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-218.pdf">SP 800-218</a>) — 19 practices organized into 42 tasks across four groups: Prepare the Organization (PO), Protect the Software (PS), Produce Well-Secured Software (PW), and Respond to Vulnerabilities (RV).</p>
<p>Of all federal compliance frameworks, the SSDF maps most directly to SDLC automation. Its practices read like a specification for what a pipeline enforcement system should do.</p>
<h3 id="sdlc-relevant-practices">SDLC-relevant practices</h3>
<table>
<colgroup>
<col style="width: 33%;" />
<col style="width: 33%;" />
<col style="width: 33%;" />
</colgroup>
<thead>
<tr class="header">
<th>SSDF Practice</th>
<th>Requirement</th>
<th>What it means technically</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>PS.1.1</td>
<td>Protect code from unauthorized access and tampering</td>
<td>Branch protection, required pull requests, signed commits, CODEOWNERS enforcement</td>
</tr>
<tr class="even">
<td>PS.3.2</td>
<td>Maintain provenance data and SBOM for all components</td>
<td>SBOM generation (CycloneDX or SPDX), license tracking, component inventory</td>
</tr>
<tr class="odd">
<td>PS.2.1</td>
<td>Protect all forms of code from unauthorized access</td>
<td>Build system access controls, artifact registry permissions, CI/CD pipeline security</td>
</tr>
<tr class="even">
<td>PO.3.1–3.3</td>
<td>Specify and verify required tools in the toolchain</td>
<td>SAST, SCA, container scanning, IaC scanning — verified as executed, not just configured</td>
</tr>
<tr class="odd">
<td>PO.4.1–4.2</td>
<td>Define criteria for security checks; track results</td>
<td>Severity thresholds, total finding caps, coverage minimums — with evidence</td>
</tr>
<tr class="even">
<td>PO.5.1–5.2</td>
<td>Separate and protect development/build/test environments</td>
<td>CI/CD environment isolation, MFA on build systems, encrypted credentials, endpoint hardening</td>
</tr>
<tr class="odd">
<td>PW.1.1</td>
<td>Design software to meet security requirements</td>
<td>Threat modeling, security design reviews, documented security architecture</td>
</tr>
<tr class="even">
<td>PW.4.1, 4.4</td>
<td>Acquire and maintain well-secured third-party components</td>
<td>SCA execution, dependency version enforcement, license allow/deny lists</td>
</tr>
<tr class="odd">
<td>PW.5.1</td>
<td>Minimize attack surfaces</td>
<td>Removal of unnecessary endpoints, services, and debug interfaces</td>
</tr>
<tr class="even">
<td>PW.6.1–6.2</td>
<td>Configure the build process securely</td>
<td>Pinned base images, approved registries, no floating tags</td>
</tr>
<tr class="odd">
<td>PW.7.1–7.2</td>
<td>Review and analyze code for vulnerabilities</td>
<td>SAST execution with severity thresholds</td>
</tr>
<tr class="even">
<td>PW.8.1–8.2</td>
<td>Test executable code</td>
<td>Test execution, passing verification, coverage thresholds</td>
</tr>
<tr class="odd">
<td>PW.9.1–9.2</td>
<td>Configure software securely by default</td>
<td>Non-root containers, health checks, resource limits</td>
</tr>
<tr class="even">
<td>RV.1.1–1.2</td>
<td>Identify vulnerabilities on an ongoing basis</td>
<td>Continuous SCA, container scanning, and IaC scanning</td>
</tr>
</tbody>
</table>
<h3 id="the-cisa-attestation-form">The CISA attestation form</h3>
<p>CISA’s <a href="https://www.cisa.gov/sites/default/files/2023-11/Secure%20Software%20Development%20Attestation%20Form_508c.pdf">attestation form</a> (required for software producers selling to federal agencies) distills EO 14028 into four categories, each mapping to concrete SDLC controls:</p>
<ol type="1">
<li><strong>Secure development environments</strong> — branch protection, signed commits, no force-push to protected branches</li>
<li><strong>Trusted source code supply chains</strong> — SCA execution, SBOM generation, approved container registries</li>
<li><strong>Provenance data</strong> — SBOM existence and format validation, digest-pinned container images</li>
<li><strong>Vulnerability management</strong> — SAST, SCA, and container scan execution with severity enforcement</li>
</ol>
<p>OMB <a href="https://www.nextgov.com/cybersecurity/2026/01/omb-reverses-biden-era-software-attestation-order/410939/">rescinded the government-wide mandatory attestation</a> in January 2026 (M-26-05), but individual agencies retain discretion to require it — and Department of War (DoW, formerly DoD) procurement almost certainly will. The underlying SSDF practices remain the de facto standard regardless of attestation status.</p>
<h2 id="disa-stigs-container-and-devsecops-requirements">DISA STIGs: container and DevSecOps requirements</h2>
<p>DISA’s Security Technical Implementation Guides (STIGs) are prescriptive — they specify individual technical requirements with associated IA (Information Assurance) controls. The <a href="https://dl.dod.cyber.mil/wp-content/uploads/devsecops/pdf/DevSecOps_Enterprise_Container_Image_Creation_and_Deployment_Guide_2.6-Public-Release.pdf">Container Image Guide</a> and the <a href="https://www.stigviewer.com/stigs/application_security_and_development/2025-02-12/MAC-2_Public">Application Security &amp; Development STIG</a> contain the most SDLC-relevant requirements.</p>
<h3 id="container-image-creation-container-image-guide-2">Container image creation (Container Image Guide §2)</h3>
<table>
<colgroup>
<col style="width: 25%;" />
<col style="width: 25%;" />
<col style="width: 25%;" />
<col style="width: 25%;" />
</colgroup>
<thead>
<tr class="header">
<th>Req #</th>
<th>Requirement</th>
<th>IA Control</th>
<th>Technical implementation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>2.2</td>
<td>Execute as non-privileged user</td>
<td>AC-6(10)</td>
<td><code>USER</code> directive in Dockerfile, <code>runAsNonRoot</code> in K8s security context</td>
</tr>
<tr class="even">
<td>2.6</td>
<td>Health check instruction required</td>
<td>SC-5</td>
<td><code>HEALTHCHECK</code> in Dockerfile, liveness/readiness probes in K8s</td>
</tr>
<tr class="odd">
<td>2.9</td>
<td>No embedded passwords or credentials</td>
<td>IA-5(1)(a)</td>
<td>Secret scanning in CI (gitleaks, truffleHog), externalized secret management</td>
</tr>
<tr class="even">
<td>2.10</td>
<td>Base images must be signed</td>
<td>CM-5(3)</td>
<td>Digest-pinned base images (no floating tags)</td>
</tr>
<tr class="odd">
<td>2.14</td>
<td>Build from DoW-approved base image (Iron Bank)</td>
<td>SC-8(2)</td>
<td>Allowed registry enforcement configured to Iron Bank</td>
</tr>
<tr class="even">
<td>2.17</td>
<td>Base image from trusted/approved source only</td>
<td>IA-5(2)(a)</td>
<td>Registry allow-list enforcement</td>
</tr>
</tbody>
</table>
<h3 id="container-deployment-container-image-guide-3">Container deployment (Container Image Guide §3)</h3>
<table>
<colgroup>
<col style="width: 25%;" />
<col style="width: 25%;" />
<col style="width: 25%;" />
<col style="width: 25%;" />
</colgroup>
<thead>
<tr class="header">
<th>Req #</th>
<th>Requirement</th>
<th>IA Control</th>
<th>Technical implementation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>3.5</td>
<td>Resource limits on CPU and memory</td>
<td>SC-5(1)</td>
<td>Kubernetes resource requests and limits</td>
</tr>
<tr class="even">
<td>3.7</td>
<td>Read-only root filesystem</td>
<td>SC-28</td>
<td><code>readOnlyRootFilesystem: true</code> in K8s security context</td>
</tr>
<tr class="odd">
<td>3.8</td>
<td>Liveness probe required</td>
<td>SC-5</td>
<td>Kubernetes liveness probe configuration</td>
</tr>
<tr class="even">
<td>3.9</td>
<td>Readiness probe required</td>
<td>SC-5</td>
<td>Kubernetes readiness probe configuration</td>
</tr>
</tbody>
</table>
<h3 id="application-security-development-stig-v6-r2">Application Security &amp; Development STIG (V6 R2)</h3>
<table>
<colgroup>
<col style="width: 33%;" />
<col style="width: 33%;" />
<col style="width: 33%;" />
</colgroup>
<thead>
<tr class="header">
<th>Finding ID</th>
<th>Requirement</th>
<th>Technical implementation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>V-222645</td>
<td>Cryptographic hashing before deployment</td>
<td>SBOM integrity verification, digest-pinned artifacts</td>
</tr>
<tr class="even">
<td>V-222650</td>
<td>Defect tracking for code review flaws</td>
<td>Issue tracker integration, ticket linking enforcement</td>
</tr>
<tr class="odd">
<td>V-222658</td>
<td>Critical vulnerabilities remediated within 21 days</td>
<td>SCA and container scan severity thresholds — enforced, not just reported</td>
</tr>
<tr class="even">
<td>V-222659</td>
<td>No unsupported vendor software (CAT I)</td>
<td>End-of-life detection for dependencies, frameworks, and runtimes via SCA</td>
</tr>
</tbody>
</table>
<h3 id="devsecops-playbook-pipeline-categories">DevSecOps Playbook pipeline categories</h3>
<p>The DoW <a href="https://dl.dod.cyber.mil/wp-content/uploads/devsecops/pdf/DoD-Enterprise-DevSecOps-2.0-Playbook.pdf">DevSecOps Playbook</a> defines expected testing categories for “meaningful pipelines.” Each maps to a concrete CI/CD integration:</p>
<table>
<colgroup>
<col style="width: 50%;" />
<col style="width: 50%;" />
</colgroup>
<thead>
<tr class="header">
<th>Playbook category</th>
<th>Technical requirement</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Static Application Security Testing (SAST)</td>
<td>SAST tool execution with results captured</td>
</tr>
<tr class="even">
<td>Software Composition Analysis (SCA)</td>
<td>SCA tool execution with severity enforcement</td>
</tr>
<tr class="odd">
<td>Container image scanning</td>
<td>Container scan execution with severity enforcement</td>
</tr>
<tr class="even">
<td>Unit and integration testing</td>
<td>Test execution, pass/fail verification, coverage thresholds</td>
</tr>
<tr class="odd">
<td>Dynamic Application Security Testing (DAST)</td>
<td>DAST tool execution against running services</td>
</tr>
<tr class="even">
<td>Infrastructure-as-Code scanning</td>
<td>IaC scan execution with severity enforcement</td>
</tr>
</tbody>
</table>
<p>Some STIG requirements resist pipeline-level automation entirely: SSH disabled in containers (2.1), SECCOMP profile enforcement (3.2), and kernel namespace isolation (3.10) require runtime enforcement mechanisms like Kubernetes admission controllers or pod security standards.</p>
<h2 id="cmmc-level-2-and-nist-800-171">CMMC Level 2 and NIST 800-171</h2>
<p>CMMC (Cybersecurity Maturity Model Certification) Level 2 maps to the 110 security practices in NIST <a href="https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-171r2.pdf">SP 800-171</a>. The majority address infrastructure, access control, and organizational processes. But a meaningful subset — particularly in Configuration Management (CM), System &amp; Information Integrity (SI), Audit &amp; Accountability (AU), and Risk Assessment (RA) — targets the SDLC.</p>
<h3 id="sdlc-relevant-practices-1">SDLC-relevant practices</h3>
<table>
<colgroup>
<col style="width: 25%;" />
<col style="width: 25%;" />
<col style="width: 25%;" />
<col style="width: 25%;" />
</colgroup>
<thead>
<tr class="header">
<th>Practice ID</th>
<th>Requirement</th>
<th>Points</th>
<th>Technical implementation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>AC.L2-3.1.4</td>
<td>Separation of duties</td>
<td>3</td>
<td>Required pull requests, minimum approvals, CODEOWNERS</td>
</tr>
<tr class="even">
<td>AU.L2-3.3.1</td>
<td>Create audit logs of system events</td>
<td><strong>5</strong></td>
<td>CI pipeline tracing, build provenance, deployment records</td>
</tr>
<tr class="odd">
<td>AU.L2-3.3.2</td>
<td>Individual traceability (no shared accounts)</td>
<td>3</td>
<td>Signed commits, ticket linking</td>
</tr>
<tr class="even">
<td>CM.L2-3.4.1</td>
<td>Baseline configurations for build systems</td>
<td>3</td>
<td>Pinned dependencies, approved base images, stable tags</td>
</tr>
<tr class="odd">
<td>CM.L2-3.4.3</td>
<td>Track, review, and approve configuration changes</td>
<td>3</td>
<td>Required pull requests, required status checks, stale review dismissal</td>
</tr>
<tr class="even">
<td>CM.L2-3.4.4</td>
<td>Analyze security impact before changes</td>
<td>3</td>
<td>Required CI status checks, IaC scanning</td>
</tr>
<tr class="odd">
<td>CM.L2-3.4.6</td>
<td>Least functionality</td>
<td>1</td>
<td>Non-root containers, minimal base images</td>
</tr>
<tr class="even">
<td>CM.L2-3.4.8</td>
<td>Software allow-by-exception</td>
<td>3</td>
<td>Allowed container registries, license deny lists</td>
</tr>
<tr class="odd">
<td>CM.L2-3.4.10</td>
<td>System component inventory</td>
<td>1</td>
<td>SBOM generation with component counts</td>
</tr>
<tr class="even">
<td>SI.L2-3.14.1</td>
<td>Flaw remediation in timely manner</td>
<td><strong>5</strong></td>
<td>SCA execution, severity thresholds, dependency version enforcement</td>
</tr>
<tr class="odd">
<td>SI.L2-3.14.2</td>
<td>Malicious code protection</td>
<td><strong>5</strong></td>
<td>SAST execution, container scanning</td>
</tr>
<tr class="even">
<td>SI.L2-3.14.3</td>
<td>Monitor security alerts and advisories</td>
<td><strong>5</strong></td>
<td>Continuous SCA (dependency monitoring)</td>
</tr>
<tr class="odd">
<td>SI.L2-3.14.5</td>
<td>Periodic and real-time scans</td>
<td>3</td>
<td>SCA, SAST, and container scanning at build time</td>
</tr>
<tr class="even">
<td>RA.L2-3.11.2</td>
<td>Vulnerability scanning</td>
<td>3</td>
<td>SCA, SAST, container scanning, IaC scanning</td>
</tr>
<tr class="odd">
<td>CA.L2-3.12.3</td>
<td>Continuous monitoring of security controls</td>
<td>3</td>
<td>Dashboard with real-time standards adherence</td>
</tr>
</tbody>
</table>
<h3 id="the-5-point-controls">The 5-point controls</h3>
<p>CMMC <a href="https://dodcio.defense.gov/Portals/0/Documents/CMMC/AssessmentGuideL2v2.pdf">weights each practice</a> by criticality. Several SDLC-relevant practices carry <strong>5 points</strong> — the maximum weight. These cannot be deferred via a Plan of Action and Milestones (POA&amp;M); failure on any 5-point control means automatic certification failure.</p>
<p>Four 5-point controls map directly to SDLC automation:</p>
<ul>
<li><strong>AU.L2-3.3.1</strong> (audit logs) — requires CI pipeline tracing, build provenance, and deployment records</li>
<li><strong>SI.L2-3.14.1</strong> (flaw remediation) — requires active vulnerability management with timely resolution</li>
<li><strong>SI.L2-3.14.2</strong> (malicious code protection) — requires code scanning at the pipeline level</li>
<li><strong>SI.L2-3.14.3</strong> (security monitoring) — requires continuous dependency and vulnerability monitoring</li>
</ul>
<p>For organizations pursuing CMMC Level 2 certification, these are non-negotiable. They require automated scanning and vulnerability management integrated into the pipeline — periodic manual reviews are insufficient.</p>
<h3 id="scope-and-gaps">Scope and gaps</h3>
<p>CMMC’s remaining practices address physical protection (PE), personnel security (PS), maintenance (MA), media protection (MP), and identification &amp; authentication (IA). These are infrastructure and organizational concerns outside the SDLC’s scope.</p>
<p>One partially addressable area: incident response (IR) plans and awareness &amp; training (AT) documentation increasingly live in git — especially in organizations adopting docs-as-code workflows. To the extent these artifacts are version-controlled, their existence and structure can be verified as part of the development process.</p>
<h2 id="fedramp-the-sa-sr-cm-ra-and-si-families">FedRAMP: the SA, SR, CM, RA, and SI families</h2>
<p>FedRAMP’s baseline contains 323 controls at Moderate impact level, drawn from <a href="https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final">NIST SP 800-53 Rev 5</a>. The SDLC-relevant subset spans five control families: System and Services Acquisition (SA), Supply Chain Risk Management (SR), Configuration Management (CM), Risk Assessment (RA), and System &amp; Information Integrity (SI).</p>
<table>
<colgroup>
<col style="width: 33%;" />
<col style="width: 33%;" />
<col style="width: 33%;" />
</colgroup>
<thead>
<tr class="header">
<th>Control</th>
<th>Requirement</th>
<th>Technical implementation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>SR-3</td>
<td>Establish supply chain controls and processes</td>
<td>Processes to identify and address supply chain weaknesses and vulnerabilities</td>
</tr>
<tr class="even">
<td>SR-4</td>
<td>Document and maintain supply chain provenance</td>
<td>SBOM generation and format validation</td>
</tr>
<tr class="odd">
<td>SA-3</td>
<td>System development life cycle</td>
<td>Defined SDLC incorporating security; protect preproduction environments</td>
</tr>
<tr class="even">
<td>SA-4(10)</td>
<td>Require SBOMs from software suppliers</td>
<td>SBOM existence with license data</td>
</tr>
<tr class="odd">
<td>SA-8</td>
<td>Security and privacy engineering principles</td>
<td>Threat modeling, secure design reviews, security architecture documentation</td>
</tr>
<tr class="even">
<td>SA-10</td>
<td>Developer configuration management</td>
<td>VCS controls, change tracking, integrity verification</td>
</tr>
<tr class="odd">
<td>SA-11</td>
<td>Developer testing and evaluation</td>
<td>SAST, test execution, SCA, flaw remediation with evidence</td>
</tr>
<tr class="even">
<td>SA-15</td>
<td>Development process, standards, and tools</td>
<td>Documented and auditable toolchain</td>
</tr>
<tr class="odd">
<td>CM-2</td>
<td>Baseline configuration under change control</td>
<td>Approved registries, pinned dependencies</td>
</tr>
<tr class="even">
<td>CM-3</td>
<td>Configuration change control</td>
<td>Security impact analysis for changes; test and validate before finalizing</td>
</tr>
<tr class="odd">
<td>CM-7(5)</td>
<td>Least functionality — deny-all/permit-by-exception</td>
<td>Registry allow-lists, license deny-lists</td>
</tr>
<tr class="even">
<td>CM-8</td>
<td>Component inventory</td>
<td>SBOM with version numbers, owners, license data</td>
</tr>
<tr class="odd">
<td>RA-5</td>
<td>Vulnerability scanning</td>
<td>SCA, SAST, container scanning, IaC scanning with machine-readable output</td>
</tr>
<tr class="even">
<td>SI-7</td>
<td>Software and firmware integrity verification</td>
<td>Signed commits, digest-pinned images</td>
</tr>
</tbody>
</table>
<h3 id="fedramp-20x">FedRAMP 20x</h3>
<p><a href="https://www.fedramp.gov/20x/">FedRAMP’s modernization direction</a> (20x) shifts toward continuous automated evidence over periodic manual narratives, OSCAL-formatted machine-readable packages, and persistent validation. Any SDLC compliance automation built today should generate machine-readable evidence as a byproduct of normal development — not as a separate process assembled before audits.</p>
<h3 id="scope-and-gaps-1">Scope and gaps</h3>
<p>FedRAMP’s remaining controls address physical security (PE), personnel security (PS), the 51 System &amp; Communications Protection (SC) controls (encryption, network segmentation, FIPS 140-2), and organizational risk management. These are infrastructure and organizational concerns outside the SDLC.</p>
<p>Contingency planning (CP) and incident response (IR) documentation is a partial overlap — when these artifacts live in git, their existence, structure, and recency can be verified through the same pipeline mechanisms that enforce other SDLC standards.</p>
<h2 id="fisma-and-itar-peripheral-fit">FISMA and ITAR: peripheral fit</h2>
<h3 id="fisma">FISMA</h3>
<p>FISMA (Federal Information Security Modernization Act) governs federal agency information security programs, not vendor software directly. Its SDLC relevance is indirect: agencies evaluating vendor software may reference FISMA’s functional areas — supply chain risk management (GOVERN), software asset management (IDENTIFY), configuration management (PROTECT), and continuous monitoring (DETECT) — when setting procurement requirements. FISMA’s shift toward the Continuous Diagnostics and Mitigation (CDM) program parallels the continuous evidence model, but the overlap is structural rather than prescriptive.</p>
<h3 id="itar">ITAR</h3>
<p><a href="https://www.ecfr.gov/current/title-22/chapter-I/subchapter-M">ITAR</a> (International Traffic in Arms Regulations) controls <em>who</em> can access defense-related technical data — citizenship, deemed exports, DDTC registration — not <em>how</em> software is built. But ITAR has concrete SDLC consequences that are easy to underestimate.</p>
<p>Repositories containing ITAR-controlled data must be private (a public repository constitutes an export). More specifically, private repositories on GitHub.com are not considered ITAR-compliant — GitHub personnel worldwide may have access. The compliant options are GitHub Enterprise Server self-hosted in GovCloud or on-premises. The same constraint extends to all CI/CD tooling: build artifacts, container images, and test results are themselves <a href="https://www.law.cornell.edu/cfr/text/22/120.33">technical data</a> subject to the same access restrictions as source code. SaaS CI/CD services running on public infrastructure are non-compliant for ITAR work.</p>
<p>Every developer with access to ITAR-controlled repos or pipelines must be verified as a U.S. person. Foreign national employees — including those on H-1B, L-1, or OPT visas — cannot be assigned to ITAR projects without a DDTC export license. This affects team composition, access provisioning, and onboarding processes.</p>
<p>The indirect relevance is that ITAR-controlled technical data is classified as CUI, which triggers CMMC Level 2 requirements. The CMMC practices cataloged above cover the cybersecurity side of ITAR compliance.</p>
<h2 id="what-addressing-these-requirements-looks-like">What addressing these requirements looks like</h2>
<p>Across all frameworks, the SDLC-relevant controls cluster around recurring themes. Each represents a category of automation that platform teams need to build or integrate — regardless of which specific framework drives the requirement.</p>
<h3 id="sbom-generation-and-validation">SBOM generation and validation</h3>
<p>Every framework that touches software supply chain requires SBOMs. But the requirements go beyond existence. The <a href="https://www.ntia.gov/files/ntia/publications/sbom_minimum_elements_report.pdf">NTIA Minimum Elements Report</a> specifies seven required data fields (supplier name, component name, version, unique identifiers, dependency relationship, author, timestamp), three approved formats (SPDX, CycloneDX, SWID), and operational practices including: a new SBOM for every build or release, all transitive dependencies listed, and explicit distinction between “no further dependencies” and “dependencies unknown.” Auditors ask follow-up questions beyond existence: Is it in an approved format? Does it contain license data? Are there disallowed licenses? Is the component count plausible, or was the generator misconfigured? Addressing this means generating SBOMs at build time <em>and</em> validating their contents against configurable criteria.</p>
<p><strong>Referenced by:</strong> SSDF PS.3.2, FedRAMP SR-4, SA-4(10), CM-8, CMMC CM.L2-3.4.10, DISA V-222645, CISA Attestation Category 3</p>
<h3 id="security-scanning-enforcement">Security scanning enforcement</h3>
<p>Frameworks require evidence that scans ran and that results fall within acceptable thresholds — not just that scanning tools are configured. This means SAST, SCA, container scanning, and IaC scanning integrated into the pipeline with configurable severity limits, and results captured as structured audit evidence.</p>
<p><strong>Referenced by:</strong> SSDF PO.3.1–3.3, PO.4.1–4.2, PW.7.1–7.2, FedRAMP SA-11, RA-5, CMMC SI.L2-3.14.1–3.14.5, RA.L2-3.11.2, DISA DevSecOps Playbook, CISA Attestation Category 4</p>
<h3 id="container-image-hardening">Container image hardening</h3>
<p>The DISA Container Image Guide maps to specific Dockerfile and Kubernetes manifest practices: non-root execution, health checks, resource limits, approved base images, and digest pinning. These are verifiable at build time through static analysis of Dockerfiles and K8s YAML — no runtime instrumentation required.</p>
<p><strong>Referenced by:</strong> DISA Container Image Guide §2–§3, SSDF PW.6.1–6.2, PW.9.1–9.2, CMMC CM.L2-3.4.6</p>
<h3 id="build-provenance-and-artifact-signing">Build provenance and artifact signing</h3>
<p>Increasingly, frameworks require not just <em>what</em> was built but <em>proof of how</em> it was built. Build provenance — cryptographically signed attestations that link artifacts to their source code, build process, and builder identity — is the technical mechanism. Standards like SLSA (Supply-chain Levels for Software Artifacts) define maturity levels for provenance, from unsigned provenance at Level 1 to hermetic, reproducible builds at Level 3. Signed container images (via cosign/sigstore) and in-toto attestations satisfy the integrity verification requirements that appear across multiple frameworks.</p>
<p><strong>Referenced by:</strong> SSDF PS.3.2, FedRAMP SI-7, CMMC AU.L2-3.3.1, DISA V-222645</p>
<h3 id="secret-scanning-and-credential-management">Secret scanning and credential management</h3>
<p>Embedded secrets — API keys, passwords, tokens checked into source code — are a recurring finding in both audits and incidents. DISA’s Container Image Guide explicitly prohibits embedded credentials (2.9), and CMMC’s malicious code protection requirement (SI.L2-3.14.2) is broadly interpreted to include detecting credential leakage. In practice, this means running secret scanning tools (gitleaks, truffleHog, GitHub secret scanning) in CI and pre-commit hooks, with findings treated as blocking.</p>
<p><strong>Referenced by:</strong> DISA Container Image Guide 2.9, CMMC SI.L2-3.14.2, SSDF PO.3.1</p>
<h3 id="version-control-and-change-management">Version control and change management</h3>
<p>Multiple frameworks require change tracking, access controls, and integrity verification for source code. In practice: branch protection, required pull requests with minimum approvals, required CI status checks, signed commits, and CODEOWNERS enforcement — applied at the organization level, not configured per-repo.</p>
<p><strong>Referenced by:</strong> SSDF PS.1.1, FedRAMP SA-10, SI-7, CMMC AC.L2-3.1.4, CM.L2-3.4.3, AU.L2-3.3.2</p>
<h3 id="testing-and-code-quality">Testing and code quality</h3>
<p>Frameworks require evidence that code is tested — not just that test infrastructure exists. This means verifying that tests executed, passed, and met coverage thresholds, with results captured as auditable artifacts.</p>
<p><strong>Referenced by:</strong> SSDF PW.8.1–8.2, FedRAMP SA-11, DISA DevSecOps Playbook</p>
<h3 id="continuous-evidence-collection">Continuous evidence collection</h3>
<p>The consistent direction across all frameworks — FedRAMP 20x, CMMC’s continuous monitoring requirement (CA.L2-3.12.3), the DevSecOps Playbook’s continuous ATO (cATO) model, FISMA’s CDM program — is that compliance evidence should be generated continuously as a byproduct of development, not assembled retroactively before audits. This requires structured, machine-readable output from every compliance-relevant pipeline step, stored centrally and queryable on demand.</p>
<p><strong>Referenced by:</strong> CMMC CA.L2-3.12.3, FedRAMP 20x, FISMA CDM, DevSecOps Playbook cATO</p>
<h2 id="how-lunar-fits">How Lunar fits</h2>
<p>The requirements cataloged above describe the problem space <a href="https://earthly.dev/">Earthly Lunar</a> was built to address. Lunar is a guardrails engine that centrally instruments repositories and CI/CD pipelines, collects structured SDLC posture data, and continuously evaluates standards in pull requests — generating compliance evidence as a byproduct of normal development.</p>
<p>For the specific frameworks covered here, Lunar ships pre-built guardrails for SBOM validation, security scanning enforcement, container hardening, VCS configuration, testing requirements, and vulnerability management — each with configurable thresholds that map to the practice-level requirements above. For organization-specific requirements that no vendor ships out of the box (specific Iron Bank image lists, contract-specific STIG checks, internal tool version mandates), Lunar’s Bash and Python SDKs allow platform teams to encode custom guardrails — and Lunar ships with Claude and Codex skills that generate and locally test new guardrails in minutes.</p>
<p>A <a href="https://earthly.dev/blog/building-software-for-government/">companion article</a> covers the operational context — the cost of satisfying these requirements manually and the organizational dynamics that make automation necessary.</p>
<p>If the requirements in this article describe what your platform team is working to address, <a href="https://earthly.dev/book-demo/">we’d like to hear from you</a>.</p>
<div class="bg-blue-50 rounded-lg py-6 my-6 cta-container" id="blog-bottom-cta-control">
<div class="mb-4">
<svg class="mb-3 block lunar-logo-cta" fill="none" height="119" viewBox="0 0 501 119" width="501" xmlns="http://www.w3.org/2000/svg">
<path d="M76.0247 30.8587L60.9741 56.9803H60.8721L45.9746 31.1138L76.0247 30.8587Z" fill="#83FF50" stroke="#83FF50" stroke-miterlimit="5.3333" stroke-width="0.510184">  <path d="M86.2689 35.5604H5.45508V0.000343323H86.2689V35.5604Z" fill="white">  <g> <g opacity="0.83"> <path d="M76.156 30.7127L76.105 30.8147H76.054V30.8658L45.9529 31.1208V31.0698H15.8008L15.5967 30.7127L30.7493 4.48903H61.0544L76.156 30.7127Z" fill="#96FF5B" fill-opacity="0.6471"> </g> </g> <path d="M76.0913 30.8193L61.0403 56.9418H60.9893L76.0403 30.8193H76.0913Z" fill="white"> <path d="M61.0593 57.3182L61.0083 57.4202L45.9067 83.5419H15.6526L0.5 57.3182L15.6526 31.0945H15.8056L30.7031 56.9611H60.8553L61.0593 57.3182Z" fill="#00D6FF" stroke="#00D6FF" stroke-miterlimit="5.3333" stroke-width="0.510184"> <path d="M60.8504 56.9579H30.7493L15.8008 31.0914H45.9529L60.8504 56.9579Z" fill="#7DFFFF" stroke="#7DFFFF" stroke-miterlimit="5.3333" stroke-width="0.510184"> <path d="M76.2476 82.8961L76.5027 83.3042H76.0435L64.5642 83.4063L45.9424 83.5593L61.0439 57.4377H90.992L76.2476 82.8961Z" fill="#32E6FF" stroke="#32E6FF" stroke-miterlimit="5.3333" stroke-width="0.510184">  <path d="M99.3161 118.67H38.1445V48.6722H99.3161V118.67Z" fill="white">  <g> <g opacity="0.86"> <path d="M91.6823 109.142L91.2231 109.907H60.969L45.8164 83.6833L45.8674 83.5813L60.969 57.4597H61.02L45.9184 83.5303L64.5403 83.3772L76.0706 83.2752H76.5297L91.3762 109.142H91.6823Z" fill="#00D5FF" fill-opacity="0.5451"> </g> </g> <path d="M76.2471 82.8963L76.5022 83.3044H76.043L61.1455 57.4379H90.9915L76.2471 82.8963Z" fill="#20E6FF" stroke="#20E6FF" stroke-miterlimit="5.3333" stroke-width="0.510184"> <path d="M106.19 83.3025H76.4973L76.2422 82.8943L90.9356 57.436H91.2417L106.19 83.3025Z" fill="#2AF0FF" stroke="#2AF0FF" stroke-miterlimit="5.3333" stroke-width="0.510184">  <path d="M111.413 113.465H71.5156V79.0269H111.413V113.465Z" fill="white">  <g> <g opacity="0.95"> <path d="M106.388 83.663L91.6948 109.121H91.3887L76.4912 83.3058H106.184L106.388 83.663Z" fill="#29EFFF" fill-opacity="0.8"> </g> </g> <path d="M121.491 57.0653L106.338 83.2889H106.185L91.2878 57.4224H61.1357L60.9316 57.0653L60.9827 56.9632L76.0332 30.8416V30.7906H106.338L121.236 56.6061L121.491 57.0653Z" fill="#32F8B9" stroke="#32F8B9" stroke-miterlimit="5.3333" stroke-width="0.510184">  <path d="M144.229 118.67H83.6699V48.2127H144.229V118.67Z" fill="white">  <g> <g opacity="0.85"> <path d="M136.625 83.2665L121.472 109.49L91.2178 109.898L106.217 84.0318L106.013 83.6747H106.166L121.319 57.451L121.064 57.0428H121.523L136.625 83.2665Z" fill="#32F6B8" fill-opacity="0.5647"> </g> </g> <path d="M155.73 81.0842V33.086H176.278V40.3849H162.95V53.4754H172.708V60.7743H162.95V73.7853H176.278V81.0842H155.73Z" fill="#090909"> <path d="M194.371 44.125L191.673 63.0069H197.068L194.371 44.125ZM190.563 70.0678L188.817 81.0955H181.28L189.452 33.1766H199.369L207.382 81.0955H199.766L198.099 70.0678H190.563Z" fill="#090909"> <path d="M229.225 44.6987C229.225 41.922 227.876 40.4939 225.1 40.4939H220.736V55.8058H225.1C226.21 55.8058 227.242 55.4091 228.035 54.6157C228.828 53.8224 229.225 52.791 229.225 51.6803V44.6987ZM224.941 33.1157C228.987 33.1157 231.923 34.2264 233.827 36.4478C235.493 38.3519 236.286 41.1286 236.286 44.5401V51.5216C236.286 54.9331 235.017 57.7892 232.399 60.1692L237.793 81.1139H229.939L225.576 63.0253H224.941H220.736V81.1139H213.517V33.195H224.941V33.1157Z" fill="#090909"> <path d="M249.271 40.4135H241.575V33.1146H264.186V40.4135H256.49V81.1128H249.271V40.4135Z" fill="#090909"> <path d="M277.201 60.7683V81.0782H269.981V33.1594H277.201V53.4694H285.928V33.0801H293.148V80.9989H285.928V60.7683H277.201Z" fill="#090909"> <path d="M319.322 81.0842H299.646V33.1654H306.866V73.8647H319.322V81.0842Z" fill="#090909"> <path d="M325.026 60.9974L315.347 33.0712H323.28L328.675 50.287L333.991 33.0712H342.004L332.245 60.9974V81.0693H325.026V60.9974Z" fill="#090909"> <path d="M491.932 44.6987C491.932 41.922 490.583 40.4939 487.807 40.4939H483.443V55.8058H487.807C488.917 55.8058 489.949 55.4091 490.742 54.6157C491.535 53.8224 491.932 52.791 491.932 51.6803V44.6987ZM487.648 33.1157C491.694 33.1157 494.63 34.2264 496.534 36.4478C498.2 38.3519 498.993 41.1286 498.993 44.5401V51.5216C498.993 54.9331 497.724 57.7892 495.106 60.1692L500.5 81.1139H492.646L488.283 63.0253H487.648H483.443V81.1139H476.224V33.195H487.648V33.1157Z" fill="#49728B"> <path d="M457.229 44.125L454.532 63.0069H459.927L457.229 44.125ZM453.421 70.0678L451.676 81.0955H444.139L452.31 33.1766H462.227L470.24 81.0955H462.624L460.958 70.0678H453.421Z" fill="#49728B"> <path d="M422.21 55.2386V81.0784H414.99V33.1595H422.21L430.937 58.4613V33.0802H438.156V80.999H430.937L422.21 55.2386Z" fill="#49728B"> <path d="M396.539 81.0784V81.0784C390.631 81.0784 385.842 76.2891 385.842 70.3812V33.1595H393.061V69.4812C393.061 71.8911 395.015 73.8447 397.425 73.8447V73.8447C399.835 73.8447 401.788 71.8911 401.788 69.4812V33.0802H409.008V70.3008C409.008 76.2221 404.231 81.0345 398.31 81.0784V81.0784H396.539Z" fill="#49728B"> <path d="M359.312 81.0842V33.086H366.531V40.3849V53.4754V60.7743V73.7853H379.86V81.0842H359.312Z" fill="#49728B">
</svg>
<p class="text-lg font-normal text-gray-700 leading-relaxed">
Turn your engineering standards into automated guardrails that provide feedback directly in pull requests, with 100+ guardrails included out of the box and support for the tools and CI/CD systems you already have.
</p>
</div>
<div class="mt-4">
<p><a class="btn-gradient" href="https://earthly.dev/" target="_blank"> Learn More </a></p>
</div>
</div>
