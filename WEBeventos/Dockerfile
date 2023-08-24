FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["WEBeventos/WEBeventos.csproj", "WEBeventos/"]
RUN dotnet restore "WEBeventos/WEBeventos.csproj"
COPY . .
WORKDIR "/src/WEBeventos"
RUN dotnet build "WEBeventos.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WEBeventos.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WEBeventos.dll"]
