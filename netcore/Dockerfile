FROM mcr.microsoft.com/dotnet/core/sdk:3.0-alpine AS build
WORKDIR /app

# copy csproj and restore as distinct layers
COPY *.sln .
COPY Sample/*.csproj ./Sample/
RUN dotnet restore

# copy everything else and build app
COPY Sample/. ./Sample/
WORKDIR /app/Sample
RUN dotnet publish -c Release -o out


FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-alpine AS runtime
WORKDIR /app
COPY --from=build /app/Sample/out ./
ENTRYPOINT ["dotnet", "Sample.dll"]