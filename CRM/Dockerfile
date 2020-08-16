#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["CRM/CRM.csproj", "CRM/"]
RUN dotnet restore "CRM/CRM.csproj"
COPY . .
WORKDIR "/src/CRM"
RUN dotnet build "CRM.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CRM.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CRM.dll"]