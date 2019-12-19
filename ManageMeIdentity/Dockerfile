FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
#WORKDIR /app
#EXPOSE 80
#EXPOSE 443

WORKDIR /src
COPY ManageMeAuth.csproj .
RUN dotnet restore "ManageMeAuth.csproj"
COPY . .

RUN dotnet build "ManageMeAuth.csproj" -c Release -o /app/build
RUN dotnet publish "ManageMeAuth.csproj" -c Release -o /app/publish

FROM build AS final
WORKDIR /app
COPY --from=build /app/publish .

#ENV ASPNETCORE_ENVIRONMENT=Development
#ENTRYPOINT ["dotnet", "ManageMeWebsite.dll"]
CMD ASPNETCORE_URLS=http://*:$PORT ASPNETCORE_ENVIRONMENT=Development dotnet ManageMeAuth.dll