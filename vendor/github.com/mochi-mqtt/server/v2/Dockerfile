FROM golang:1.21.0-alpine3.18@sha256:445f34008a77b0b98bf1821bf7ef5e37bb63cc42d22ee7c21cc17041070d134f AS builder

RUN apk update
RUN apk add git

WORKDIR /app

COPY go.mod ./
COPY go.sum ./
RUN go mod download

COPY . ./

RUN go build -o /app/mochi ./cmd


FROM alpine

WORKDIR /
COPY --from=builder /app/mochi .

# tcp
EXPOSE 1883

# websockets
EXPOSE 1882

# dashboard
EXPOSE 8080

ENTRYPOINT [ "/mochi" ]
