FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 54100
ENV ASPNETCORE_URLS=http://*:54100

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["web-app.csproj", "./"]
RUN dotnet restore "web-app.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "web-app.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "web-app.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "web-app.dll"]
