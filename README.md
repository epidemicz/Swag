# Static Web App
![](/img/icon.png)

## Overview
This is a simple containerized web application that can be used to quickly serve static files from a directory (with directory browsing enabled).

I mainly use this to run godot games exported to html.

You can find the docker image on dockerhub [here](https://hub.docker.com/repository/docker/epidemicz/staticwebapp/general)

```
docker pull epidemicz/staticwebapp:latest
```

## Container Variables
 - SERVER_PORT: Default: 8085. The port web server will be operating on.
 - SERVE_DIRECTORY: Default: Current working directory. The path on the host machine to serve. 
   - If not using docker compose, map the directory on your host machine to `/app/wwwroot`.

## Usage

### Docker compose
See the `.env` file to customize the environment variables

```
docker compose --project-directory docker up
```

### Docker run temporary container
To serve the directory `c:\dump` on port 8088:
```
docker run --rm -ti -p 8088:8088 -e SERVER_PORT=8088 -v c:\dump:/app/wwwroot epidemicz/staticwebapp
```

### Dotnet run
To serve `c:\dump`:
```
dotnet run path=c:\dump
```

### As a stand-alone binary
To serve `c:\dump`:
```
StaticWebApp.exe path=c:\dump
```

## Building the container
From the root directory
```
docker build -f docker/Dockerfile -t epidemicz/staticwebapp:latest .
```
