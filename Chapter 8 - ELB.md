# Section 1: Elastic Load Balancing
## ELB
- Elastic Load Balancing automatically distributes incoming application traffic across multiple targets, such as Amazon EC2 instances. This can be done across multiple AZs.
- 3 types of Load Balancer:
  - Application Load Balancer: Best suited for load balacing of HTTP and HTTPS traffic. They operate at Layer 7 and are application-aware. It's an intelligent load balancer.
  - Network Load Balancer: Operating at the connection level(Layer 4), Network Load Balancers are capable of handling millions of requests per second, while maintaining ultra-low latencies. It's Performance Load Balancer.
  - Classic Load Balancer: Lagacy load balancers. You can load balance HTTP/HTTPS applications and use Layer 7-specific features, such as X-Forwarded and sticky sessions. It's Classic/Test/Dev Load Balancer.
## Health Check
- All AWS load balancers can be configured with health checks. Health checks periodically send requests to load balancers registered instances to test their status.
- The status of the instances that are healthy at the time of the health check is InService.
- The status of any instances that are unhealthy at the time of the health check is OutService. The load balancer performs health checks on all registered instances, whether the instance is in a healthy state or an unhealthy state.
- The load balancer routes requests only to the healthy instances. When the load balancer determines an instance is unhealthy, it stops routing requests to that instance.
- The load balancer resumes routing requests to the instance when it has been restored to a healthy state.
## Exam tips:
- Application Load Balancer: Intelligent
- Network Load Balancer: Extreme performance.
- Classic Load Balancer: Dev/test environment.
- You can use health checks to route your traffic to instances or targets that are healthy.
# Section 2: Application Load Balancer
## Layer 7 Load Balancing
- An Application Load Balancer functions at the Application Layer - the seventh layer of the Open Systems Interconnection(OSI) model. After the load balancer receives a request, it evaluates the listener rules in priority order to determine which rule to apply, and then selects a target from the target group for the rule action.
- Listeners: 
  - A listener check for connection requests from clients, using the protocol and port you configure.
  - You define rules that determine how the load balancer routes requests to its registered targets.
  - Each rule consists of a priority, one or more actions, and one or more conditions.
- Rules: When the conditions for a rule are met, then its action are performed. You must define a default rule for each listener, and you can optionally define additional rules.
- Target Groups: Each target group routes requests to one or more registered targets, such as EC2 instances, using the protocol and port number you specify.
## Exam tips:
- Limitations of Application Load Balancers: Application Load Balancer only support HTTP and HTTPS.
## HTTPS Load Balancing:
- To use an HTTPS listener, you must deploy at least one SSL/TLS server certificate on your load balancer. The load balancer uses a server certificate to terminate the frontend connection and then decrypt requests from clients before sending them to the targets.
## Exam tips:
- Listener: A listener checks for connection requests from client, using the protocol and port you configure.
- Rules: Determine how the load balancer routes requests to its registered targets. Each rule consists of a priority, one or more actions, and one or more conditions.
- Target Groups: Each target group routes requests to one or more registered targets, such as EC2 instances, using the protocol and port number you specify.
- Limitation: Application Load Balancer only support HTTP and HTTPS.
- HTTPS: To use an HTTPS listener, you must deploy at least 1 SSL/TLS server certificate on your load balancer. The load balancer uses a server certificate to terminate the frontend connection and then decrypt requests from clients before sending them to the targets.
# Section 3: Network Load Balancer
## Layer 4 Load Balancing
- A Network Load Balancer functions at the fourth layer of the Open Systems Interconnection(OSI) model. It can handle millions of requests per second.
## Request Received
- After the load balancer receives a connection request, it selects a target from the target group for the default rule.
- It attempts to open A TCP connection to the selected target on the port specified in the listener configuration.
## Listeners
- A listener checks for connection requests from clients, using the protocol and port you configure.
- The listener on a Network Load Balancer then forward the request to the target group. There are no rules, unlike with Application Load Balancer.
## Target Groups
- Each target group routes request to one or more registered targets, such as EC2 instances, using the protocol and port number you specify.
## Encryption
- You can use a TLS listener to offload the work of encryption and decryption to your load balancer so your applications can focus on their business logic.
- If the listener protocol is TLS, you must deploy exactly one SSL server certificate on the listener.
## Exam tips:
- Network Load Balancers are best suited for load balacing of TCP traffic where extreme performance is required. Operating at the connection level(Layer 4), Network Load Balancers are capable of handling millions of requests per second, while maintaining ultra-low latencies.
- Use where you need extreme performance.
- Other use cases are where you need protocols not supported by Application Load Balaner
- Network Load Balancers can decrypt traffic, but you will need to install the certificate on the load balancer.
# Section 4: Classic Load Balancers
