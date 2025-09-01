# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

COPY FinanceApi.csproj ./
RUN dotnet restore FinanceApi.csproj

COPY . ./
RUN dotnet publish FinanceApi.csproj -c Release -o /app/out

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/out ./

ENV ASPNETCORE_URLS=http://+:${PORT}
ENTRYPOINT ["dotnet", "FinanceApi.dll"]

