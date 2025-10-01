
<img width="800" height="600" alt="quickSetupGuide" src="https://github.com/user-attachments/assets/6f7deb3f-0b4b-4522-9e83-c8decb267b5f" />

---

🚀 [Azure Marketplace Offer](https://azuremarketplace.microsoft.com/en-us/marketplace/apps?search=frametype&page=1)

---

## Azure Firewall deployed w/ Basic SKU

### Purpose

1. **Cost-Effective Security:**
   - **Affordable Protection:** The Basic SKU provides essential firewall capabilities at a lower cost, making it suitable for small to medium-sized businesses that need to secure their Azure resources without a significant financial investment.

2. **Network Traffic Control:**
   - **Application and Network Rules:** You can define rules to control both application-level (FQDN filtering) and network-level (IP, port, protocol) traffic. This helps ensure that only authorized traffic is allowed, enhancing your network security.

3. **Built-in High Availability:**
   - **Resilience:** The Basic SKU includes built-in high availability, ensuring that your firewall remains operational even in the event of a failure, without requiring additional configurations.

4. **Threat Intelligence:**
   - **Alert Mode:** The Basic SKU supports threat intelligence in alert mode, which helps detect and alert you to potential threats based on Microsoft’s threat intelligence feed. This adds an extra layer of security by identifying suspicious activities.

5. **Simplified Management:**
   - **Centralized Control:** Azure Firewall provides a centralized way to manage and enforce your network security policies across your Azure environment, simplifying the management of security rules and configurations.

6. **Scalability:**
   - **Adaptability:** While the Basic SKU is designed for environments with throughput needs of up to 250 Mbps, it can still scale to meet the demands of growing businesses. You can easily upgrade to higher SKUs if your requirements increase.

7. **Integration with Azure Services:**
   - **Seamless Integration:** Azure Firewall integrates seamlessly with other Azure services, such as Azure Monitor for logging and diagnostics, and Azure Policy for compliance management. This ensures a cohesive security strategy across your Azure environment.

Deploying an Azure Firewall with a Basic SKU helps you achieve a balanced approach to security, cost, and manageability, making it an excellent choice for many organizations.

### Scope

Azure Firewall deployed with a Basic SKU is designed for small to medium-sized businesses with throughput needs of up to 250 Mbps. It does not support advanced features like TLS inspection and IDPS available in the higher SKUs.

## Overview

### Architecture Overview

#### Network Diagram

<img width="800" height="600" alt="AzureFirewallDeployment" src="https://github.com/user-attachments/assets/f4ba7284-675c-456d-ba9f-34ebddf65950" />

### Components Description

The following Azure artifacts are delivered via IaC (infrastructure as code) utilizing Bicep templates and Powershell scripting.

- **Resource Group:** A unique resource group is created for the deployment of the firewall artifact and related resources.
- **Virtual network**
- **IP Group**
- **Firewall Policy**
- **Firewall Public IP address**
- **Management Public IP address**
- **Firewall**
- **Route table**
- **Log Analytics workspace**

### Azure Firewall Basic SKU Features

Azure Firewall deployed with a Basic SKU offers several features that make it a robust choice for network security, especially for small and medium-sized businesses. You can leverage the following features:

- **Built-in High Availability:** No additional load balancers are required, and high availability is built into the service.
- **Availability Zones:** You can deploy Azure Firewall across multiple Availability Zones for increased availability.
- **Application FQDN Filtering Rules:** This allows you to limit outbound HTTP/S traffic or Azure SQL traffic to specified fully qualified domain names (FQDNs), including wildcards.
- **Network Traffic Filtering Rules:** Centrally create allow or deny network filtering rules by source and destination IP address, port, and protocol.
- **FQDN Tags:** Simplifies the process of allowing well-known Azure service network traffic through your firewall.
- **Service Tags:** Represents groups of IP address prefixes to minimize complexity for security rule creation.
- **Threat Intelligence in Alert Mode:** Provides threat intelligence-based filtering to alert you about potential threats.
- **Outbound SNAT Support:** Supports Source Network Address Translation (SNAT) for outbound traffic.
- **Inbound DNAT Support:** Supports Destination Network Address Translation (DNAT) for inbound traffic.
- **Multiple Public IP Addresses:** Supports multiple public IP addresses for better scalability and management.
- **Azure Monitor Logging:** Integrates with Azure Monitor for logging and monitoring.

## Azure Pricing

To calculate the total monthly recurring cost for a single Azure Firewall deployed with a single policy, each with a Basic SKU, you need to consider the costs for all of the associated resources.

- **Virtual Network:** Virtual Networks in Azure are free of charge. Every subscription can create up to 50 Virtual Networks across all regions. VNET Peering links two virtual networks – either in the same region, or in different regions - and enables you to route traffic between them using private IP addresses (carry a nominal charge). Inbound and outbound traffic is charged at both ends of the peered networks.
- **Public IP Addresses**
- **Azure Firewall – Basic SKU:** $0.395/hour * 24 hours/day * 30 days/month = $284.40 approximate monthly deployment cost.
- **Data processing cost:** $0.065 per GB processed.
- **Azure Firewall Policy – Basic SKU:** The cost for an Azure Policy is $100 per policy per region per month. However, the first Azure Firewall policy associated with a single firewall in a single region incurs no monthly charge. For this deployment, as configured, there will not be any additional costs incurred for the policy itself since it is the only one associated with the firewall in a single region.
- **Log Analytics Workspace**

For more information on Azure pricing, please refer to the Microsoft website: [Azure Pricing](https://azure.microsoft.com/en-us/pricing/)

## Prerequisites

The following prerequisites are required for a successful deployment of the Azure firewall.

- **Azure Subscription:** A valid Azure subscription is required for deployment.
- **Required Permissions:** A user account with the RBAC role of ‘contributor’ or 'owner' on the target Azure subscription is necessary for deployment of the Azure firewall and associated resources from Azure Marketplace.

## Deployment Steps

1. **Resource Group Creation**
2. **Virtual Network and Subnet Configuration**
3. **Public IP Address Configuration**
4. **Azure Firewall Deployment**
5. **Firewall Policy Configuration**

## Bicep Template Details

- **Parameters**
- **Variables**
- **Resources**
  - **NAME**
  - **TYPE**
  - **afw-basic-infra-westus2-01:** Firewall
  - **fwp-afw-infra-westus2-01:** Firewall Policy
  - **ipg-afw-infra-westus2-01:** IP Group
  - **law-afw-infra-westus2-01:** Log Analytics workspace
  - **pip-azFw-westus2-mgt-01:** Public IP address
  - **pip-azFw-westus2-pub-01:** Public IP address
  - **rt-afw-infra-westus2-01:** Route table
  - **vn-afw-infra-westus2-10.120:** Virtual network
- **Outputs**

## Security Considerations

- **Network Security Groups (NSGs)**
- **Application and Network Rule Collections**
- **Logging and Monitoring**

## Azure Governance

Governance is one aspect of Azure Management. This project uses Azure Policy as part of the governance strategy to govern, configure, secure, protect, and monitor Azure resources and workloads. Using Azure Policy to enforce resource tagging and regional restrictions meets some of the challenges of managing Azure resources.

When deploying an Azure Firewall with a Basic SKU, it's important to follow best practices for governance compliance to ensure security, reliability, and cost optimization. Here are some key recommendations:

- **Use Azure Policy:** Implement Azure Policy to enforce compliance with organizational standards. Policies can help ensure that configurations are consistent and meet security requirements. For example, you can create policies to enable Threat Intelligence, enforce DNS Proxy, and restrict deployments to multiple availability zones.
- **Follow the Azure Well-Architected Framework:** This framework provides architectural recommendations mapped to key design principles such as reliability, security, cost optimization, and operational excellence. It includes a design checklist to help you build a resilient and compliant architecture.
- **Monitor and Optimize:** Regularly review and optimize your firewall rules and configurations. Use Azure Firewall Policy Analytics to tune and optimize firewall rules effectively.
- **Enable Key Features:** Ensure that essential features like Threat Intelligence, DNS Proxy, and TLS inspection are enabled to enhance security and compliance.
- **Stay Updated:** Keep your Azure Firewall deployment updated with the latest features and best practices. Regularly review the list of known issues and platform limitations to mitigate potential risks.

By following these best practices, you can ensure that your Azure Firewall deployment is secure, compliant, and optimized for your organization's needs.

## Naming Conventions

Naming conventions and standards take on special importance since there is no way to rename resources in Azure once they are deployed. The naming conventions follow the best practices of the Cloud Adoption Framework.

## Identity and RBAC Roles

This project supports the use of Microsoft Entra ID for identity management and RBAC roles can be assigned to govern access to resources. RBAC roles allow the granting of only the required access needed to perform the job.

For more information on best practices, please refer to the Microsoft website: [RBAC Best Practices](https://learn.microsoft.com/en-us/azure/role-based-access-control/best-practices)

## Testing and Validation

- **Connectivity Tests**
- **Rule Verification**
- **Performance Monitoring**

## Troubleshooting

- **Common Issues**
- **Diagnostic Tools**
- **Support Resources**

## Conclusion

- **Summary**
- **Next Steps**

## Appendices

- **Bicep Template Code**
- **References**

For more information on Azure Firewall Basic SKU features, please refer to the Microsoft website: [Azure Firewall Basic Features](https://learn.microsoft.com/en-us/azure/firewall/basic-features)
