# Stage 1: Build the application
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env
WORKDIR /app

# Copy only the project file and restore dependencies
COPY MediaService/*.csproj ./MediaService/
RUN dotnet restore ./MediaService/MediaService.csproj

# Copy the entire project and build
COPY . ./
RUN dotnet publish -c Release -o out

# Stage 2: Create the runtime image
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app

# Copy the published output from the build stage
COPY --from=build-env /app/out .

# Set the entry point for the application
ENTRYPOINT ["dotnet", "MediaService.dll"]
