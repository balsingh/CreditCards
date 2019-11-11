FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS base
WORKDIR /app
EXPOSE 500

FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build-env
WORKDIR /app
# copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore CreditCards.csproj
# copy everything else and build
COPY . ./
RUN dotnet build CreditCards.csproj -c Release -o out

# build runtime image
FROM build-env AS publish
RUN dotnet publish CreditCards.csproj -c Release -o out	

FROM base AS final
COPY --from=publish /app/out ./
ENTRYPOINT ["dotnet", "CreditCards.dll"]
