FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Rt.Dotnet.EcsApi/Rt.Dotnet.EcsApi.csproj", "Rt.Dotnet.EcsApi/"]
RUN dotnet restore "Rt.Dotnet.EcsApi/Rt.Dotnet.EcsApi.csproj"
COPY . .
WORKDIR "/src/Rt.Dotnet.EcsApi"
RUN dotnet build "Rt.Dotnet.EcsApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Rt.Dotnet.EcsApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Rt.Dotnet.EcsApi.dll"]
