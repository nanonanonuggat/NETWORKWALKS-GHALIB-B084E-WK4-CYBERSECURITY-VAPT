# Mediroza General Hospital — Black-Box Penetration Test

**Networkwalks Academy · Cybersecurity Internship · Week 4 · Batch B084**

## Project Overview

This repository documents a Week 4 black-box web application penetration test of **Mediroza General Hospital**, conducted as part of the Networkwalks Academy Cybersecurity Internship.

The assessment focused on identifying weaknesses in the assigned web application, validating their security impact within the authorized scope, preserving supporting evidence, and preparing remediation recommendations.

The work covered the assessment milestones from initial access and patient-report retrieval through document security analysis, database exposure assessment, and final reporting.

## Engagement Information

| Item | Details |
|---|---|
| Programme | Networkwalks Academy — Cybersecurity Internship |
| Week / Batch | Week 4 — **B084** |
| Project | Mediroza General Hospital |
| Assessment Type | Black-Box Web Application Penetration Test |
| Target | `https://medirozahospital.com` |
| Testing Window | 23–27 November 2026 |
| Authorization | Written authorization recorded in the project brief |
| Prepared By | Ghalib Farras Ahmad |
| Overall Risk Rating | **CRITICAL** |

## Authorization and Scope

Testing was conducted under the written authorization provided for the Networkwalks Academy Week 4 exercise.

**In scope**
- The explicitly authorized target domain: `medirozahospital.com`.
- The externally accessible web application and resources within that target.
- Assessment of authentication, input handling, restricted application areas, document protection, metadata, and exposed data.

**Rules of engagement**
- Testing was limited to the authorized target domain.
- Social engineering was not permitted.
- Denial-of-service testing was not permitted.
- Testing outside the agreed scope was not permitted.

No other domains, subdomains, third-party services, or infrastructure are represented as tested unless separately authorized.

## Assessment Objectives

- Identify externally accessible application entry points and exposed resources.
- Review the patient portal's authentication behaviour and input handling.
- Determine whether restricted patient reports could be accessed.
- Assess the strength of password protection applied to retrieved PDF reports.
- Review document metadata for information disclosure.
- Determine whether publicly exposed backup material contained sensitive records.
- Document the impact, evidence, risk ratings, and remediation recommendations.

## Project Milestones

| Milestone | Objective | Result |
|---|---|---|
| **M1 — Initial Access** | Identify exposed entry points, assess authentication, and retrieve the three designated patient reports. | Achieved |
| **M2 — PDF Security Analysis** | Extract PDF password hashes, perform offline password recovery, and inspect the protected documents. | Achieved; supporting content-view evidence is recorded in the evidence set |
| **M3 — Sensitive Data Exposure** | Review the exposed legacy database backup and assess the staff and shareholder tables. | Achieved |
| **M4 — Final Reporting** | Consolidate findings, evidence references, risk ratings, recommendations, and project status. | Report and progress tracker prepared for final review |

## Executive Summary

The assessment identified a chain of weaknesses that could allow an unauthenticated external user to reach restricted patient resources and retrieve a publicly exposed database backup.

The most significant issues were:

1. A patient-portal authentication bypass. The observed behaviour is consistent with SQL injection; the report distinguishes the observed bypass from the inferred underlying cause.
2. Access to three encrypted pathology PDF reports after the authentication boundary was bypassed.
3. A publicly retrievable database backup containing **30 staff records** and **10 shareholder records**.
4. Weak, guessable passwords protecting the three retrieved PDF reports.
5. Additional weaknesses involving directory listing, session and form hardening, HTTP security headers, `robots.txt` disclosures, technology disclosure, and PDF metadata.

The overall assessment risk is rated **CRITICAL**, driven by the combined impact of the authentication bypass, patient-report exposure, and publicly accessible database backup.

## Findings Summary

The current report records ten findings:

| Finding ID | Finding | Severity |
|---|---|---|
| F-01 | SQL injection authentication bypass in the patient portal | **Critical** |
| F-02 | Patient pathology reports accessible after login bypass | **Critical** |
| F-03 | Publicly downloadable database backup containing staff and shareholder records | **Critical** |
| F-04 | Patient PDF reports protected by weak, guessable passwords | **High** |
| F-05 | Directory listing enabled on the legacy directory | **Medium** |
| F-06 | Session-cookie and login-form hardening gaps | **Medium** |
| F-07 | Missing HTTP security headers | **Low** |
| F-08 | `robots.txt` discloses sensitive application paths | **Low** |
| F-09 | Technology and version disclosure | **Low** |
| F-10 | PDF metadata reveals clinical test categories without decryption | **Low** |

### Risk Distribution

| Severity | Number of Findings |
|---|---:|
| Critical | 3 |
| High | 1 |
| Medium | 2 |
| Low | 4 |
| **Total** | **10** |

These are the ratings in the current project report. They describe the assessment results and should not be interpreted as confirmation that the vulnerabilities remain present after remediation.

## Key Remediation Priorities

1. Correct the patient-portal authentication flaw using parameterized queries or prepared statements, secure password verification, and generic authentication error messages.
2. Enforce server-side authentication and authorization checks before returning patient documents or other restricted resources.
3. Remove database backups from web-accessible directories and store backups outside the public web root with restricted access.
4. Disable directory indexing and review the web root for legacy, temporary, and backup files.
5. Replace weak document-password practices with secure, authenticated document delivery and strong, unique encryption where encryption is required.
6. Harden session cookies and login forms, including appropriate cookie attributes and CSRF protection.
7. Configure appropriate HTTP security headers and minimize unnecessary technology and metadata disclosure.
8. Review access logs and determine the extent of access to exposed patient, employee, and shareholder information.

## Tools Used

| Tool | Purpose |
|---|---|
| Kali Linux | Assessment workstation |
| Burp Suite Community Edition | HTTP interception, site mapping, and request analysis |
| `curl` | HTTP requests, response-header review, and resource verification |
| Nikto | Limited web-server configuration checks |
| John the Ripper / `pdf2john` | Offline analysis of PDF password hashes |
| `mutool` | PDF information and password-authenticated document inspection |
| ExifTool | PDF metadata inspection |
| MariaDB | Local, controlled analysis of the downloaded SQL backup |
| `sha256sum` | Evidence integrity checks |

## Project Deliverables

The project working directory contains the following deliverables and supporting material:

- **Penetration Testing Report** — findings, impact analysis, risk ratings, evidence references, and remediation recommendations.
- **Progress Monitoring Workbook** — dashboard, milestone tracking, daily activity log, evidence register, findings tracker, and open issues.
- **Evidence** — screenshots and source artifacts organized by evidence ID.
- **Logs** — command outputs, HTTP response records, hash manifests, and analysis results.
- **Notes** — scope, authorization references, testing-window information, and evidence-handling records.

Evidence IDs are used to connect the report, screenshots, and supporting logs. Refer to the evidence register for the corresponding artifact and its handling status.

## Learning Outcomes

This project provided practical experience in:

- Black-box web application security assessment.
- Reconnaissance and attack-surface identification.
- Authentication and input-handling analysis.
- SQL injection impact validation.
- Protected-document and PDF password analysis.
- Metadata and information-disclosure assessment.
- Database backup exposure analysis.
- Evidence collection, integrity verification, and report preparation.
- Risk-based remediation planning.

## Disclaimer

This repository documents an educational security assessment performed under written authorization and within the agreed engagement scope.

The findings and techniques are provided for educational and defensive security purposes. Do not access, test, or attempt to reproduce these findings against any system without explicit written authorization from its owner.

The project report and supporting evidence should be handled according to the instructor's publication instructions and the applicable evidence-handling requirements. Do not publish passwords, session tokens, or other authentication secrets.

---

**Networkwalks Academy · Week 4 · Batch B084**  
**Project:** Mediroza General Hospital — Black-Box Penetration Test
