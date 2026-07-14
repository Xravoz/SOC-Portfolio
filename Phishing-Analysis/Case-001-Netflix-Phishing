# Phishing Email Investigation Report

**Case ID:** SOC-2026-001  
**Analyst:** Mohamed Khater  
**Investigation Date:** 14 July 2026  
**Severity:** High  
**Category:** Phishing Email  

---

# Executive Summary

A suspicious email impersonating **Netflix** was investigated after being identified as a potential phishing attempt. The email claimed that the recipient's Netflix account had been placed on hold due to billing issues and requested immediate action to update payment information.

During the investigation, multiple phishing indicators were identified, including spoofed sender domains, email authentication failures, malicious URL redirection, and social engineering tactics. Based on the collected evidence, the email was classified as **Confirmed Phishing**.

---

# Email Information

| Field | Value |
|--------|-------|
| Subject | Your Netflix Account is on Hold |
| Display Name | Netflix |
| Recipient | redacted@yahoo.com |
| Date | 07 July 2021 |
| Return-Path | postmaster@etekno.xyz |
| Sender Domain | JGQ47wazXe1xYVBrkeDg-JOg7ODDQwWdR@JOg7ODDQwWdR-yVkCaBkTNp.gogolecloud.com |

---

# Investigation Methodology

The following investigation workflow was performed:

1. Initial Email Triage
2. Header Analysis
3. Sender Verification
4. Email Authentication Review
5. URL Analysis
6. IOC Extraction
7. MITRE ATT&CK Mapping
8. Risk Assessment
9. Final Classification

---

# Initial Triage

## Observations

The email impersonates **Netflix** and informs the recipient that their account has been placed on hold because of payment issues.

The email encourages immediate action by clicking the **"UPDATE ACCOUNT NOW"** button.

### Initial Findings

- Netflix branding is used.
- Urgent language is present.
- Requests payment information.
- Includes a shortened URL.
- Uses suspicious sender infrastructure.

---

# Header Analysis

## Return-Path

```text
postmaster@etekno.xyz
```

### Analysis

The **Return-Path** belongs to `etekno.xyz`, which is unrelated to Netflix.

A legitimate Netflix email would normally use a `netflix.com` domain.

**Result:** Suspicious

---

## Sender Domain

```text
JOg7ODDQwWdR-yVkCaBkTNp.gogolecloud.com
```

### Analysis

The sender domain is not owned by Netflix.

The domain also appears to imitate Google's infrastructure:

```text
gogolecloud.com
```

instead of

```text
googlecloud.com
```

This technique is known as **Typosquatting**, where attackers register domains that closely resemble trusted brands.

**Result:** High Confidence Phishing Indicator

---

## SPF

```text
Received-SPF: none
```

### Analysis

The sender domain could not verify that the sending server was authorized to send emails on its behalf.

**Result:** Authentication Failure

---

## DKIM

```text
dkim=unknown
```

### Analysis

A valid DKIM signature could not be verified.

Email authenticity cannot be confirmed.

**Result:** Authentication Failure

---

## DMARC

```text
dmarc=unknown
```

### Analysis

DMARC validation could not be confirmed.

The sender failed to demonstrate proper domain authentication.

**Result:** Authentication Failure

---

# URL Analysis

## Embedded URL

```text
https://t.co/yuxfZm8KPg?amp=1
```

### VirusTotal Result

**Verdict:** Malicious

### Redirect Chain

```text
https://t.co/yuxfZm8KPg
        ↓
https://bit.ly/2TiRpyj
```

### Analysis

The attacker used multiple URL shortening services to hide the final destination.

This technique is commonly used to evade security filters and deceive users.

**Result:** Malicious URL

---

# IP Analysis

## Originating IP

```text
209.85.167.226
```

| Property | Value |
|----------|-------|
| Organization | Google LLC |
| ASN | AS15169 |
| Country | United States |

### Analysis

Although the IP belongs to Google LLC, this **does not** prove the email is legitimate.

Cloud providers such as Google are frequently used as part of email delivery infrastructure or abused by attackers.

The email should be evaluated using multiple indicators rather than relying solely on IP ownership.

---

# Social Engineering Analysis

| Technique | Present |
|-----------|---------|
| Brand Impersonation | ✅ |
| Urgency | ✅ |
| Fear | ✅ |
| Payment Request | ✅ |
| Account Suspension | ✅ |

### Analysis

The attacker attempts to pressure the victim into acting quickly by claiming the Netflix account has been suspended due to payment issues.

This is a common phishing technique designed to trigger emotional responses and reduce critical thinking.

---

# Indicators of Compromise (IOCs)

| Type | Value |
|------|-------|
| Fake Sender Domain | gogolecloud.com |
| Return-Path Domain | etekno.xyz |
| Malicious URL | https://t.co/yuxfZm8KPg |
| Redirect URL | https://bit.ly/2TiRpyj |
| Originating IP | 209.85.167.226 |

---

# MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Initial Access | Phishing: Spearphishing Link | T1566.002 |

---

# Risk Assessment

| Category | Rating |
|----------|--------|
| Likelihood | High |
| Impact | High |
| Overall Severity | High |

---

# Recommendations

- Block the sender domain.
- Block the malicious URLs.
- Add the identified IOCs to security monitoring systems.
- Increase monitoring for similar phishing campaigns.
- Educate users on phishing awareness.
- Enable Multi-Factor Authentication (MFA).

---

# Final Verdict

## Classification

**Confirmed Phishing Email**

### Justification

The investigation identified multiple independent indicators supporting the phishing classification:

- Spoofed sender identity.
- Typosquatted domain (`gogolecloud.com`).
- Suspicious Return-Path (`etekno.xyz`).
- Missing or invalid SPF, DKIM, and DMARC authentication.
- Malicious URL identified by VirusTotal.
- Multiple URL redirections using URL shorteners.
- Strong social engineering tactics involving urgency and payment verification.

Based on the collected evidence, this email is classified as a **High-Confidence Phishing Email**.

---

# Lessons Learned

This investigation demonstrates that email legitimacy should **never** be determined using a single indicator.

Although the originating IP belonged to **Google LLC**, multiple independent indicators—including sender inconsistencies, authentication failures, malicious URL behavior, and social engineering tactics—provided sufficient evidence to classify the email as phishing.

A SOC Analyst should always correlate multiple artifacts before reaching a final conclusion.
