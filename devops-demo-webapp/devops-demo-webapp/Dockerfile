FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY devops-demo-webapp/devops-demo-webapp.csproj devops-demo-webapp/
RUN dotnet restore devops-demo-webapp/devops-demo-webapp.csproj
COPY . .
WORKDIR /src/devops-demo-webapp
RUN dotnet build devops-demo-webapp.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish devops-demo-webapp.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "devops-demo-webapp.dll"]
