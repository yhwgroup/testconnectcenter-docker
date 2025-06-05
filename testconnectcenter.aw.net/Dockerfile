# Stage 1: Build the application
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copy the project files and restore dependencies
COPY *.csproj ./
RUN dotnet restore

# Copy the rest of the application files and build
COPY . .
WORKDIR /app/testconnectcenter.aw.net
RUN dotnet publish -c Release -o out

# Stage 2: Create the runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app
COPY --from=build /app/testconnectcenter.aw.net/out .

# Expose the port (e.g., 5011 as per launchSettings.json, or standard HTTP/HTTPS)
EXPOSE 5011

# Set the entry point for the application
ENTRYPOINT ["dotnet", "testconnectcenter.aw.net.dll"]