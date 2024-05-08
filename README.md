[![build](https://github.com/Azure/azqr/actions/workflows/build.yaml/badge.svg)](https://github.com/Azure/azqr/actions/workflows/build.yaml)
[![CodeQL](https://github.com/Azure/azqr/actions/workflows/codeql.yml/badge.svg)](https://github.com/Azure/azqr/actions/workflows/codeql.yml)
[![Github All Releases](https://img.shields.io/github/downloads/Azure/azqr/total.svg)]()
[![codecov](https://codecov.io/gh/Azure/azqr/branch/main/graph/badge.svg?token=VReik9rs3l)](https://codecov.io/gh/Azure/azqr)
[![Average time to resolve an issue](http://isitmaintained.com/badge/resolution/Azure/azqr.svg)](http://isitmaintained.com/project/Azure/azqr "Average time to resolve an issue")
[![Percentage of issues still open](http://isitmaintained.com/badge/open/Azure/azqr.svg)](http://isitmaintained.com/project/Azure/azqr "Percentage of issues still open")

# Azure Quick Review

[![Open in vscode.dev](https://img.shields.io/badge/Open%20in-vscode.dev-blue)](https://vscode.dev/github/Azure/azqr)

**Azure Quick Review (azqr)** is a command-line interface (CLI) tool specifically designed to analyze Azure resources and identify whether they comply with Azure's best practices and recommendations. Its primary purpose is to provide users with a detailed overview of their Azure resources, enabling them to easily identify any non-compliant configurations or potential areas for improvement.

## Scan Results

The output generated by **Azure Quick Review (azqr)** is presented by default in four `csv` files:

* **azqr-YYYY-MM-DD-HH-MM-SS.services.csv:** This file contains the details of the Azure services scanned by the tool, including:
    * Subscription: The unique identifier for the Azure subscription under which the resource is deployed.
    * Resource Group: The resource group where the resource is deployed.
    * Location: The geographical region where the resource is deployed.
    * Type: The specific type or category of the Azure resource.
    * Service Name: The name assigned to the service, providing a human-readable identifier for easy reference and management.
    * Compliant: A Boolean value indicating whether the service is compliant with Azure's best practices and recommendations.
    * Impact: The potential impact of non-compliance on the service.
    * Category: The category or type of recommendation.
    * Recommendation: The specific recommendation or best practice.
    * Result: The result or value resulting from the evaluation of the recommendation (i.e. Service SLA or SKU). 
    * Learn: A link to additional information or documentation related to the recommendation.
* **azqr-YYYY-MM-DD-HH-MM-SS.defender.csv:**
    * Subscription: The unique identifier for the Azure subscription under which the resource is deployed.
    * Name: Microsoft Defender for Cloud plan name.
    * Tier: The tier of the plan.
    * Deprecated: a Boolean value indicating whether the plan is deprecated.
* **azqr-YYYY-MM-DD-HH-MM-SS.advisor.csv:**
    * Subscription: The unique identifier for the Azure subscription under which the resource is deployed.
    * Name: The name of the resource identified by Advisor.
    * Type: The resource type of the resource identified by Advisor.
    * Category: The category of the recommendation.
    * Description: The description of the recommendation.
    * PotentialBenefits: The potential benefits of the recommendation.
    * Risk: Risk related to the recommendation.
    * LearnMoreLink: A link to additional information or documentation related to the recommendation.
* **azqr-YYYY-MM-DD-HH-MM-SS.costs.csv:**
    * From: the start date of the cost analysis period.
    * To: the end date of the cost analysis period.
    * Subscription: The unique identifier for the Azure subscription under which the resource is deployed.
    * ServiceName: The type of the Azure service for which the cost is calculated.
    * Value: The cost value associated with the service.
    * Currency: The currency in which the cost is calculated.

> By default, Azure Quick Review (azqr) masks the Subscription Ids in the spreadsheet, ensuring that they are not directly visible in the output. This helps protect sensitive information and maintain data privacy and security. To view the Subscription Ids, you can use the `--mask=false` flag when running the tool.

> Azure Quick Review can also generate an Excel file with the same information as the CSV files. To generate the Excel file, you can use the `--excel` (or `-x`) flag when running the tool.

> A Power BI template is also available to help you visualize the results generated by Azure Quick Review. You can create the template running Azure Quick Review with the `pbi` command.

## Azure Quick Review Recommendations

To learn more about the recommendations used by **Azure Quick Review (azqr)**, you can refer to the documentation available [here](https://azure.github.io/azqr/docs/recommendations/).

## Supported Azure Services

**Azure Quick Review (azqr)** currently supports the following Azure services:

* Azure Analysis Service
* Azure API Management
* Azure App Configuration
* Azure App Services
* Azure Application Gateway
* Azure Application Insights
* Azure Cache for Redis
* Azure Cognitive Services Account
* Azure Container Apps Environment
* Azure Container Apps
* Azure Container Instances
* Azure Container Registry
* Azure Cosmos DB
* Azure Databricks
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
* Azure Logic Apps
* Azure Managed Grafana
* Azure Service Bus
* Azure SignalR Service
* Azure SQL Server
* Azure SQL Elastic Pool
* Azure SQL Database
* Azure Storage Account
* Azure Synapse Analytics Workspace
* Azure Synapse Spark Pool
* Azure Synapse Dedicated SQL Pool
* Azure Traffic Manager
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

### Install on Windows

Use `winget`:

```console
winget install azqr
```

or download the executable file:

```
$latest_azqr=$(iwr https://api.github.com/repos/Azure/azqr/releases/latest).content | convertfrom-json | Select-Object -ExpandProperty tag_name
iwr https://github.com/Azure/azqr/releases/download/$latest_azqr/azqr-windows-latest-amd64.exe -OutFile azqr.exe
```

### Install on Mac

Download the latest release from [here](https://github.com/Azure/azqr/releases).

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
