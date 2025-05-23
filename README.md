# Contact Database Application (.NET MVC)

## Overview
This repository contains a .NET MVC web application for managing contacts. The application is built using ASP.NET Core MVC and can be deployed to Azure using ARM templates.

## Prerequisites
- .NET 8.0 SDK or later
- Visual Studio 2022 or VS Code
- Azure subscription (for deployment)
- GitHub account (for GitHub Actions)

## Local Development Setup
1. Clone the repository
```bash
git clone [repository-url]
```

2. Navigate to the project directory
```bash
cd MyMvcApp-Contact-Database-Application
```

3. Restore dependencies and run the application
```bash
dotnet restore
dotnet run
```

The application will be available at `https://localhost:5001` or `http://localhost:5000`

## Solution Structure
- `Controllers/` - MVC Controllers including UserController
- `Models/` - Data models and view models
- `Views/` - Razor views for the UI
- `Infrastructure/` - Infrastructure related code
- `deploy.json` - ARM template for Azure deployment
- `deploy.parameters.json` - Parameters for ARM template

## Deployment
### Azure Deployment using ARM Template

The application can be deployed to Azure using the provided ARM template (`deploy.json`). The template includes:
- App Service Plan
- Web App
- SQL Database (if applicable)

To deploy using Azure CLI:
```bash
az login
az group create --name [resource-group-name] --location [location]
az deployment group create --resource-group [resource-group-name] --template-file deploy.json --parameters @deploy.parameters.json
```

### GitHub Actions Workflow

The repository includes a GitHub Actions workflow for CI/CD. The workflow:
1. Builds the application
2. Runs tests
3. Deploys to Azure using ARM template

To set up GitHub Actions:

1. In your GitHub repository, go to Settings > Secrets and add the following secrets:
   - `AZURE_CREDENTIALS` - Azure Service Principal credentials
   - `RESOURCE_GROUP` - Target Azure Resource Group name
   - `SUBSCRIPTION_ID` - Azure Subscription ID

2. Create a Service Principal:
```bash
az ad sp create-for-rbac --name "myapp-sp" --role contributor --scopes /subscriptions/{subscription-id}/resourceGroups/{resource-group}
```

3. The workflow will automatically trigger on:
   - Push to master branch
   - Pull request to master branch

## Testing
Run the tests using:
```bash
dotnet test MyMvcApp.Tests/MyMvcApp.Tests.csproj
```

## Contributing
1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License
[Add your license information here]
