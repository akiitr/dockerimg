FROM alpine:latest

WORKDIR /app

# Download the Fabric binary
RUN wget https://github.com/danielmiessler/fabric/releases/latest/download/fabric-linux-amd64 -O fabric

# Make it executable
RUN chmod +x fabric

# Set the default command
CMD ["./fabric", "-h"]
