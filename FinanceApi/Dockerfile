# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

COPY FinanceApi/FinanceApi.csproj ./
RUN dotnet restore FinanceApi.csproj

COPY FinanceApi/ ./ 
RUN dotnet publish FinanceApi.csproj -c Release -o /app/out

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/out ./

ENV ASPNETCORE_URLS=http://+:${PORT}
ENTRYPOINT ["dotnet", "FinanceApi.dll"]
