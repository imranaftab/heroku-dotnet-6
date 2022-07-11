#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["demo-dotnet-6/demo-dotnet-6.csproj", "demo-dotnet-6/"]
RUN dotnet restore "demo-dotnet-6/demo-dotnet-6.csproj"
COPY . .
WORKDIR "/src/demo-dotnet-6"
RUN dotnet build "demo-dotnet-6.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "demo-dotnet-6.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "demo-dotnet-6.dll"]