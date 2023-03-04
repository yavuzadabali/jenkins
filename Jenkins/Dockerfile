FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Jenkins/Jenkins.csproj", "Jenkins/"]
RUN dotnet restore "Jenkins/Jenkins.csproj"
COPY . .
WORKDIR "/src/Jenkins"
RUN dotnet build "Jenkins.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Jenkins.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Jenkins.dll"]