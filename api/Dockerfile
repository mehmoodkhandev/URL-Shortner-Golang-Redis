# ---- Build stage ----
FROM golang:1.24-alpine AS builder

WORKDIR /app

# Copy go.mod and go.sum first (for caching)
COPY go.mod go.sum ./
RUN go mod download

# Copy the rest of your source code and .env
COPY . .

# Build the Go binary
RUN go build -o main .

# ---- Run stage ----
FROM alpine:latest

RUN adduser -S -D -H -h /app appuser

USER appuser
WORKDIR /app

# Copy binary
COPY --from=builder /app/main .

EXPOSE 3000
CMD ["./main"]
