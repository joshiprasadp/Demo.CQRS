FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["Demo.Command.Api/Demo.Command.Api/Demo.Command.Api.csproj", "Demo.Command.Api/"]
RUN dotnet restore "Demo.Command.Api/Demo.Command.Api/Demo.Command.Api.csproj"
COPY . .
WORKDIR "/src/Demo.Command.Api"
RUN dotnet build "Demo.Command.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Demo.Command.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Demo.Command.Api.dll"]
