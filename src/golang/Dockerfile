FROM golang:1.17-bullseye AS build

WORKDIR /go/src/app 

COPY *.go .
RUN go mod init
RUN go get -d -v ./...

RUN go build -o /go/bin/app
COPY file.p12 /go/bin

FROM gcr.io/distroless/base-debian11
EXPOSE 80
COPY --from=build /go/bin/app /
COPY --from=build /go/bin/file.p12 /
CMD ["/app"]


