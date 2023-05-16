# Section 1
## Vertical Scaling
- Build modern
## Horizontal Scaling
- Build more
## The 3 W's of scaling
### What
- What do we scale? 
### Where
- Where do we scale? Database? Server?
### When
- When do we scale?
# Section 2
## What is a Launch Template?
- A Launch Template specifies all of the needed settings that go into building out an EC2 instance. It is a collection of settings that you can configure so you don't have to walk through the EC2 wizard over and over.
## Templates
- More than just autoscaling
- Supports versioning
- More granularity
- AWS Recommended
## Configurations
- Only for scaling
- Immutable
- Limited configuration options
- Don't use them
## Exam tips
- It's critical to understand what goes into a Launch Template. You need to know that it includes the AMI, EC2-Instance size, security groups and potentially networking information.
- Launch Templates is the most up to date and flexible way to create a template.
- Launch Configurations is the older version.
- User-Data: User-data is included in the template or configuration.
- Change: Can be versioned, configurations are immutable.
- Networking: Configs don't include networking information. Templates could.
# Section 3
## Auto Scaling Groups
- An Auto Scaling group contains a collection of EC2 instances that are treated as a collective group for purposes of scaling and management.
1/ Define your template
