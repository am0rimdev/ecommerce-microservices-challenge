# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY Stock.csproj .
RUN dotnet restore "Stock.csproj"
COPY . .
RUN dotnet publish "Stock.csproj" -c Release -o /app/publish --no-restore

# Final stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "Stock.dll"]

# Create a non-root user
RUN adduser -u 5000 --disabled-password --gecos "" appuser
USER appuser
