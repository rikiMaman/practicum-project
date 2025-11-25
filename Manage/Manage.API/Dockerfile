# ============================
#   BUILD STAGE
# ============================
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy entire solution (Manage/) into container
COPY .. .

# Restore
WORKDIR /src/Manage.API
RUN dotnet restore Manage.API.csproj

# Publish
RUN dotnet publish Manage.API.csproj -c Release -o /app/publish

# ============================
#   RUNTIME STAGE
# ============================
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app
COPY --from=build /app/publish .

EXPOSE 8080
ENV ASPNETCORE_URLS=http://+:8080

ENTRYPOINT ["dotnet", "Manage.API.dll"]
