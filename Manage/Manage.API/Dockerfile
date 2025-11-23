# ============================
#   BUILD STAGE
# ============================
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy project folders from one level above (because Dockerfile is inside Manage.API)
COPY ../Manage.Core/ Manage.Core/
COPY ../Manage.Data/ Manage.Data/
COPY ../Manage.Service/ Manage.Service/

# Copy ONLY this API folder ('.' means current directory)
COPY . Manage.API/

# Restore & Publish
WORKDIR /src/Manage.API
RUN dotnet restore
RUN dotnet publish -c Release -o /app/publish

# ============================
#   RUNTIME STAGE
# ============================
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app

COPY --from=build /app/publish .

EXPOSE 8080
ENV ASPNETCORE_URLS=http://+:8080

ENTRYPOINT ["dotnet", "Manage.API.dll"]
