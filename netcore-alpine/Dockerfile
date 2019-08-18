FROM mikiyamizui/base-alpine

ARG URL=https://download.visualstudio.microsoft.com/download/pr/a6b8ba2c-30f2-4bb8-80ed-3f12ac623c41/2455fd6f2369d9a7396bb363482e9047/dotnet-runtime-2.2.6-linux-musl-x64.tar.gz

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
