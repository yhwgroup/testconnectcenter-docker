# Stage 1: Build the application
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy the entire application source code into the container
# Since the GitHub Actions context is './testconnectcenter.aw.net',
# everything from that directory will be copied to /src in the container.
COPY . .

# Change the working directory to the project directory
# This ensures that dotnet commands are run from where the .csproj file is located.
WORKDIR /src/testconnectcenter.aw.net

# Restore project dependencies
RUN dotnet restore

# Publish the application for release
RUN dotnet publish -c Release -o out

# Stage 2: Create the runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app

# Copy the published output from the build stage to the final runtime image
COPY --from=build /src/testconnectcenter.aw.net/out .

# Expose the application's port
EXPOSE 5011

# Define the entry point for the application
ENTRYPOINT ["dotnet", "testconnectcenter.aw.net.dll"]