FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["SignalRDemo/SignalRDemo.csproj", "SignalRDemo/"]
RUN dotnet restore "SignalRDemo/SignalRDemo.csproj"
COPY . .
WORKDIR "/src/SignalRDemo"
RUN dotnet build "SignalRDemo.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "SignalRDemo.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "SignalRDemo.dll"]