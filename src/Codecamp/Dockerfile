FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /build
COPY ["./src", "./src"]
COPY . .
RUN dotnet restore "CodeCampster.sln"
WORKDIR "/build/src/Codecamp"
RUN ls
RUN dotnet build "Codecamp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Codecamp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Codecamp.dll"]