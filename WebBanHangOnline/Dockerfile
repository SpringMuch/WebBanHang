
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

ARG BUILD_CONTEXT

COPY ["${BUILD_CONTEXT}/WebBanHangOnline.csproj", "./"]
RUN dotnet restore "WebBanHangOnline.csproj"

COPY "${BUILD_CONTEXT}/." .
RUN dotnet build "WebBanHangOnline.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebBanHangOnline.csproj" -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebBanHangOnline.dll"]
