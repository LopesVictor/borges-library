FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build-env
WORKDIR /api/BorgesLibraryCore/

# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
WORKDIR /api
COPY --from=build-env /api/BorgesLibraryCore/out/ .
ENTRYPOINT ["dotnet", "BorgesLibraryCore.dll"]