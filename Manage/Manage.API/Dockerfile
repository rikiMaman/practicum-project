# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

COPY . .

# Restore using correct path
WORKDIR /src/Manage/Manage.API
RUN dotnet restore Manage.API.csproj

# Publish
RUN dotnet publish Manage.API.csproj -c Release -o /app/publish

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app
COPY --from=build /app/publish .

ENTRYPOINT ["dotnet", "Manage.API.dll"]
