FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["RabbitMQ.Banking.Api/RabbitMQ.Banking.Api.csproj", "RabbitMQ.Banking.Api/"]
RUN dotnet restore "RabbitMQ.Banking.Api/RabbitMQ.Banking.Api.csproj"
COPY . .
WORKDIR "/src/RabbitMQ.Banking.Api"
RUN dotnet build "RabbitMQ.Banking.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "RabbitMQ.Banking.Api.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "RabbitMQ.Banking.Api.dll"]
