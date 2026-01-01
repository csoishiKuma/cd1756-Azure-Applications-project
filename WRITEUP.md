# Write-up Template

### Analyze, choose, and justify the appropriate resource option for deploying the app.

*For **both** a VM or App Service solution for the CMS app:*
- *Analyze costs, scalability, availability, and workflow*
- *Choose the appropriate solution (VM or App Service) for deploying the app*
- *Justify your choice*

Azure App Service vs. VM for the CMS (Python/Flask)

For this low-traffic, internal web app, Azure App Service is the better deployment choice. Below is a comparison on cost, scalability, availability, and workflow, with reasons App Service comes out ahead:

    • Cost Efficiency: Running the app on App Service minimizes costs because the platform is fully managed. You pay for a small App Service plan and don’t need to maintain extra capacity or infrastructure – this reduces operational overhead. By contrast, an Azure VM runs 24/7 and incurs costs even when usage is low, and you’d be responsible for OS licensing and maintenance costs on top of that. Given the project’s steady low usage and budget sensitivity, App Service’s pay-for-what-you-use model is more economical.

    • Scalability: Azure App Service provides built-in auto-scaling and load balancing. If usage grows, you can scale out simply by adjusting the instance count or enabling auto-scale rules – the service handles distribution of traffic for you. With a VM, scaling is manual and complex: you would need to set up a VM scale set or additional VMs behind a load balancer to handle increased load. For a small app, this added complexity isn’t justified. App Service can seamlessly handle future traffic spikes without manual intervention, ensuring the app remains responsive as demand fluctuates.

    • High Availability: App Service inherently offers high availability through the platform. Your app can run on multiple instances across Azure’s infrastructure with no extra setup, and Azure handles patching and health for the underlying servers to keep the app online. Achieving comparable availability with VMs requires configuring multiple VM instances in an availability set or across zones and managing a load balancer yourself. In short, App Service delivers reliable uptime out-of-the-box, whereas a single VM could be a single point of failure unless you invest considerably in redundancy.

    • Deployment & Maintenance Workflow: Using App Service means minimal management effort. You can deploy updates easily (through Zip deploy, GitHub Actions, or Azure DevOps pipelines) and Azure takes care of OS updates, security patches, and server maintenance for you. This allows the team to focus on the application code and future CI/CD setup rather than managing servers. In contrast, a VM would require full server administration – you’d need to configure and patch the OS, manage firewalls/SSL, install and update the web server and runtime, and monitor the machine’s health continuously. That overhead is significant for a simple training app. Since there’s no existing DevOps pipeline, App Service’s integrated deployment slots and CI/CD support provide a clear path to add those in the future with minimal effort. Overall, App Service’s PaaS approach streamlines the workflow, reducing maintenance tasks and risk of misconfiguration.

    • Security (Intranet Access): Both solutions can be secured within the Chevron intranet, but App Service makes it straightforward. It supports VNet integration and access restrictions to ensure the app is only reachable from the internal network. This avoids the need to manually manage OS-level firewalls as on a VM. In practice, either option can meet the intranet security requirement, but App Service does so with less setup and automatically keeps the underlying systems patched, which adds confidence in security maintenance. [thebernardlim.com]

Azure App Service aligns better with the project’s priorities. It minimizes cost by eliminating server management and right-sizing resources to the app’s light usage. It also provides easy scalability and high availability without extra engineering, which is ideal for a small app that might need to scale later. The development and deployment experience is simplified, allowing future improvements (like a CI/CD pipeline) to be integrated smoothly. In short, App Service delivers the required functionality and security with far less overhead and cost than a self-managed VM, which makes it the ideal choice for this CMS project.

### Assess app changes that would change your decision.

*Detail how the app and any other needs would have to change for you to change your decision in the last section.* 

Only if the app’s requirements change substantially would a VM make sense. For example, if the application evolved to require very specialized software, custom server configurations, or legacy OS support that App Service doesn’t support, a VM might be warranted. Similarly, if the workload became extremely resource-intensive or needed a specific compute type, App Service’s fixed tiers could become a limitation. In such cases – or if full control over the environment and hardware became a priority – a VM could be considered. Absent those scenarios, the fully managed Azure App Service is the superior choice for the current project’s needs