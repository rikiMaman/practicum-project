# ============================
#   BUILD STAGE
# ============================
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy all project folders (as they exist במבנה שלך)
COPY Manage.Core/ Manage.Core/
COPY Manage.Data/ Manage.Data/
COPY Manage.Service/ Manage.Service/
COPY Manage.API/ Manage.API/

# Restore & Publish
WORKDIR /src/Manage.API
RUN dotnet restore
RUN dotnet publish -c Release -o /app/publish


# ============================
#   RUNTIME STAGE
# ============================
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app

# Copy build result
COPY --from=build /app/publish .

# Default port for Render
EXPOSE 8080
ENV ASPNETCORE_URLS=http://+:8080

# Start the API
ENTRYPOINT ["dotnet", "Manage.API.dll"]