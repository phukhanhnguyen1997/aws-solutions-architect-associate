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
