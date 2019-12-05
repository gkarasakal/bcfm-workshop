FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["bcfmworkshop/bcfmworkshop.csproj", "bcfmworkshop/"]
RUN dotnet restore "bcfmworkshop/bcfmworkshop.csproj"
COPY . .
WORKDIR "/src/bcfmworkshop"
RUN dotnet build "bcfmworkshop.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "bcfmworkshop.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "bcfmworkshop.dll"]