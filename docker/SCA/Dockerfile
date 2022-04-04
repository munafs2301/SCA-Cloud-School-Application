FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["./SCA.csproj", "SCA/"]
RUN dotnet restore "SCA/SCA.csproj"
WORKDIR "/src/SCA"
COPY . .

RUN dotnet build "SCA.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SCA.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SCA.dll"]
