# Nano.GitHub.RunnerApp

> _An organization-scoped GitHub App authorized to run GitHub Actions workflows._

***

## Table of Contents
* **[Summary](#summary)**
* **[Configuration](#configuration)**
  * **[Create GitHub App](#create-github-app)**
  * **[Generate a Private Key](#generate-a-private-key)**
  * **[Installing the GitHub App](#installing-the-github-app)**
  * **[GitHub Secrets](#github-secrets)**

## Summary
Nano deployments use a GitHub App to securely execute GitHub Actions workflows on Azure-based self-hosted runners.  

This architecture is designed to keep the system private by default. GitHub never directly communicates with Azure infrastructure. Instead, Azure hosts self-hosted runners that 
register outbound to GitHub and pull jobs when workflows are triggered.  

This approach ensures secure, controlled execution of CI/CD pipelines entirely within Azure while maintaining full network isolation from inbound GitHub traffic. The GitHub App is 
scoped at the organization level and is used to authorize and manage workflow execution through these self-hosted runners.  

For enterprise organization structures, the industry standard to create a dedicated GitHub App inside your organization. 

The **[Nano.Azure.Kubernetes.GitHubRunner](https://github.com/Nano-Core/Nano.Azure.Kubernetes/tree/master/Nano.Azure.Kubernetes.GitHubRunner/README.md#nanoazurekubernetesgithubrunner)** 
underlying scaling engine (KEDA) natively supports GitHub App authentication using an App ID, an Installation ID, and a Private Key (.pem file). 

## Configuration
To configure the GitHub App follow the steps below.

### Create GitHub App
Follow these steps to create a GitHub App with the required permissions to run GitHub Actions workflows.

1. Go to Organization Settings ➔ Developer Settings ➔ GitHub Apps ➔ New GitHub App.  
2. Give it a name (e.g., `nano-deployment-agent`) and set the required Homepage URL to anything valid (e.g., your org URL).  
3. Scroll to the Webhooks section at the bottom of the app page and uncheck _Active_ to disable webhooks. 
   KEDA in Azure Container Apps does not require GitHub webhooks because it polls the GitHub API at intervals to check for queued work.  
4. With webhooks disabled, no event subscriptions are needed. Leave the _Subscribe to events_ section empty (this is the default).  
5. Under Permissions ➔ Repository Permissions, grant:  
   - Actions: Read & Write (required for runner queue monitoring and registration).  
   - Metadata: Read-only (default).  
6. Under Permissions ➔ Organization Permissions, grant:  
   - Self-hosted runners: Read & Write.  
7. Under _Where can this GitHub App be installed?_, select _Only on this account_ (default). This restricts the app to your organization and prevents external installations.  
8. Click _Create the app_.  

> ⚠️ The GitHub runner uses the _Default Runner Group_. If it should be available to public repositories, you must enable this manually in Organization Settings ➔ Actions ➔ Runner Groups ➔ Default, then select **Allow public repositories**.

### Generate a Private Key
After creating the GitHub App, generate a private key:

1. Scroll to the _Private keys_ section and click _Generate a private key_.  
2. A `.pem` file will be downloaded. Store it securely, as it is required later for authentication.

### Installing the GitHub App
Next, the app must be installed in your organization so it can access the required repositories and operate on behalf of the app.  

1. Install the App from the left-hand menu on the app details page, selecting the relevant organization and repositories.  
2. Extract the App parameters:  
   - After installation, check the browser URL. The trailing number (e.g., `12345678`) is your _Installation ID_.  
   - Go to _⚙️ App settings_ and copy the _App ID_ from the top of the settings page.  

### GitHub Secrets
Add the following GitHub organization secrets.  

These are required later for deploying **[Nano.Azure.Kubernetes.GitHubRunner](https://github.com/Nano-Core/Nano.Azure.Kubernetes/tree/master/Nano.Azure.Kubernetes.GitHubRunner/README.md#nanoazurekubernetesgithubrunner)**, 
which uses the GitHub App for authentication.  

| Secret                          | Type     | Description                                                                                                           |
| ------------------------------- | -------- | --------------------------------------------------------------------------------------------------------------------- |
| `GITHUBRUNNER_APP_ID`           | secret   | The App ID of the GitHub App. Found under Organization Settings ➔ Developer Settings ➔ GitHub Apps ➔ App Settings.  |
| `GITHUBRUNNER_INSTALLATION_ID`  | secret   | The Installation ID shown in the app’s URL after installation.                                                        |
| `GITHUBRUNNER_PRIVATE_KEY`      | secret   | The private key downloaded as a `.pem` file when generating the GitHub App key.                                       |
