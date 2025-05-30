FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app
COPY . .
WORKDIR /app
RUN dotnet restore
RUN dotnet publish DevOpsProject.HiveMind.API.csproj -c Release -o /publish

FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /publish .

EXPOSE 5149
ENTRYPOINT ["dotnet", "DevOpsProject.HiveMind.API.dll"]