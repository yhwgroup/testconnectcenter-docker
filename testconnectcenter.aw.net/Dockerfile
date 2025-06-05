FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app
COPY *.csproj ./
RUN dotnet restore
COPY . .
WORKDIR /app/testconnectcenter.aw.net
RUN dotnet publish -c Release -o out
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS final
WORKDIR /app
COPY --from=build /app/testconnectcenter.aw.net/out .

EXPOSE 5011

# Set the entry point for the application
ENTRYPOINT ["dotnet", "testconnectcenter.aw.net.dll"]