# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
ARG BUILD_FROM
FROM $BUILD_FROM

ARG PYTHON_VERSION=3.11

RUN apk add --no-cache python3 py3-pip

# Execute during the build of the image
ARG TEMPIO_VERSION BUILD_ARCH
RUN \
    curl -sSLf -o /usr/bin/tempio \
    "https://github.com/home-assistant/tempio/releases/download/${TEMPIO_VERSION}/tempio_${BUILD_ARCH}"

COPY rootfs /
RUN git clone https://github.com/slespersen/PetkitW5BLEMQTT.git && \
    cp -r ./PetkitW5BLEMQTT/PetkitW5BLEMQTT /etc/petkit-ble-bridge/ && \
    rm -rf ./PetkitW5BLEMQTT
#COPY PetkitW5BLEMQTT/PetkitW5BLEMQTT /etc/petkit-ble-bridge/PetkitW5BLEMQTT
# COPY pyproject.toml /usr/bin/PetkitW5BLEMQTT

WORKDIR /etc/petkit-ble-bridge
RUN /etc/petkit-ble-bridge/init

WORKDIR /