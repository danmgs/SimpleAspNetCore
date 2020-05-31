#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["SimpleAspNetCore/SimpleAspNetCore.csproj", "SimpleAspNetCore/"]
RUN dotnet restore "SimpleAspNetCore/SimpleAspNetCore.csproj"
COPY . .
WORKDIR "/src/SimpleAspNetCore"
RUN dotnet build "SimpleAspNetCore.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SimpleAspNetCore.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SimpleAspNetCore.dll"]