FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["CoreWebApplication2/CoreWebApplication2.csproj", "CoreWebApplication2/"]
RUN dotnet restore "CoreWebApplication2/CoreWebApplication2.csproj"
COPY . .
WORKDIR "/src/CoreWebApplication2"
RUN dotnet build "CoreWebApplication2.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "CoreWebApplication2.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CoreWebApplication2.dll"]