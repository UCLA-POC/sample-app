FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY sample-app/sample-app.csproj sample-app/
RUN dotnet restore sample-app/sample-app.csproj
COPY . .
WORKDIR /src/sample-app
RUN dotnet build sample-app.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish sample-app.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "sample-app.dll"]
