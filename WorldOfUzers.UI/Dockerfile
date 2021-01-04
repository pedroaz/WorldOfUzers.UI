#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["WorldOfUzers.UI/WorldOfUzers.UI.csproj", "WorldOfUzers.UI/"]
RUN dotnet restore "WorldOfUzers.UI/WorldOfUzers.UI.csproj"
COPY . .
WORKDIR "/src/WorldOfUzers.UI"
RUN dotnet build "WorldOfUzers.UI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WorldOfUzers.UI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WorldOfUzers.UI.dll"]