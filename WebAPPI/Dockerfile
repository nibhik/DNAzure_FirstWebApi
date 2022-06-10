#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.



FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build-env
WORKDIR /app
COPY ["WebAPPI/WebAPPI.csproj", "WebAPPI/"]
RUN dotnet restore "WebAPPI/WebAPPI.csproj"
COPY . .
WORKDIR "/src/WebAPPI"
RUN dotnet build "WebAPPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebAPPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebAPPI.dll"]
