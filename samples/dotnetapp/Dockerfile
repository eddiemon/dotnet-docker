FROM microsoft/dotnet:2.1-sdk-alpine AS prebuild

RUN apk update && apk add --no-cache git openssh

WORKDIR /home

FROM prebuild AS build
RUN git clone https://github.com/eddiemon/dotnet-docker.git

WORKDIR /home/dotnet-docker/samples/dotnetapp/dotnetapp
RUN dotnet build

WORKDIR /home/dotnet-docker/samples/dotnetapp/dotnetapp
ENTRYPOINT ["dotnet", "run"]
