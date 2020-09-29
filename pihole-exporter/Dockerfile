# image for builder
FROM golang:alpine as builder

ENV PIHOLE_EXPORTER_VERSION "0.0.9"

RUN apk update && \
    apk --no-cache add git alpine-sdk upx

RUN git clone --branch ${PIHOLE_EXPORTER_VERSION} https://github.com/eko/pihole-exporter.git /go/src/github.com/eko/pihole-exporter

WORKDIR /go/src/github.com/eko/pihole-exporter

RUN GO111MODULE=on go mod vendor
RUN CGO_ENABLED=0 GOOS=linux GOARCH=arm GOARM=7 go build -ldflags '-s -w' -o binary ./

RUN upx -f --brute binary

# Image for usage
FROM scratch

LABEL name="pihole-exporter"

WORKDIR /root/
COPY --from=builder /go/src/github.com/eko/pihole-exporter/binary pihole-exporter

CMD ["./pihole-exporter"]
