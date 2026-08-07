# Nano.GitHub.NuGet

> _Private Nuget registry setup and configuration._

***

## Table of Contents
* **[Summary](#summary)**
* **[Configuration](#configuration)**

## Summary
A private NuGet registry is a core requirement for maintaining a controlled, scalable, and efficient codebase.

Nano relies on a private NuGet server to distribute internal packages across services and libraries, ensuring consistent dependency management and secure access to proprietary 
components.

## Configuration
Private NuGet package hosting with GitHub Packages works out of the box when using GitHub Actions and the built-in `GITHUB_TOKEN`, which already provides the required authentication 
for publishing and consuming packages within your organization. For additional context on how GitHub Packages NuGet authentication works and the supported scenarios, see the 
**[official documentation](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-nuget-registry)**.

> ⚠️ Be aware: consuming NuGet packages across repositories requires explicit access permissions. 

The package repository must grant access to the consuming workflow repository in order for restores to succeed within the organization. Navigate to the repository of the NuGet packages, 
and continue to packages. Click package settings and add add the repositiories to grant access, and allow to pull the NuGet packages. Unfortunately, this can't be automated as the 
`GITHUB_TOKEN` only has permissions within it's own repository, but it's a one-time setup.

For local development in Visual Studio, add a new NuGet package source using the GitHub NuGet feed URL:

`https://nuget.pkg.github.com/{org-name}/index.json`

When prompted for credentials, enter your GitHub username and use a Personal Access Token (PAT) as the password. The PAT must have at least the `read:packages` permission to authenticate 
and restore packages from private GitHub repositories.

> ⚠️ If Visual Studio continuously prompts for credentials, make sure the username does _not_ include the GitHub NuGet host: `https://nuget.pkg.github.com/{org-name}/` as a prefix.

> ⚠️ If the GitHub NuGet password prompt does not appear and you only see "An error occurred" when listing packages, Visual Studio may be using cached or conflicting credentials. Check 
Windows Credential Manager, remove any conflicting NuGet/GitHub entries, close Visual Studio, delete the .vs folder, and refresh the package list. The login prompt should then appear.