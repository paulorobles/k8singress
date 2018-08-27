FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY myFirstContainerapp.csproj myFirstContainerapp/
RUN dotnet restore myFirstContainerapp/myFirstContainerapp.csproj
COPY . .
WORKDIR /src/myFirstContainerapp
RUN dotnet build myFirstContainerapp.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish myFirstContainerapp.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "myFirstContainerapp.dll"]

