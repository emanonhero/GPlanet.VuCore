FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["gpWebCore/gpWebCore.csproj", "gpWebCore/"]
RUN dotnet restore "gpWebCore/gpWebCore.csproj"
COPY . .
WORKDIR "/src/gpWebCore"
RUN dotnet build "gpWebCore.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "gpWebCore.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "gpWebCore.dll"]