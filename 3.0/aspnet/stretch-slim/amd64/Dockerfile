ARG REPO=mcr.microsoft.com/dotnet/core/runtime
FROM $REPO:3.0-stretch-slim

# Install ASP.NET Core
ENV ASPNETCORE_VERSION 3.0.0-preview3-19128-02

RUN curl -SL --output aspnetcore.tar.gz https://dotnetcli.blob.core.windows.net/dotnet/aspnetcore/Runtime/$ASPNETCORE_VERSION/aspnetcore-runtime-$ASPNETCORE_VERSION-linux-x64.tar.gz \
    && aspnetcore_sha512='f59be95a812581ebab01070ef53cac89d705266b7fd0fe96dd2d1fd3caccfa4ca6cbae9238962dc32ae506b50a210cc6d3c890f59ffb2f21d1a738105e5fa7e6' \
    && echo "$aspnetcore_sha512  aspnetcore.tar.gz" | sha512sum -c - \
    && tar -zxf aspnetcore.tar.gz -C /usr/share/dotnet ./shared/Microsoft.AspNetCore.App \
    && rm aspnetcore.tar.gz
