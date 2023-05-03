# Section 1
## CloudWatch
- CloudWatch is a monitoring and observability platform that was designed to give us insight into our AWS architecture. it allows us to monitor multiple levels of our applications and identify potential issues.
## CloudWatch features:
### System Metric
- These are metrics that you get out of the box.
- The more managed the service is, the more you get.
### Application Metrics:
- By installing the CloudWatch agent, you can get information from inside your EC2 instances.
### Alarms:
- What's the point of collecting data if you don't do something with it? Alarms can alert you when something goes wrong.
## Metrics: 2 types of metrics
### Default:
- These metrics are provided out of the box and do not require any additional work on your part to configure.
### Custom:
- These metrics will need to be provided by using the CloudWatch agent installed on the host.
## Exam tips:
- What tool do we use to monitor? => CloudWatch
- There are no default alarms. Anything you want to hear about must be created.
- Default vs Custom. AWS can't see past the hypervisor level for EC2 instances.
- Managed Services: The more managed a service is, the more checks you get out of the box.
- Standard vs Detailed: Standard is 5 minutes interval, whereas detailed is 1 minute.
- A period is the length of time associated with a specific Amazon CloudWatch statistic. The default period value is 60 seconds.
# Section 2
## CloudWatch logs
- CloudWatch logs is a tool that allows you to monitor, store and access log files from a variety of different sources. It gives you the ability to query your logs to look for potential issues or data that is relevant to you.
## 3 CloudWatch Logs Terms
- Log event: This is the record of what happended. It contains a timestamp and the data.
- Log Stream: A collection of log events from the same source create a log stream. Think of one continuous set of logs from a single instance.
- Log Group: This iss a collection of log streams. For example, you'd group all your Apache web server logs across hosts together.
## CloudWatch Logs Feature
### Filter Patterns
- You can look for specific terms in your logs. Think 400 errors in your web server logs.
### CloudWatch Logs Insights
- This allows you to query all your logs using a SQL-like interactive solution.
### Alarms
- Once you've identified your trends or patterns, it's time to alert on them.
## Exam tips:
- Goto tool: Generally, favor CloudWatch Logs, unless the exam asks for a real-time solution.
- Alarms: CloudWatch alarms can be used to alert if the filter patterns are found.
- Agent Based: The CloudWatch agent must be installed and configured. It's not automatic.
- SQL: If the exam mentions SQL, think CloudWatch Logs Insights.
