# image for builder
FROM golang:alpine as builder

RUN apk update && \
    apk --no-cache add git alpine-sdk upx

RUN git clone --branch master https://github.com/io-developer/prom-smartctl-exporter.git /go/src/github.com/io-developer/prom-smartctl-exporter

WORKDIR /go/src/github.com/io-developer/prom-smartctl-exporter

RUN CGO_ENABLED=0 GOOS=linux GOARCH=arm GOARM=7 go build -ldflags '-s -w' -o binary ./

RUN upx -f --brute binary

# Image for usage
FROM scratch

WORKDIR /root/
COPY --from=builder /go/src/github.com/io-developer/prom-smartctl-exporter/binary prom-smartctl-exporter

EXPOSE 9167
CMD ["./prom-smartctl-exporter"]
