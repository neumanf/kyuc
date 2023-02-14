FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Kyuc.API/Kyuc.API.csproj", "Kyuc.API/"]
RUN dotnet restore "Kyuc.API/Kyuc.API.csproj"
COPY . .
WORKDIR "/src/Kyuc.API"
RUN dotnet build "Kyuc.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Kyuc.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Kyuc.API.dll"]
