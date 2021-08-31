FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
ENV ASPNETCORE_URLS=http://*:80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["demomvccore/demomvccore.csproj", "./"]
RUN dotnet restore "demomvccore.csproj"
COPY . .
WORKDIR "/src/demomvccore"
RUN dotnet build "demomvccore.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "demomvccore.csproj" -c Release -o /app/publish

FROM base AS final

USER 0

WORKDIR /app
COPY --from=publish /app/publish .

RUN chown -R 1001:0 /app && chmod -R og+rwx /app

USER 1001

ENTRYPOINT ["dotnet", "demomvccore.dll"]
