#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["WebApplication7.csproj", "WebApplication7/"]
RUN dotnet restore "WebApplication7/WebApplication7.csproj"
COPY . WebApplication7/
WORKDIR "/src/WebApplication7"
RUN dotnet build "WebApplication7.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "WebApplication7.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApplication7.dll"]