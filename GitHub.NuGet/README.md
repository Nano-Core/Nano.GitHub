# Nano.GitHub.NuGet
Nano requires a private NuGet server, to publish application dependencies for servieces and libraries.  

***

### Setup
To setup private NuGet packages on GitHub, follow the documentation here:  
* Nano: GitHub NuGet setup: https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-nuget-registry

The environmental variables needed for Nano are the following:
* NUGET_HOST: https://nuget.pkg.github.com/{{org-name}}/index.json
* NUGET_APIKEY: GitHub PAT Token
* NUGET_USERNAME:  GitHub Username (for PAT Token)
* NUGET_PASSWORD: secrets.GITHUB_TOKEN (build-in secret)

***
