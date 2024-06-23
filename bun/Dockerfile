# Use the base image with specified platform
FROM --platform=$TARGETOS/$TARGETARCH oven/bun:latest

LABEL author="Razorrftw" maintainer="ryanw@beaconhosting.org"

# Update package lists and install necessary packages including Git
RUN apt-get update \
    && apt-get -y install \
        software-properties-common \
        python3 \
        python3-dev \
        ffmpeg \
        iproute2 \
        git \
        sqlite3 \
        libsqlite3-dev \
        ca-certificates \
        dnsutils \
        tzdata \
        zip \
        tar \
        curl \
        build-essential \
        libtool \
        tini \
        net-tools \
        iputils-ping \
    && useradd -m -d /home/container container \
    && chown -R container:container /bin/ping \
    && bun upgrade

USER container
ENV USER=container HOME=/home/container
WORKDIR /home/container

STOPSIGNAL SIGINT

# Copy entrypoint script
COPY --chown=container:container ./../entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

# Define entrypoint
ENTRYPOINT ["/usr/bin/tini", "-g", "--"]
CMD ["/entrypoint.sh"]
