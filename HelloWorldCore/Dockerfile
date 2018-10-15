FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80:80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY HelloWorldCore/HelloWorldCore.csproj HelloWorldCore/
RUN dotnet restore HelloWorldCore/HelloWorldCore.csproj
COPY . .
WORKDIR /src/HelloWorldCore
RUN dotnet build HelloWorldCore.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish HelloWorldCore.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "HelloWorldCore.dll"]
