#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["Dockerfile/Dockerfile.csproj", "Dockerfile/"]
RUN dotnet restore "Dockerfile/Dockerfile.csproj"
COPY . .
WORKDIR "/src/Dockerfile"
RUN dotnet build "Dockerfile.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Dockerfile.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Dockerfile.dll"]