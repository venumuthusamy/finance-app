# Stage 1: Build Angular frontend
FROM node:20 AS frontend
WORKDIR /app
COPY ../FinanceUI/package*.json ./
RUN npm install
COPY ../FinanceUI/ .
RUN npm run build --prod

# Stage 2: Build .NET backend
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY . .
RUN dotnet publish -c Release -o /app/publish

# Copy Angular build to wwwroot
COPY --from=frontend /app/dist /src/wwwroot

# Stage 3: Runtime
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "FinanceApi.dll"]
