2025-07-27 15:34
Status: #baby
Tags: [[system design]]
## Main

### Health monitoring
## 🔍 **Why Health Monitoring is Important**

1. **Early Detection of Failures**
    
    - Detect CPU, memory, or disk failures before they affect users.
        
2. **Improved Reliability & Uptime**
    
    - Prevent outages with proactive maintenance.
        
3. **Faster Troubleshooting**
    
    - Pinpoint issues quickly via real-time metrics and logs.
        
4. **Capacity Planning**
    
    - Understand system load to plan for scaling.
        

---

## 🏥 **What to Monitor**

|Category|Examples|
|---|---|
|**System Resources**|CPU, memory, disk I/O, network usage|
|**Application Health**|Response time, error rate, throughput|
|**Infrastructure**|VM health, container status, node availability|
|**Network**|Latency, packet loss, connection errors|
|**Security**|Unauthorized access attempts, firewall logs|
|**Custom Metrics**|Business KPIs, queue size, job success rates|

---

## 🛠️ **Tools for Health Monitoring**

|Type|Examples|
|---|---|
|**Infrastructure Monitoring**|Prometheus, Grafana, Zabbix, Datadog|
|**Application Performance Monitoring (APM)**|New Relic, Dynatrace, AppDynamics|
|**Log Aggregation**|ELK Stack (Elasticsearch, Logstash, Kibana), Splunk|
|**Cloud-native**|AWS CloudWatch, Azure Monitor, GCP Operations Suite|
|**Alerting**|PagerDuty, Opsgenie, VictorOps|

---

## 🚨 **Common Monitoring Patterns**

1. **Health Checks (Liveness & Readiness Probes)**
    
    - Used in Kubernetes & cloud-native environments.
        
    - Liveness = Is it running?
        
    - Readiness = Can it serve traffic?
        
2. **Heartbeat Signals**
    
    - Periodic "I am alive" messages from components.
        
3. **Threshold-based Alerts**
    
    - E.g., Notify if CPU > 85% for 5 minutes.
        
4. **Anomaly Detection**
    
    - Use ML to detect unusual patterns (e.g., sudden traffic spikes).
        

---

## ✅ **Best Practices**

- **Set meaningful SLIs/SLOs** (e.g., 99.9% uptime).
    
- **Monitor from the user's perspective** (end-to-end).
    
- **Automate alerting and escalation**.
    
- **Tag resources and metrics** for traceability.
    
- **Test your monitoring setup** (e.g., simulate failures).
    
- **Visualize trends** with dashboards.

### Availability monitoring
**Availability Monitoring** is a subset of system health monitoring focused specifically on ensuring that **systems, services, and applications are accessible and operational** for end-users. Its primary goal is to detect **downtime or degraded performance** as early as possible.

---

## ✅ **What Is Availability Monitoring?**

It answers the question:

> **"Is the service up and reachable from the user’s perspective?"**

This includes:

- Uptime vs. downtime
    
- Service responsiveness
    
- Error rates
    
- End-to-end connectivity
    

---

## 📊 **Key Metrics for Availability Monitoring**

|Metric|Description|
|---|---|
|**Uptime (%)**|Percentage of time a system is operational (e.g., 99.9%)|
|**Downtime duration**|Time when service was unavailable|
|**Mean Time to Detect (MTTD)**|How fast the system detects an outage|
|**Mean Time to Repair (MTTR)**|How quickly the issue is resolved|
|**Error rate**|% of failed requests or responses (e.g., 500 errors)|
|**Success rate**|% of successful operations (e.g., HTTP 200)|

---

## 🔍 **Availability Monitoring Techniques**

|Technique|Description|
|---|---|
|**Ping Monitoring**|ICMP ping to check if a host is up|
|**Port/Service Checks**|Is a specific service (e.g., HTTP/SSH) reachable?|
|**Synthetic Transactions**|Simulate user actions (e.g., login, checkout)|
|**Heartbeat Mechanism**|Agents/services send periodic "I’m alive" signals|
|**Real User Monitoring (RUM)**|Monitor actual user interactions|
|**API Health Checks**|Monitor API endpoints for expected status/content|

---

## 🛠️ **Popular Tools**

|Tool Type|Examples|
|---|---|
|**Cloud-native**|AWS CloudWatch, Azure Monitor, GCP Operations|
|**External uptime checks**|UptimeRobot, Pingdom, StatusCake, BetterUptime|
|**Self-hosted monitoring**|Prometheus + Grafana, Zabbix, Nagios|
|**Synthetic + real user monitoring**|New Relic, Datadog, Dynatrace, AppDynamics|

---

## ⚠️ **Alerting on Availability**

Set up automatic alerts when:

- Uptime drops below a threshold (e.g., <99.9%)
    
- Services fail health checks
    
- High response time or high error rate
    
- No heartbeat received within X minutes
    

Integrate with:  
→ **Slack, PagerDuty, Opsgenie, Email, SMS**

---

## 📈 **Visualization & Reporting**

- Use dashboards (Grafana, Kibana, CloudWatch Dashboards)
    
- Track trends over time (monthly uptime reports)
    
- SLA & SLO tracking (e.g., alert if <99.5% availability)
    

---

## 🧠 **Best Practices**

1. **Monitor from multiple locations** (user geography matters)
    
2. **Set meaningful SLAs/SLOs/SLIs**
    
3. **Monitor dependencies too** (DNS, DB, 3rd-party APIs)
    
4. **Combine synthetic and real monitoring**
    
5. **Automate incident response** where possible

### Performance monitoring
**Performance Monitoring** is the practice of **measuring and tracking how efficiently a system, application, or infrastructure performs**, with the goal of ensuring **responsiveness, reliability, and optimal user experience**.

It answers:

> **“How fast is the system running and where are the bottlenecks?”**

---

## 🎯 **Goals of Performance Monitoring**

- Detect performance degradation before users complain
    
- Identify slow components or bottlenecks
    
- Ensure Service Level Objectives (SLOs) are met
    
- Enable capacity planning and optimization
    

---

## 📊 **Key Performance Metrics**

|Category|Metric|Description|
|---|---|---|
|**Application**|Response time|Time taken to process a request|
||Throughput|Requests per second (RPS) or transactions/sec|
||Error rate|% of failed requests|
||Request queue length|Backlog of unprocessed requests|
|**System Resources**|CPU, memory, disk I/O, network usage|Utilization of system hardware|
|**Database**|Query execution time|How long queries take|
||Connection pool usage|Active vs. idle connections|
|**Infrastructure**|Container/VM performance|Resource usage, restarts, crashes|
|**Frontend**|Page load time (TTFB, FCP, LCP)|Browser-side performance (Real User Monitoring)|

---

## 🛠️ **Tools for Performance Monitoring**

### 🔍 **Application Performance Monitoring (APM)**

- **New Relic**
    
- **Datadog**
    
- **Dynatrace**
    
- **AppDynamics**
    
- **Elastic APM**
    

### 📈 **Metrics + Visualization**

- **Prometheus + Grafana**
    
- **InfluxDB + Chronograf**
    
- **AWS CloudWatch**, **Azure Monitor**
    

### 🧪 **Synthetic Testing**

- Simulate traffic and measure performance (e.g., k6, JMeter, Locust)
    

### 🔎 **Real User Monitoring (RUM)**

- Collect performance data from actual users (e.g., Google Lighthouse, New Relic Browser, SpeedCurve)
    

---

## ⚠️ **Alerting Based on Performance**

Set alerts for:

- Slow response times (>2 seconds)
    
- High CPU/memory usage
    
- Database query times exceeding thresholds
    
- High number of HTTP 5xx/4xx errors
    

---

## 📌 **Best Practices**

1. **Monitor end-to-end**
    
    - Frontend ➝ Backend ➝ Database ➝ Infrastructure
        
2. **Use baselines and thresholds**
    
    - Detect anomalies (e.g., sudden latency spike)
        
3. **Correlate metrics**
    
    - Link CPU spike with slow queries, or app latency with GC pauses
        
4. **Instrument custom code**
    
    - Add tracing/timing to important business logic
        
5. **Use distributed tracing**
    
    - Track requests across microservices (OpenTelemetry, Jaeger, Zipkin)
        
6. **Visualize trends**
    
    - Use Grafana or APM dashboards to spot long-term patterns

### Security monitoring

**Security Monitoring** is the continuous process of **detecting, analyzing, and responding to security threats, vulnerabilities, and suspicious activities** in real time across your systems, networks, and applications.

It answers:

> 🔐 “Is my system under attack? Has any unauthorized activity occurred?”

---

## 🛡️ **Goals of Security Monitoring**

- Detect breaches or malicious behavior early
    
- Respond to threats before damage is done
    
- Ensure compliance (e.g., ISO 27001, GDPR, HIPAA)
    
- Monitor for insider threats, malware, data exfiltration
    
- Maintain security posture over time
    

---

## 🔍 **What to Monitor**

|Category|What to Monitor|
|---|---|
|**Authentication**|Login failures, brute-force attempts, password changes|
|**Authorization**|Privilege escalation, role changes|
|**Network Traffic**|Suspicious ports, unusual outbound connections|
|**Endpoint Activity**|Malware signatures, unauthorized software|
|**System Logs**|Audit trails, file access, privilege use|
|**Application Logs**|Input validation failures, injection attempts|
|**Cloud Resources**|Misconfigurations, IAM abuse, key leaks|
|**Third-party API usage**|Abuse, rate limits, failed calls|

---

## 🛠️ **Tools for Security Monitoring**

### 🔧 Security Information and Event Management (SIEM)

|Tool|Features|
|---|---|
|**Splunk**|Scalable log collection, alerting, dashboards|
|**Elastic SIEM (ELK)**|Open-source, customizable log analysis|
|**IBM QRadar**|Enterprise-grade threat detection|
|**Azure Sentinel**, **AWS GuardDuty**|Cloud-native SIEMs|

### 🔐 Endpoint Detection & Response (EDR)

- CrowdStrike Falcon, SentinelOne, Microsoft Defender for Endpoint
    

### 🧠 Behavior & Threat Intelligence

- Suricata, Zeek (formerly Bro), Open Threat Exchange (OTX), VirusTotal
    

### 🔎 Log Collectors & Agents

- Filebeat, Fluentd, Logstash, OSSEC, Wazuh
    

---

## 🚨 **Alerting Examples**

|Condition|Alert Triggered|
|---|---|
|>5 failed logins in 1 minute|Possible brute-force|
|SSH login from unknown IP|Suspicious access|
|File accessed by unusual process|Possible malware|
|Admin rights granted outside office hours|Privilege abuse|
|Sudden traffic to known bad IP|Data exfiltration or beaconing|

Alerts can be sent to: **Slack, Email, PagerDuty, SIEM dashboards**

---

## 🧪 **Security Monitoring Use Cases**

1. **Web Application Firewall (WAF) Logs**
    
    - Detect SQL injection, XSS, path traversal attempts
        
2. **Cloud Monitoring (AWS, Azure, GCP)**
    
    - Detect open S3 buckets, unused IAM roles, public instances
        
3. **Insider Threat Detection**
    
    - Monitor file access, unusual behavior from known users
        
4. **Zero Trust & MFA Monitoring**
    
    - Ensure multi-factor is enforced and working
        

---

## ✅ **Best Practices**

1. **Centralize logs and secure them**  
    → Use ELK, Splunk, or Cloud-native tools
    
2. **Apply least privilege principles**  
    → Monitor for privilege misuse
    
3. **Use anomaly-based detection**  
    → Baseline normal activity, flag outliers
    
4. **Automate response**  
    → E.g., auto-block IPs, disable user accounts
    
5. **Regularly review audit logs**  
    → Especially for sensitive resources
    
6. **Integrate threat intelligence feeds**  
    → Flag known malicious IPs/domains automatically
    

---

## 📦 Example: Simple Log Monitoring with Wazuh

- Collects system, auth, app, and firewall logs
    
- Detects brute-force, malware, file integrity violations
    
- Provides dashboards, alerts, and rules out-of-the-box

### Usage monitoring

**Usage Monitoring** refers to the **tracking, recording, and analysis of how users, systems, or resources are used** over time. It’s essential for understanding user behavior, optimizing resources, managing costs, and detecting anomalies.

---

## 🎯 **Why Usage Monitoring Matters**

- Understand **how and when** your system is used
    
- Track **resource consumption** (compute, bandwidth, API calls)
    
- Support **billing, quotas, and cost control**
    
- Detect **abuse, misuse, or inefficiencies**
    
- Optimize system performance and capacity planning
    
- Ensure compliance and auditability
    

---

## 🧩 **Types of Usage Monitoring**

|Category|Monitored Usage Examples|
|---|---|
|**User Activity**|Login times, page views, session duration, feature usage|
|**Resource Usage**|CPU, memory, bandwidth, disk I/O|
|**API Usage**|Number of requests, endpoints hit, user agents|
|**License Usage**|Active licenses, concurrent users, seat allocation|
|**Data Usage**|Storage consumed, data transfer, DB queries|
|**Service Utilization**|Serverless functions, compute instances, containers used|
|**Cloud Consumption**|AWS/GCP/Azure resource usage, costs, scaling events|

---

## 🛠️ **Popular Tools for Usage Monitoring**

|Tool Type|Tools|
|---|---|
|**Telemetry / Metrics**|Prometheus, Grafana, StatsD|
|**User Analytics**|Google Analytics, Mixpanel, Amplitude|
|**Cloud-native monitoring**|AWS CloudWatch, Azure Monitor, GCP Operations|
|**Billing/Quota Tools**|Stripe Metered Billing, Chargebee, custom meters|
|**APM & Logs**|Datadog, New Relic, ELK Stack|
|**Audit & Compliance**|Wazuh, Splunk, CloudTrail (AWS), Audit Logs|

---

## 📈 **Key Metrics to Monitor**

|Metric Type|Example Metrics|
|---|---|
|**Per-user**|Daily active users (DAU), feature usage per session|
|**Per-resource**|Disk read/write per volume, memory per container|
|**Per-endpoint**|Calls per API route, latency, error rate|
|**Per-service**|Requests/sec, job completions, usage time|
|**Quota tracking**|Storage used vs limit, API call quota left|
|**Cost drivers**|$/user/month, bandwidth costs, compute usage|

---

## ⚠️ **Common Alerting Conditions**

|Scenario|Alert Condition|
|---|---|
|API usage spikes|>1000 requests/min|
|User near quota|>90% of storage/API limit|
|Unused licenses or services|No activity in last X days|
|Cost anomalies|Sudden spike in cloud spend|
|Idle resources|Running VMs with 0% CPU for 1 hr|

---

## 📌 **Best Practices**

1. **Log and tag everything**  
    → Track usage by user ID, team, or region
    
2. **Aggregate and analyze**  
    → Use tools like Grafana or BigQuery for trend analysis
    
3. **Set usage thresholds and quotas**  
    → Prevent overconsumption and abuse
    
4. **Separate internal vs external usage**  
    → Helps in chargeback/showback models
    
5. **Expose usage dashboards to users**  
    → Self-service monitoring improves transparency
    

---

## 🧠 Example Use Cases

- **SaaS Billing**: Track feature usage to support pay-as-you-go models
    
- **Cloud Cost Control**: Alert when bandwidth > 100GB/day
    
- **DevOps Optimization**: Identify which services are under/overused
    
- **Security**: Alert if a user downloads >1GB in 10 minutes
    
- **Customer Success**: Identify power users vs dormant ones

## References