# escape=`

ARG REPO=mcr.microsoft.com/dotnet/core/runtime

# Installer image
FROM mcr.microsoft.com/windows/servercore:1709 AS installer

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

# Install ASP.NET Core Runtime
ENV ASPNETCORE_VERSION 3.0.0-preview3-19128-02

RUN Invoke-WebRequest -OutFile aspnetcore.zip https://dotnetcli.blob.core.windows.net/dotnet/aspnetcore/Runtime/$Env:ASPNETCORE_VERSION/aspnetcore-runtime-$Env:ASPNETCORE_VERSION-win-x64.zip; `
    $aspnetcore_sha512 = 'eb1f7658e6f377058acfd0d8492df704fb31f1bbc3cff20b1d4c49fb9bb4e59dc3933ae537f805d3eb62ce23c56864f7918cec5a37ebae96c466f0bb60ef19d5'; `
    if ((Get-FileHash aspnetcore.zip -Algorithm sha512).Hash -ne $aspnetcore_sha512) { `
        Write-Host 'CHECKSUM VERIFICATION FAILED!'; `
        exit 1; `
    }; `
    `
    Expand-Archive aspnetcore.zip -DestinationPath dotnet; `
    Remove-Item -Force aspnetcore.zip

# Runtime image
FROM $REPO:3.0-nanoserver-1709

COPY --from=installer ["/dotnet/shared/Microsoft.AspNetCore.App", "/Program Files/dotnet/shared/Microsoft.AspNetCore.App"]
