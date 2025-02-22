FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src
COPY ["HitoHoney/HitoHoney.csproj", "HitoHoney/"]
RUN dotnet restore "HitoHoney/HitoHoney.csproj"
COPY . .
WORKDIR "/src/HitoHoney"
RUN dotnet build "HitoHoney.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "HitoHoney.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HitoHoney.dll"]
