" SOC Alert Triage "

SECTION 1 - ALERT

1. What is a Security Alert?

A security alert is a notification generated when activity is considered suspicious or requires a security analyst's attention.

An alert does not automatically mean that an attack has occurred. The detected activity could also have a legitimate explanation.

For example; An employee may forget their password and generate multiple failed login attempts before successfully logging in. The SOC analyst must investigate the activity and determine whether it is legitimate, suspicious, or malicious.

SECTION 2 - TRIAGE

2. Alert Triage

Alert triage is the initial assessment of a security alert to
understand what happened, determine how suspicious it is, and
decide whether it requires further investigation.

During triage, a SOC analyst looks at important details such as:

- Who was involved?
- What happened?
- When did it happen?
- Where did the activity come from?
- Was the activity expected or legitimate?
- How serious could the activity be?
- Does it require further investigation or escalation?

The goal of triage is to quickly determine whether an alert should
be closed, investigated further, or escalated to another analyst or
security team.

SIMPLE FLOW : 

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


SECTION 3 - INVESTIGATION 

3. Investigation

Investigation is the process of examining a suspicious alert to understand what happened and determine whether the activity is legitimate, suspicious, or malicious.

A SOC analyst looks at multiple related events instead of relying on a single event. This helps build a timeline and understand the full activity.

# Example

Suppose an alert shows:

- Multiple failed logons
- A successful logon
- PowerShell execution
- A connection to another internal server

Instead of looking at these events separately, I would correlate them and investigate what happened after the successful logon.

I would check the account, source IP, processes, commands, and destination system.

This activity would be considered suspicious, but it would not automatically prove that the system was compromised. More evidence would be required.

# Key Lesson

A SOC analyst should correlate related events and investigate the activity in context rather than making a decision based on a single event.

SECTION 4 - SEVERITY & PRIORITY

4.Severity

Severity describes how serious the potential impact of a security event or incident could be.

5.Priority

Priority describes how urgently the SOC team should respond to the alert.

Severity and priority are related, but they are not always the same.

# Example

A suspicious login on a normal employee workstation may have medium severity.

The same activity on a Domain Controller could have a much higher priority because a compromise could affect many systems.

# Key Lesson

Severity = How serious could it be?

Priority = How urgently should we handle it?


SECTION 5 - FALSE & TRUE POSITIVES

a)False Positive

A false positive occurs when an alert is triggered, but the activity is actually legitimate and not a security threat.

b)True Positive

A true positive occurs when an alert correctly detects activity that is genuinely suspicious or malicious.

# Example

An employee enters the wrong password several times and then successfully logs in.

If the activity is confirmed as normal user behavior, the alert is a false positive.

If an attacker repeatedly attempts passwords and eventually successfully logs in, the alert is a true positive.

# Key Lesson

False Positive = Alert triggered, but no real threat.

True Positive = Alert correctly detected a real threat.

SECTION 6 - IOC vs IOA

a) IOC (Indicator of Compromise)

An IOC is a piece of evidence that may indicate that a system has
been compromised.

Examples include malicious IP addresses, domains, file hashes, URLs, and suspicious files.

b) IOA (Indicator of Attack)

An IOA is a behavior or activity that may indicate an ongoing or attempted attack.

Examples include repeated failed logons, credential dumping, suspicious PowerShell execution, and unusual network connections.

# Example

A known malicious file hash found on a computer is an IOC.

If that file is executed using PowerShell, the execution behavior can
be considered an IOA.

# Key Lesson

IOC = What evidence was left behind?

IOA = What suspicious behavior is happening?

SECTION 7 - MITRE ATT&CK

MITRE ATT&CK is a knowledge base that describes common techniques used by attackers during different stages of an attack.

It helps SOC analysts understand attacker behavior and map observed activity to known attack techniques.

# Example

Suppose an attacker uses PowerShell to execute commands on a Windows machine.

A SOC analyst can map this activity to:

    Tactic: Execution
    Technique: Command and Scripting Interpreter
    Sub-technique: PowerShell

This helps the analyst understand what the attacker is trying to achieve and how they are doing it.

# Key Lesson

Tactic = Why the attacker is doing it

Technique = How the attacker is doing it

SECTION 8 - DETECTION

A detection rule identifies activity that may require investigation.
Good detections often combine multiple related events instead of alerting on a single event.

# Example

A detection can look for:

- 10 or more failed Windows logons (Event ID 4625)
- Followed by a successful logon (Event ID 4624)
- From the same source within a short period

This could indicate a possible password attack followed by a successful login.

The SOC analyst would then investigate the account, source IP, target system, and activity after the successful login.

# Key Lesson

A detection identifies suspicious activity; investigation determines what actually happened.

SECTION 9 - ESCALATION 

Escalation means passing a suspicious or confirmed security issue to a higher-level analyst or security team when it requires further investigation or response.

A SOC analyst should escalate when the available evidence suggests that the activity could have a significant security impact or cannot be safely resolved at the current level.

# Example

If an alert shows:

- Multiple failed logons
- A successful logon
- Suspicious PowerShell activity
- A connection to another internal server

I would collect the available evidence and escalate the alert to L2 for deeper investigation.

# Key Lesson

Escalate when the activity requires deeper investigation or a higher level of response.

-----------------------------------------------------

10. LESSONS LEARNED AO FAR : 

Alert triage is not about immediately deciding whether an alert is
malicious.

A SOC analyst should understand the alert, investigate related activity, correlate events, and make a decision based on available evidence.

# Key Points

- An alert does not always mean an attack occurred.
- Investigate events in context.
- Correlate multiple events to build a timeline.
- Use IOCs and IOAs to support the investigation.
- Consider severity and priority when handling alerts.
- Escalate when deeper investigation is required.

# Key Lesson

Good SOC analysis is based on evidence, context, and correlation — not assumptions.