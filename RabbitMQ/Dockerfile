FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["RabbitMQ/RabbitMQ..csproj", "RabbitMQ/"]
RUN dotnet restore "RabbitMQ/RabbitMQ..csproj"
COPY . .
WORKDIR "/src/RabbitMQ"
RUN dotnet build "RabbitMQ..csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "RabbitMQ..csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "RabbitMQ..dll"]
