#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["demomvccore/demomvccore.csproj", ""]
RUN dotnet restore "demomvccore/demomvccore.csproj"
COPY . .
WORKDIR "/src/demomvccore"
RUN dotnet build "demomvccore.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "demomvccore.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "demomvccore.dll"]