# Choose runtime for .dll file to run
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base

WORKDIR /app

# Define port 80 for http access
EXPOSE 80

# Define port 443 for https access
EXPOSE 443

# Choose skd to compile,build and publish application
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build


# Choose root-folder where to do the sdk stuff
WORKDIR /src

COPY . .

# .cproj is the projectfile 
#COPY ./api/Basic3TierAPI/Basic3TierAPI.csproj Basic3TierAPI/

# restore download all the dependencies
RUN dotnet restore /src/api/Basic3TierAPI/Basic3TierAPI.csproj

#COPY ./api/Basic3Tier.Core/Basic3Tier.Core.csproj Basic3Tier.Core/

#COPY ./api/Basic3Tier.Infrastructure/Basic3Tier.Infrastructure.csproj Basic3Tier.Infrastructure/

RUN dotnet restore /src/api/Basic3Tier.Core/Basic3Tier.Core.csproj

RUN dotnet restore /src/api/Basic3Tier.Infrastructure/Basic3Tier.Infrastructure.csproj

#RUN dotnet build -c Release -o /app/build

FROM build AS publish

# change to this directorey to start building
WORKDIR /src/api/Basic3TierAPI

RUN dotnet publish -c Release -o /app/publish

# Define where to look at runtime
FROM base AS final

WORKDIR /app

COPY --from=publish /app/publish .

ENTRYPOINT ["dotnet", "Basic3TierAPI.dll"]