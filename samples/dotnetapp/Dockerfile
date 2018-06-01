FROM microsoft/dotnet:2.1-sdk-alpine AS build

RUN apk update && apk add --no-cache git openssh

WORKDIR /home

RUN git clone https://github.com/dotnet/dotnet-docker.git

WORKDIR /home/dotnet-docker/samples/dotnetapp

# copy csproj and restore as distinct layers
RUN dotnet restore

# copy everything else and build app
WORKDIR /home/dotnet-docker/samples/dotnetapp/dotnetapp
RUN dotnet build


FROM build AS testrunner
WORKDIR /home/dotnet-docker/samples/dotnetapp/tests
ENTRYPOINT ["dotnet", "test", "--logger:trx"]


FROM build AS test
WORKDIR /home/dotnet-docker/samples/dotnetapp/tests
RUN dotnet test


FROM build AS publish
WORKDIR /home/dotnet-docker/samples/dotnetapp/dotnetapp
RUN dotnet publish -c Release -o out

WORKDIR /home/dotnet-docker/samples/dotnetapp/dotnetapp
ENTRYPOINT ["dotnet", "run"]
