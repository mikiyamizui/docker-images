FROM mikiyamizui/base-sdk-alpine

ARG URL=https://download.visualstudio.microsoft.com/download/pr/c8b8c117-a7b8-4a4f-ac3e-e97aac2e1b1a/fd0f3f7461ad7c518c2b0aa5613c80ca/dotnet-sdk-2.2.401-linux-musl-x64.tar.gz

USER root
RUN apk update \
    && apk add --no-cache \
    krb5-libs \
    libgcc \
    icu-libs \
    libintl \
    libssl1.1 \
    libstdc++ \
    lttng-ust \
    tzdata \
    userspace-rcu \
    zlib \
    && wget -nv -O dotnet.tar.gz $URL \
    && mkdir -p /usr/share/dotnet \
    && tar -C /usr/share/dotnet -xzf dotnet.tar.gz \
    && chown -R root:root /usr/share/dotnet \
    && ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet \
    && rm dotnet.tar.gz

USER dev
ENV DOTNET_SYSTEM_GLOBALIZATION_INVARIANT=false
ENV ASPNETCORE_URLS=http://+:80
ENV DOTNET_RUNNING_IN_CONTAINER=true
ENV DOTNET_USE_POLLING_FILE_WATCHER=true
ENV NUGET_XMLDOC_MODE=skip
RUN dotnet help
