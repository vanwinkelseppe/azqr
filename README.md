[![build](https://github.com/Azure/azqr/actions/workflows/build.yaml/badge.svg)](https://github.com/Azure/azqr/actions/workflows/build.yaml)
[![CodeQL](https://github.com/Azure/azqr/actions/workflows/codeql.yml/badge.svg)](https://github.com/Azure/azqr/actions/workflows/codeql.yml)
[![codecov](https://codecov.io/gh/Azure/azqr/branch/main/graph/badge.svg?token=VReik9rs3l)](https://codecov.io/gh/Azure/azqr)
[![Average time to resolve an issue](http://isitmaintained.com/badge/resolution/Azure/azqr.svg)](http://isitmaintained.com/project/Azure/azqr "Average time to resolve an issue")
[![Percentage of issues still open](http://isitmaintained.com/badge/open/Azure/azqr.svg)](http://isitmaintained.com/project/Azure/azqr "Percentage of issues still open")

# Azure Quick Review

[![Open in vscode.dev](https://img.shields.io/badge/Open%20in-vscode.dev-blue)](https://vscode.dev/github/Azure/azqr)

**Azure Quick Review (azqr)** is a command-line interface (CLI) tool specifically designed to analyze Azure resources and identify whether they comply with Azure's best practices and recommendations. Its primary purpose is to provide users with a detailed overview of their Azure resources, enabling them to easily identify any non-compliant configurations or potential areas for improvement.

## Scan Results

The output generated by **Azure Quick Review (azqr)** is presented in the form of an Excel file, which consists of several sheets including **Overview**, **Recommendations**, **Services**, **Defender**, **Advisor** and **Costs**. Additionally, when running the tool on a Windows system, it also generates a Power BI Desktop Template for further analysis and visualization of the Azure resource data.

The **Overview** sheet provides a summary of the Azure resources scanned by the tool, including the following information:

* **SubscriptionID**: This is the unique identifier for the Azure subscription under which the resource is deployed.
* **ResourceGroup**: The resource group where the resource is deployed.
* **Location**: The geographical region where the resource is deployed.
* **Type**: The specific type or category of the Azure resource.
* **Name**: The name assigned to the resource, providing a human-readable identifier for easy reference and management.
* **SKU**: The SKU represents the specific variant or configuration of the Azure resource. It defines the characteristics and capabilities of the resource.
* **SLA**: The Service Level Agreement (SLA) represents the agreed-upon performance and availability guarantees for the Azure service based on its current configuration.
* **AZ**: A Boolean value indicating whether the service is "Availability Zone aware." Availability Zones are physically separate datacenters within an Azure region, providing increased resiliency and fault tolerance for critical services.
* **PVT**: A Boolean value indicating whether the service has a private IP address. Private IP addresses are used for internal communication within Azure Virtual Networks.
* **DS**: A Boolean value indicating whether diagnostic settings are enabled for the service. Diagnostic settings allow you to collect logs, metrics, and other monitoring data for Azure resources.
* **CAF**: A Boolean value indicating whether the service is compliant with the [Cloud Adoption Framework](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/resource-abbreviations) (CAF) naming convention. The CAF provides best practices and guidance for organizations adopting Azure.

> By default, Azure Quick Review (azqr) masks the Subscription Ids in the spreadsheet, ensuring that they are not directly visible in the output. This helps protect sensitive information and maintain data privacy and security. To view the Subscription Ids, you can use the `--mask=false` flag when running the tool.

To learn more about the **Recommendations**, **Services**, **Defender**, **Advisor** and **Costs** sheets, check the [Scan Results](docs/scan_results/README.md) documentation.

## Azure Quick Review Rules

To learn more about the rules used by **Azure Quick Review (azqr)** for generating recommendations, you can refer to the documentation available [here](docs/rules/README.md).

## Supported Azure Services

**Azure Quick Review (azqr)** currently supports the following Azure services:

* Azure API Management
* Azure App Configuration
* Azure App Services
* Azure Application Gateway
* Azure Application Insights
* Azure Cache for Redis
* Azure Cognitive Services Account
* Azure Container Apps
* Azure Container Instances
* Azure Container Registry
* Azure Cosmos DB
* Azure Data Explorer
* Azure Data Factory
* Azure Database for MariaDB
* Azure Database for MySQL Flexible Server
* Azure Database for MySQL Single Server
* Azure Database for PostgreSQL Flexible Server
* Azure Database for PostgreSQL Single Server
* Azure Event Grid
* Azure Event Hub
* Azure Firewall
* Azure Front Door
* Azure Functions
* Azure Key Vault
* Azure Kubernetes Service
* Azure Load Balancer
* Azure Service Bus
* Azure SignalR Service
* Azure SQL Database
* Azure Storage Account
* Azure Virtual Machine
* Azure Virtual Network
* Azure Virtual WAN
* Azure Web PubSub

## Usage

### Install on Linux or Azure Cloud Shell

```bash
latest_azqr=$(curl -sL https://api.github.com/repos/Azure/azqr/releases/latest | jq -r ".tag_name" | cut -c1-)
wget https://github.com/Azure/azqr/releases/download/$latest_azqr/azqr-ubuntu-latest-amd64 -O azqr
chmod +x azqr
```

### Install on Mac

Download the latest release from [here](https://github.com/Azure/azqr/releases).

### Install on Windows

```console
winget install azqr
```

### Authentication

**Azure Quick Review (azqr)** supports the following authentication methods:

* Azure CLI
* Service Principal. You'll need to set the following environment variables:
  * AZURE_CLIENT_ID
  * AZURE_CLIENT_SECRET
  * AZURE_TENANT_ID

### Authorization

**Azure Quick Review (azqr)** requires the following permissions:

* Subscription Reader

### Running the Scan

To scan all resource groups in all subscription run:

```bash
./azqr scan
```

To scan all resource groups in a specific subscription run:

```bash
./azqr scan -s <subscription_id>
```

To scan a specific resource group in a specific subscription run:

```bash
./azqr scan -s <subscription_id> -g <resource_group_name>
```

For information on available commands and help run:

```bash
./azqr -h
```

## Troubleshooting

If you encounter any issue while using **Azure Quick Review (azqr)**, please set the `AZURE_SDK_GO_LOGGING` environment variable to `all`, run the tool with the `--debug` flag and then share the console output with us by filing a new [issue](https://github.com/Azure/azqr/issues).


## Support

This project uses GitHub Issues to track bugs and feature requests.
Before logging an issue please check our [troubleshooting](#troubleshooting) guide.

Please search the existing issues before filing new issues to avoid duplicates.

- For new issues, file your bug or feature request as a new [issue](https://github.com/Azure/azqr/issues).
- For help, discussion, and support questions about using this project, join or start a [discussion](https://github.com/Azure/azqr/discussions).

Support for this project / product is limited to the resources listed above.

## Contributors

Thanks to everyone who has contributed!

<a href="https://github.com/Azure/azqr/graphs/contributors">
  <img src="https://contributors-img.web.app/image?repo=Azure/azqr" />
</a>

## Code of Conduct

This project has adopted the [Microsoft Open Source Code of Conduct](CODE_OF_CONDUCT.md)

## Trademark Notice

> **Trademarks** This project may contain trademarks or logos for projects, products, or services. Authorized use of Microsoft trademarks or logos is subject to and must follow Microsoft’s Trademark & Brand Guidelines. Use of Microsoft trademarks or logos in modified versions of this project must not cause confusion or imply Microsoft sponsorship. Any use of third-party trademarks or logos are subject to those third-party’s policies.
