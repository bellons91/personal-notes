---
tags: docker
---

# Dockerfile

A Dockerfile is a script that contains a series of instructions that are used to build a [[Docker]] image.

Dockerfiles typically include the following information:

- The **base or parent image** we use to create the new image
- Commands to update the base OS and install other software
- Build artifacts to include, such as a developed application
- Services to expose, such a storage and network configuration
- **Command to run** when the container is launched

Here's an example of a Dockerfile to build a .NET application:

```dockerfile
# Use the .NET 6 runtime as a base image
FROM mcr.microsoft.com/dotnet/runtime:6.0

# Set the working directory to /app
WORKDIR /app

# Copy the contents of the published app to the container's /app directory
COPY bin/Release/net6.0/publish/ .

# Expose port 80 to the outside world
EXPOSE 80

# Set the command to run when the container starts
CMD ["dotnet", "MyApp.dll"]
```

In particular:

`FROM mcr.microsoft.com/dotnet/runtime:6.0`: this command sets the base image to the .NET 6 runtime, which is needed to run .NET 6 apps.

`WORKDIR /app`: it sets the working directory **of the container structure** to `/app`. This is where app files will be copied.

`COPY bin/Release/net6.0/publish/ .`: this command copies the content within the `bin/Release/net6.0/publish` folder to the current directory (`.`, which is now set to `/app`).

`EXPOSE 80`: it opens the port 80 to the external world. When you run a container using this image, you have to ensure that you are accessing this _internal_ port.

`CMD ["dotnet", "MyApp.dll"]`: this is the command to run when the container starts. In this case, we are running the `dotnet` command with the name of the app's [[DLL]].

Read more [here](https://docs.docker.com/engine/reference/builder/).
