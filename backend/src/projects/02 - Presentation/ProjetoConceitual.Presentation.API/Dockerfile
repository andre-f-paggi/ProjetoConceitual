FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["projects/02 - Presentation/ProjetoConceitual.Presentation.API/ProjetoConceitual.Presentation.API.csproj", "projects/02 - Presentation/ProjetoConceitual.Presentation.API/"]
RUN dotnet restore "projects/02 - Presentation/ProjetoConceitual.Presentation.API/ProjetoConceitual.Presentation.API.csproj"
COPY . .
WORKDIR "/src/projects/02 - Presentation/ProjetoConceitual.Presentation.API"
RUN dotnet build "ProjetoConceitual.Presentation.API.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ProjetoConceitual.Presentation.API.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ProjetoConceitual.Presentation.API.dll"]