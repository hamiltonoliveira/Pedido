
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["src/Pedido.Ui/Pedido.Ui.csproj", "src/Pedido.Ui/"]
RUN dotnet restore "src/Pedido.Ui/Pedido.Ui.csproj"
COPY . .
WORKDIR "/src/src/Pedido.Ui"
RUN dotnet build "Pedido.Ui.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Pedido.Ui.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Pedido.Ui.dll"]