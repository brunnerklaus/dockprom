# Builder
FROM arm32v7/golang as builder

ENV RPI_EXPORTER_VERSION "v0.6.0"

RUN apt-get update && apt-get install -y git dmsetup && apt-get clean

RUN git clone --branch ${RPI_EXPORTER_VERSION} https://github.com/lukasmalkmus/rpi_exporter.git /go/src/github.com/lukasmalkmus/rpi_exporter

WORKDIR /go/src/github.com/lukasmalkmus/rpi_exporter

RUN make build

# Image for usage
FROM arm32v7/debian

COPY --from=builder /go/src/github.com/lukasmalkmus/rpi_exporter /usr/bin/rpi_exporter

EXPOSE 9243
ENTRYPOINT ["/usr/bin/rpi_exporter"]
