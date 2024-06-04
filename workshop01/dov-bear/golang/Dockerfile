# first container to build executable 
FROM golang:1.22.3-alpine3.20 AS builder

WORKDIR /app

COPY go.mod .
COPY go.sum .
COPY main.go .

# building an executable named main
RUN go build -o main main.go

# second container to use the executable from builder container
FROM alpine:3.20 AS runner

WORKDIR /app

# copy the executable named main to runner container
COPY --from=builder /app/main main
COPY public public
COPY templates templates

# health check
RUN apk update && apk add curl

ENV PORT=3000

EXPOSE ${PORT}

HEALTHCHECk --interval=30s --timeout=5s --start-period=5s --retries=3 CMD curl -s http://localhost:${PORT}/healthz || exit 1

ENTRYPOINT /app/main