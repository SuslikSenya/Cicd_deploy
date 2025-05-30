# Этап сборки
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Копируем только нужные файлы для восстановления зависимостей
COPY src/CommunicationControl/DevOpsProject/*.csproj ./DevOpsProject/
RUN dotnet restore ./DevOpsProject/DevOpsProject.CommunicationControl.API.csproj

# Копируем весь исходный код
COPY src/CommunicationControl/DevOpsProject ./DevOpsProject/

# Публикуем проект в режиме Release в папку /publish
RUN dotnet publish ./DevOpsProject/DevOpsProject.CommunicationControl.API.csproj -c Release -o /publish

# Этап выполнения
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app

# Копируем артефакты из этапа сборки
COPY --from=build /publish .

EXPOSE 8080

ENTRYPOINT ["dotnet", "DevOpsProject.CommunicationControl.API.dll"]




# FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime Add commentMore actions
# WORKDIR /app 

# RUN groupadd --gid 1000 appuser && \ 
#     useradd --uid 1000 --gid appuser --shell /bin/bash --create-home appuser

# COPY --chown==appuser:appuser published/ ./ 
# USER appuser
# EXPOSE 8080 
 
# ENTRYPOINT ["dotnet", "DevOpsProject.CommunicationControl.API.dll"]