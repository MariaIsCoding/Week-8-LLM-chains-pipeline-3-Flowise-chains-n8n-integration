# Week 8: Prompt Engineering & LLM Security Analysis Pipeline

## Overview

This lab focused on prompt engineering, LLM chain development, and workflow automation using Flowise, Groq, and n8n. The objective was to design a modular AI-assisted cybersecurity analysis pipeline capable of classifying security alerts, analyzing threat indicators, and recommending incident response actions through chained LLM calls.

The final system simulates a lightweight SOC (Security Operations Center) workflow by transforming raw alert data into structured threat intelligence and actionable response recommendations.

---

## Objectives

- Build three independent Flowise LLM chains for cybersecurity analysis
- Apply prompt engineering principles for structured AI output
- Connect Flowise chatflows to n8n using HTTP API requests
- Automate a multi-stage threat analysis workflow
- Produce machine-readable JSON outputs for downstream automation

---

## Architecture

The pipeline consists of three sequential AI components:

**1. Alert Classifier**
- Classifies raw security alerts by severity
- Output format:
```json
{
  "severity": "HIGH",
  "confidence": 0.8,
  "reasoning": "..."
}
```

**2. Threat Analyzer**
- Interprets classified alerts
- Maps indicators to attack behavior and MITRE ATT&CK techniques
- Output format:
```json
{
  "attack_type": "C2",
  "indicators": [],
  "potential_impact": "...",
  "related_mitre_techniques": [],
  "confidence_assessment": "HIGH"
}
```

**3. Response Recommender**
- Generates actionable incident response recommendations
- Output format:
```json
{
  "immediate_actions": [],
  "investigation_steps": [],
  "containment_strategy": "...",
  "escalation_needed": true
}
```

---

## Tech Stack

- **Flowise**
- **Groq API**
- **Llama 3.3 70B Versatile**
- **n8n**
- **Prompt Engineering**
- **HTTP API Integration**
- **MITRE ATT&CK Framework**

---

## Prompt Engineering Concepts Applied

This lab emphasized five core prompt engineering patterns:

- Role assignment
- Structured JSON output formatting
- Constraint enforcement
- Domain-specific instruction design
- Multi-stage reasoning through chained workflows

Each model was instructed to return strict JSON outputs to ensure compatibility with workflow automation.

---

## Workflow Pipeline

The n8n automation pipeline executes the following sequence:

Manual Trigger  
↓  
Set Security Alert Input  
↓  
HTTP Request → Alert Classifier  
↓  
HTTP Request → Threat Analyzer  
↓  
HTTP Request → Response Recommender  

This enables automated progression from raw alert ingestion to incident response planning.

---

## Example Test Scenario

### Input Alert
```text
Outbound DNS queries to known C2 domain detected from workstation-47
```

### Classification Output
```json
{
  "severity": "HIGH",
  "confidence": 0.8,
  "reasoning": "Outbound DNS queries to a known C2 domain indicate likely malicious activity requiring immediate investigation."
}
```

### Threat Analysis Output
- Attack Type: Command & Control (C2)
- MITRE ATT&CK Techniques:
  - T1041
  - T1064
- Potential impact:
  Data exfiltration, lateral movement, persistent compromise

### Recommended Response
- Isolate affected workstation
- Review DNS/system logs
- Run malware scans
- Rotate credentials
- Escalate to incident response team

---
## Improvements / Future Enhancements

Several improvements could strengthen this pipeline for real-world deployment:

- **Prompt refinement for classification consistency**  
  The Alert Classifier occasionally showed inconsistency in severity assignment for borderline alerts. Prompt constraints and additional few-shot examples could improve classification reliability.

- **Structured output validation**  
  Adding JSON schema validation between workflow steps would ensure malformed model outputs do not break downstream automation.

- **Confidence threshold logic**  
  Low-confidence classifications could trigger manual analyst review instead of automatically progressing through the pipeline.

- **Expanded threat intelligence context**  
  Integrating a retrieval-based knowledge source such as MITRE ATT&CK documentation or internal threat intelligence could improve analysis accuracy.

- **Persistent logging and audit tracking**  
  Storing alerts, classifications, and recommendations in a database would improve traceability and support incident review.

- **Human-in-the-loop escalation workflows**  
  Critical alerts could trigger analyst approval steps rather than relying entirely on automated recommendations.

---

## Key Takeaways

This project demonstrated how LLMs can be orchestrated as modular security analysis components rather than standalone chatbots.

By combining prompt engineering, API-based LLM deployment, and workflow automation, the system transforms free-text alerts into structured threat intelligence and operational response guidance.

This architecture reflects how AI can support real-world cybersecurity triage, analysis, and incident response workflows.

---
