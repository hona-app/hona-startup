FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR "/app"

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR "/src"
#把整个api项目，复制到当前工作目录
COPY "../../api" .
RUN ls -ld $PWD/*
WORKDIR "Hona.Api"
RUN dotnet restore "Hona.Api.csproj"
RUN dotnet build "Hona.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Hona.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR "/app"
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Hona.Api.dll"]

EXPOSE 80 443