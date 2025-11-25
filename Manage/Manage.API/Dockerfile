# ============================
#   BUILD STAGE
# ============================
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy full repo into container
COPY . .

# Go to API folder
WORKDIR /src/Manage/Manage.API
RUN dotnet restore Manage.API.csproj

# Publish
RUN dotnet publish Manage.API.csproj -c Release -o /app/publish

# ============================
#   RUNTIME
# ============================
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app

COPY --from=build /app/publish .

ENTRYPOINT ["dotnet", "Manage.API.dll"]
