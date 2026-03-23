FROM golang:1.22-alpine AS builder
WORKDIR /app
COPY . .

RUN go mod tidy && go mod download
RUN CGO_ENABLED=0 GOOS=linux go build -o server .

FROM alpine:latest
WORKDIR /root/
COPY --from=builder /app/server .
EXPOSE 8004
CMD ["./server"]
