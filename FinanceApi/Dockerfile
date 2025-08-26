# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copy csproj and restore
COPY FinanceApi/FinanceApi.csproj ./
RUN dotnet restore FinanceApi.csproj

# Copy all files and publish
COPY FinanceApi/ ./   # copy all project files from FinanceApi folder
RUN dotnet publish FinanceApi.csproj -c Release -o /app/out

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/out ./

# Use Render's PORT env var
ENV ASPNETCORE_URLS=http://+:${PORT}

ENTRYPOINT ["dotnet", "FinanceApi.dll"]
