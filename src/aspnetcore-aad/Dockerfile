#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0.2-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0.201-buster-slim AS build
WORKDIR /src
COPY ["aspnetcore-aad.csproj", ""]
RUN dotnet restore "./aspnetcore-aad.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "aspnetcore-aad.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "aspnetcore-aad.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "aspnetcore-aad.dll"]