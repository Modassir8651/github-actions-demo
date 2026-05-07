FROM golang:1.26-alpine AS builder

RUN apk add --no-cache git ca-certificates

WORKDIR /app

COPY . .

# ❌ REMOVE this line
# RUN go mod tidy

# ✅ direct build (skip tidy)
RUN CGO_ENABLED=0 GOOS=linux go build -o skillpulse .

FROM alpine:3.18

RUN apk add --no-cache ca-certificates

WORKDIR /app

COPY --from=builder /app/skillpulse .

EXPOSE 8080

CMD ["./skillpulse"]