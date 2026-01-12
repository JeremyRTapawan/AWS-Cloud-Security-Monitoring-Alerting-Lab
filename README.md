# AWS Cloud Security Monitoring & Alerting Lab

## Overview
This project demonstrates cloud security monitoring and detection using **AWS CloudTrail** and **Amazon CloudWatch Logs Insights**. A limited-permission IAM user was used to intentionally generate unauthorized API activity, allowing for the detection, analysis, and alerting of suspicious authorization failures in a controlled lab environment.

The lab simulates real-world cloud security monitoring tasks performed by SOC analysts and cloud security engineers.

---

## Objectives
- Enable and analyze AWS CloudTrail logs for security monitoring
- Detect unauthorized API activity (`AccessDenied` events)
- Query and investigate logs using CloudWatch Logs Insights
- Convert detections into actionable alerts
- Document findings using SOC-style investigation workflows

---

## Architecture
**IAM User → AWS API Calls → CloudTrail → CloudWatch Logs → Logs Insights → Alerts**

**Components:**
- AWS CloudTrail (API activity logging)
- Amazon CloudWatch Logs
- CloudWatch Logs Insights
- IAM (test user with restricted permissions)

---

## Lab Environment
- **Cloud Provider:** AWS
- **Logging:** CloudTrail
- **Monitoring & Detection:** CloudWatch Logs Insights
- **Alerting:** CloudWatch Alarms
- **IAM User:** Limited-permission test user

---

## Detection Logic

### AccessDenied Event Detection
The following CloudWatch Logs Insights query was used to identify unauthorized API calls:

```sql
fields @timestamp, eventName, errorCode, userIdentity.userName, sourceIPAddress
| filter errorCode = "AccessDenied"
| sort @timestamp desc
