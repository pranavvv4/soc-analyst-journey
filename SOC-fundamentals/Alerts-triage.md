# SOC Alert Triage

## 1. Alert

### What is a Security Alert?

A security alert is a notification generated when activity is considered suspicious or requires a security analyst's attention.

An alert does not automatically mean that an attack has occurred. The detected activity could also have a legitimate explanation.

### Example

An employee may forget their password and generate multiple failed login attempts before successfully logging in.

The SOC analyst must investigate the activity and determine whether it is legitimate, suspicious, or malicious.

> [!NOTE]
> **Alert ≠ Attack**
>
> An alert only indicates that something may require investigation.

---

## 2. Triage

### What is Alert Triage?

Alert triage is the initial assessment of a security alert to understand what happened, determine how suspicious it is, and decide whether it requires further investigation.

During triage, a SOC analyst looks at important details such as:

- **Who** was involved?
- **What** happened?
- **When** did it happen?
- **Where** did the activity come from?
- Was the activity expected or legitimate?
- How serious could the activity be?
- Does it require further investigation or escalation?

The goal of triage is to quickly determine whether an alert should be closed, investigated further, or escalated.

### Simple Flow

```text
Alert
  ↓
What happened?
  ↓
Who?
  ↓
When?
  ↓
Where?
  ↓
Is it legitimate?
  ↓
How serious?
  ↓
Close / Investigate / Escalate

[!IMPORTANT] Triage is the initial assessment. It is not the same as a full investigation.

## 3. INVESTIGATION

### Investigation

Investigation is the process of examining a suspicious alert to understand what happened and determine whether the activity is legitimate, suspicious, or malicious.

A SOC analyst looks at multiple related events instead of relying on a single event. This helps build a timeline and understand the full activity.

### Example

Suppose an alert shows:

- Multiple failed logons
- A successful logon
- PowerShell execution
- A connection to another internal server

Instead of looking at these events separately, I would correlate them and investigate what happened after the successful logon.

I would check the account, source IP, processes, commands, and destination system.

This activity would be considered suspicious, but it would not automatically prove that the system was compromised. More evidence would be required.

> [!IMPORTANT]
> A SOC analyst should correlate related events and investigate the
> activity in context rather than making a decision based on a single
> event.


## 4. SEVERITY & PRIORITY

### Severity

Severity describes how serious the potential impact of a security event or incident could be.

### Priority

Priority describes how urgently the SOC team should respond to the alert.

Severity and priority are related, but they are not always the same.

### Example

A suspicious login on a normal employee workstation may have medium severity.

The same activity on a Domain Controller could have a much higher priority because a compromise could affect many systems.

> [!IMPORTANT]
> **Severity = How serious could it be?**
>
> **Priority = How urgently should we handle it?**


## 5. FALSE & TRUE POSITIVES

### False Positive

A false positive occurs when an alert is triggered, but the activity is actually legitimate and not a security threat.

### True Positive

A true positive occurs when an alert correctly detects activity that is genuinely suspicious or malicious.

### Example

An employee enters the wrong password several times and then successfully logs in.

If the activity is confirmed as normal user behavior, the alert is a **false positive**.

If an attacker repeatedly attempts passwords and eventually successfully logs in, the alert is a **true positive**.

> [!IMPORTANT]
> **False Positive = Alert triggered, but no real threat.**
>
> **True Positive = Alert correctly detected a real threat.**


## 6. IOC vs IOA

### IOC — Indicator of Compromise

An IOC is a piece of evidence that may indicate that a system has been compromised.

Examples include:

- Malicious IP addresses
- Malicious domains
- File hashes
- URLs
- Suspicious files

### IOA — Indicator of Attack

An IOA is a behavior or activity that may indicate an ongoing or attempted attack.

Examples include:

- Repeated failed logons
- Credential dumping
- Suspicious PowerShell execution
- Unusual network connections

### Example

A known malicious file hash found on a computer is an **IOC**.

If that file is executed using PowerShell, the execution behavior can be considered an **IOA**.

> [!IMPORTANT]
> **IOC = What evidence was left behind?**
>
> **IOA = What suspicious behavior is happening?**


## 7. MITRE ATT&CK

### MITRE ATT&CK

MITRE ATT&CK is a knowledge base that describes common techniques used by attackers during different stages of an attack.

It helps SOC analysts understand attacker behavior and map observed activity to known attack techniques.

### Example

Suppose an attacker uses PowerShell to execute commands on a Windows machine.

A SOC analyst can map this activity to:

```text
Tactic: Execution
Technique: Command and Scripting Interpreter
Sub-technique: PowerShell

## 8. DETECTION

### Detection

A detection rule identifies activity that may require investigation.

Good detections often combine multiple related events instead of alerting on a single event.

### Example

A detection can look for:

- 10 or more failed Windows logons — Event ID 4625
- Followed by a successful logon — Event ID 4624
- From the same source within a short period

This could indicate a possible password attack followed by a successful login.

The SOC analyst would then investigate the account, source IP, target system, and activity after the successful login.

> [!IMPORTANT]
> A detection identifies suspicious activity; investigation determines
> what actually happened.


## 9. ESCALATION

### Escalation

Escalation means passing a suspicious or confirmed security issue to a higher-level analyst or security team when it requires further investigation or response.

A SOC analyst should escalate when the available evidence suggests that the activity could have a significant security impact or cannot be safely resolved at the current level.

### Example

If an alert shows:

- Multiple failed logons
- A successful logon
- Suspicious PowerShell activity
- A connection to another internal server

I would collect the available evidence and escalate the alert to L2 for deeper investigation.

> [!IMPORTANT]
> Escalate when the activity requires deeper investigation or a higher
> level of response.


## 10. LESSONS LEARNED

### Lessons Learned

Alert triage is not about immediately deciding whether an alert is malicious.

A SOC analyst should understand the alert, investigate related activity, correlate events, and make a decision based on available evidence.

### Key Points

- An alert does not always mean an attack occurred.
- Investigate events in context.
- Correlate multiple events to build a timeline.
- Use IOCs and IOAs to support the investigation.
- Consider severity and priority when handling alerts.
- Escalate when deeper investigation is required.

### Key Lesson

> [!IMPORTANT]
> **Good SOC analysis is based on evidence, context, and correlation —
> not assumptions.**