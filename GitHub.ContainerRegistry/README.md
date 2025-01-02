# Nano.GitHub.ContainerRegistry
Nano requires a container registry server, to publish cotaniner images for applications.  

***

### Configuration
To setup private container registry on GitHub, follow the documentation here:  
* https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry

The environmental variables needed for Nano are the following:
* CONTAINER_REGISTRY_HOST: 'ghcr.io/${{ github.repository_owner }}'
* CONTAINER_REGISTRY_USERNAME: GitHub Username (for PAT Token)
* CONTAINER_REGISTRY_PASSWORD: GitHub PAT Token
* CONTAINER_REGISTRY_SOURCE_LABEL: https://github.com/{{org-name}}/{{image-name}}

**NOTE:** It's also possible to use ```{{ Github.actor}}``` as username and ```{{ Github.GITHUB_TOKEN }}``` as Password, but it the repository must be manually linked with the package on GitHub.  

***
