# Dockerfile for log-server

# Use an official Golang runtime as a parent image
FROM golang:1.21 as builder

# Set the working directory inside the container
WORKDIR /app

# Copy the Go module files
COPY go.mod go.sum ./
RUN go mod download

# Copy the rest of the application code
COPY . .

# Build the Go app
RUN cd cmd && go build -o /log-ingestor

# Use a minimal image for the runtime
FROM gcr.io/distroless/base-debian10

# Copy the built binary from the builder
COPY --from=builder /log-ingestor /log-ingestor

# Set the entry point to the binary
ENTRYPOINT ["/log-ingestor"]

# Expose the port the app runs on
EXPOSE 3000
