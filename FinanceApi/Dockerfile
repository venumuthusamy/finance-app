# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copy csproj and restore
COPY FinanceApi/FinanceApi/FinanceApi.csproj ./FinanceApi/
RUN dotnet restore FinanceApi/FinanceApi.csproj

# Copy everything and publish
COPY FinanceApi/FinanceApi ./FinanceApi/
RUN dotnet publish FinanceApi/FinanceApi.csproj -c Release -o /app/out

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/out ./

# Use Render’s PORT env var
ENV ASPNETCORE_URLS=http://+:${PORT}

# Run the app
ENTRYPOINT ["dotnet", "FinanceApi.dll"]
