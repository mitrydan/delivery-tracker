#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["src/Delivery.State.Api/Delivery.State.Api.csproj", "src/Delivery.State.Api/"]
RUN dotnet restore "src/Delivery.State.Api/Delivery.State.Api.csproj"
COPY . .
WORKDIR "/src/src/Delivery.State.Api"
RUN dotnet build "Delivery.State.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Delivery.State.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Delivery.State.Api.dll"]