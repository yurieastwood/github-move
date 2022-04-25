#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["GitHub.Upload.API/GitHub.Upload.API.csproj", "GitHub.Upload.API/"]
RUN dotnet restore "GitHub.Upload.API/GitHub.Upload.API.csproj"
COPY . .
WORKDIR "/src/GitHub.Upload.API"
RUN dotnet build "GitHub.Upload.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "GitHub.Upload.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "GitHub.Upload.API.dll"]