# escape=`

FROM mcr.microsoft.com/windows/servercore:ltsc2019@sha256:997e32161f322f5f301023ae675f39329bd60888f5f9a373100eba77f55cbb31 AS installer

LABEL maintainer="Michael Kriese <michael.kriese@visualon.de>" `
    org.opencontainers.image.authors="Michael Kriese <michael.kriese@visualon.de>" `
    org.opencontainers.image.licenses="MIT" `
    org.opencontainers.image.source="https://github.com/VisualOn/docker-images" `
    org.opencontainers.image.url="https://github.com/VisualOn/docker-images"

# renovate: datasource=github-tags depName=meltwater/drone-cache
ARG CACHE_VERSION=1.1.0

RUN `
  mkdir tmp && cd tmp`
	&& curl -sSfLo cache.zip https://github.com/meltwater/drone-cache/releases/download/v%CACHE_VERSION%/drone-cache_%CACHE_VERSION%_Windows_x86_64.zip `
  && tar -oxzf cache.zip `
  && move drone-cache_%CACHE_VERSION%_Windows_x86_64 c:\bin `
  && /bin/drone-cache --version

FROM mcr.microsoft.com/windows/nanoserver:1809-amd64@sha256:e27d06463660ed9fb963fc8d9c9c7d286450107161a029c29ddb4c916d15d1f5

COPY --from=installer ["/bin", "/bin"]

ENTRYPOINT ["/bin/drone-cache"]
