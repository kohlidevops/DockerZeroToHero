# Multi Stage Docker Build

The main purpose of choosing a golang based applciation to demostrate this example is golang is a statically-typed programming language that does not require a runtime in the traditional sense. Unlike dynamically-typed languages like Python, Ruby, and JavaScript, which rely on a runtime environment to execute their code, Go compiles directly to machine code, which can then be executed directly by the operating system.

So the real advantage of multi stage docker build and distro less images can be understand with a drastic decrease in the Image size.

### First clone this below repository

```
https://github.com/kohlidevops/DockerZeroToHero.git
```

Move to below path

```
/home/ubuntu/DockerZeroToHero/examples/golang-multi-stage-docker-build
```

### Firstly run the BASE Image Dockerfile and check the docker image size

```
###########################################
# BASE IMAGE
###########################################
FROM ubuntu AS build
RUN apt-get update && apt-get install -y golang-go
ENV GO111MODULE=off
COPY . .
RUN CGO_ENABLED=0 go build -o /app .

############################################
# HERE STARTS THE MAGIC OF MULTI STAGE BUILD
############################################
#FROM scratch
# Copy the compiled binary from the build stage
#COPY --from=build /app /app
# Set the entrypoint for the container to run the binary
#ENTRYPOINT ["/app"]
```

### Secondly run the Multi stage Dockerfile and check the docker image size

```
###########################################
# BASE IMAGE
###########################################
FROM ubuntu AS build
RUN apt-get update && apt-get install -y golang-go
ENV GO111MODULE=off
COPY . .
RUN CGO_ENABLED=0 go build -o /app .

############################################
# HERE STARTS THE MAGIC OF MULTI STAGE BUILD
############################################
FROM scratch
# Copy the compiled binary from the build stage
COPY --from=build /app /app
# Set the entrypoint for the container to run the binary
ENTRYPOINT ["/app"]
```

![image](https://github.com/kohlidevops/DockerZeroToHero/assets/100069489/2aef7964-b080-4a82-8d3b-549c40ae9aef)

Seems, distro image is 800 times less than base image
