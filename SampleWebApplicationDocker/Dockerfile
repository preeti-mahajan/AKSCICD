#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat 

    
FROM mcr.microsoft.com/dotnet/framework/sdk:4.8 AS build
WORKDIR /app

# copy csproj and restore as distinct layers
COPY *.sln .
COPY SampleWebApplicationDocker/*.csproj ./SampleWebApplicationDocker/
COPY SampleWebApplicationDocker/*.config ./SampleWebApplicationDocker/
RUN nuget restore

# copy everything else and build app
COPY SampleWebApplicationDocker/. ./SampleWebApplicationDocker/
WORKDIR /app/SampleWebApplicationDocker
RUN msbuild /p:Configuration=Release


FROM mcr.microsoft.com/dotnet/framework/aspnet:4.8 AS runtime
WORKDIR /inetpub/wwwroot
COPY --from=build /app/SampleWebApplicationDocker/. ./