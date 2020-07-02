FROM mcr.microsoft.com/dotnet/core/sdk:2.1 AS build
WORKDIR /api

# Restore packages just from CSPROJ
COPY api.csproj .
RUN dotnet restore

# Copy eveyrthing else in another stage so we can cache above.
COPY . .
RUN dotnet publish -o /publish

FROM mcr.microsoft.com/dotnet/core/aspnet:2.1 AS runtime
WORKDIR /publish
COPY --from=build /publish .
ENTRYPOINT ["dotnet", "api.dll"]