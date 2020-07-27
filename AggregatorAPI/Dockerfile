#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM  microsoft/aspnetcore:2.0-nanoserver-1803 AS base
WORKDIR /app

FROM microsoft/aspnetcore-build:2.0-nanoserver-1803 AS build-env
WORKDIR /src

# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o /app/out

# Build runtime image
FROM base AS final
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "AggregatorAPI.dll"]