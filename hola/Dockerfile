FROM golang:alpine AS builder
RUN apk add --no-cache git && mkdir -p $GOPATH/src/github.com/DTherHtun/gitactions-test/hola && go get github.com/rakyll/statik
WORKDIR $GOPATH/src/github.com/DTherHtun/gitactions-test/hola
COPY . .
RUN sed -i 's#./index.html#/go/bin/index.html#g' main.go 
RUN CGO_ENABLED=0 GOOS=linux go build -ldflags="-w -s" -a -installsuffix cgo -o /go/bin/hola .
FROM scratch
COPY --from=builder /go/src/github.com/DTherHtun/gitactions-test/hola/index.html /go/bin/index.html
COPY --from=builder /go/bin/hola /go/bin/hola
ENTRYPOINT ["/go/bin/hola"]
EXPOSE 8080
