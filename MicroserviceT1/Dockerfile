#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["MicroserviceT1/MicroserviceT1.csproj", "MicroserviceT1/"]
RUN dotnet restore "MicroserviceT1/MicroserviceT1.csproj"
COPY . .
WORKDIR "/src/MicroserviceT1"
RUN dotnet build "MicroserviceT1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MicroserviceT1.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MicroserviceT1.dll"]