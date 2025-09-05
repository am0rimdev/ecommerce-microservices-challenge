# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY Sales.csproj .
RUN dotnet restore "Sales.csproj"
COPY . .
RUN dotnet publish "Sales.csproj" -c Release -o /app/publish --no-restore

# Final stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "Sales.dll"]

# Create a non-root user
RUN adduser -u 5000 --disabled-password --gecos "" appuser
USER appuser
