# Why Use

- User Experience
	- Application latency
	- Application outages
- Internal monitoring
	- Reduce customer support requirement
	- Troubleshooting and remediation is easier
	- Prevent issues before the happen
	- Performance and cost
	- Trends (scaling patterns)
	- Learn & improve

# Monitoring

- [[20.1 - CloudWatch|AWS CloudWatch]]
- [[20.3 - X-Ray|AWS X-Ray]]
- [[20.4 - CloudTrail|AWS CloudTrail]]

# Differences

- CloudTrail:  
	- Audit API calls made by users / services / AWS console  
	- Useful to detect unauthorized calls or root cause of changes  
- CloudWatch:  
	- CloudWatch Metrics over time for monitoring  
	- CloudWatch Logs for storing application log  
	- CloudWatch Alarms to send notifications in case of unexpected metrics  
- X-Ray:  
	- Automated Trace Analysis & Central Service Map Visualization  
	- Latency, Errors and Fault analysis  
	- Request tracking across distributed systems