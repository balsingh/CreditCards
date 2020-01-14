FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS base
WORKDIR /app
EXPOSE 500

FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build-env
WORKDIR /src
# copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore CreditCards.csproj
# copy everything else and build
COPY . ./
RUN dotnet build CreditCards.csproj -c Release -o /app

# build runtime image
FROM build-env AS publish
RUN dotnet publish CreditCards.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app ./
ENTRYPOINT ["dotnet", "CreditCards.dll"]
