# AWS EC2 Decision Framework

| Category | Decision Criteria | Description |
|----------|-------------|-------------|
| **AMI** | Amazon Linux | Fast, secure, and optimized. Default choice. |
| **AMI** | Ubuntu | Flexible, widely used, and great for containers. |
| **AMI** | Windows AMI | Supports .NET and SQL Server. Licensing applies. |
| **AMI** | Custom AMIs | Save setup time with preconfigured environments. |
| **Instance Type** | General Purpose | Balances CPU, memory, and cost. Best for most workloads. |
| **Instance Type** | Compute Optimized | Ideal for high CPU workloads like gaming. |
| **Instance Type** | Memory Optimized | Best for databases, caching, and big data. |
| **Instance Type** | Storage Optimized | Handles fast, high throughput disk access. |
| **Cost & Pricing** | On Demand | Flexible. Pay per use, no commitments. |
| **Cost & Pricing** | Reserved Instances | Save cost for steady workloads. 1-3 yr term. |
| **Cost & Pricing** | Spot Instances | Cheap but can terminate anytime. |
| **Cost & Pricing** | Savings Plans | Cut costs with flexible usage commitments. |
| **Instance Type** | vCPUs | Affect compute power. More cores for high perf apps. |
| **Instance Type** | RAM | Impacts speed. Use more for caching and databases. |
| **Placement** | Placement Groups | Optimize latency and instance distribution. |
| **Placement** | Nitro System | Enhances security and performance. |
| **Lifecycle & Recovery** | Stop and Start | Keeps EBS data but resets RAM. |
| **Lifecycle & Recovery** | Hibernate | Preserves RAM and state for faster boot. |
| **Lifecycle & Recovery** | Auto Recovery | Restarts failed instances automatically. |
| **Cost & Pricing** | Spot Fleets | Scale workloads with the lowest cost instances. |