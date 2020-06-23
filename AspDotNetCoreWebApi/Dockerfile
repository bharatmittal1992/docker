# Get base sdk Image from Microsoft
FROM mcr.microsoft.com/dotnet/core/sdk:2.2 as build-env
WORKDIR /app

#Copy the CSPROJ file and restore any dependencies (via NUGET)

COPY *.csproj ./
RUN dotnet restore

# Copy the project files and build our released
COPY . ./
RUN dotnet publish -c Release -o out

# Generate runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet","AspDotNetCoreWebApi.dll"]