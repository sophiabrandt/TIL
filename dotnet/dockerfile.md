# Dockerfile

Example Dockerfile for dotnet 8 that publishes a single file and runs it from a distroless runtime image.

```dockerfile
# BUILD IMAGE
FROM mcr.microsoft.com/dotnet/sdk:8.0-bookworm-slim-arm64v8 AS build

WORKDIR /src

COPY ["src/OneReview/OneReview.csproj", "OneReview/"]
RUN dotnet restore "OneReview/OneReview.csproj" -r linux-arm64 /p:PublishReadyToRun=true

COPY ["src/OneReview", "OneReview/"]
WORKDIR /src/OneReview
RUN dotnet build "OneReview.csproj" -c Release -o /app/build

# PUBLISH IMAGE
FROM build AS publish
RUN dotnet publish "OneReview.csproj" --no-restore -c Release -r linux-arm64 \
  /p:PublishTrimmed=true /p:PublishSingleFile=true \
  --self-contained=true -o /app/publish

# LIBZ
FROM debian:bookworm-slim AS libz
RUN apt-get update && apt-get install -y zlib1g libgcc-s1 libstdc++6

# RUNTIME IMAGE
FROM gcr.io/distroless/base-debian12:nonroot-arm64 AS runtime
WORKDIR /app

COPY --from=libz /usr/lib/aarch64-linux-gnu/libz.so.1 /lib/libz.so.1
COPY --from=libz /usr/lib/aarch64-linux-gnu/libgcc_s.so.1 /lib/libgcc_s.so.1
COPY --from=libz /usr/lib/aarch64-linux-gnu/libstdc++.so.6 /lib/libstdc++.so.6

COPY --from=publish /app/publish .

ENV ASPNETCORE_URLS=http://+:5001
EXPOSE 5001

ENTRYPOINT ["./OneReview"]
```
