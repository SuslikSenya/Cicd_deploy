FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app 

RUN groupadd --gid 1000 appuser && \ 
    useradd --uid 1000 --gid appuser --shell /bin/bash --create-home appuser

COPY --chown==appuser:appuser published/ ./ 

USER appuser
EXPOSE 5149 
 
ENTRYPOINT ["dotnet", "DevOpsProject.HiveMind.API.dll"]