#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["A-3/A-3.csproj", "A-3/"]
RUN dotnet restore "A-3/A-3.csproj"
COPY . .
WORKDIR "/src/A-3"
RUN dotnet build "A-3.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "A-3.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "A-3.dll"]