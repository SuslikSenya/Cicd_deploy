# Этап сборки
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Копируем только нужные файлы для восстановления зависимостей
COPY src/CommunicationControl/DevOpsProject.HiveMind.API/*.csproj ./DevOpsProject.HiveMind.API/
RUN dotnet restore ./DevOpsProject.HiveMind.API/DevOpsProject.HiveMind.API.csproj

# Копируем весь исходный код
COPY src/CommunicationControl/DevOpsProject.HiveMind.API ./DevOpsProject.HiveMind.API/

# Публикуем проект в режиме Release в папку /publish
RUN dotnet publish ./DevOpsProject.HiveMind.API/DevOpsProject.HiveMind.API.csproj -c Release -o /publish

# Этап выполнения
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app

# Копируем артефакты из этапа сборки
COPY --from=build /publish .

EXPOSE 8080

ENTRYPOINT ["dotnet", "DevOpsProject.HiveMind.API.dll"]
