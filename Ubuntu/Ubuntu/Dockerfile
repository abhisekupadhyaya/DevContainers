# Dockerfile
FROM mcr.microsoft.com/devcontainers/base:jammy

# Install code-server
RUN curl -fsSL https://code-server.dev/install.sh | sh

# Expose the port for code-server
EXPOSE 8833

# Default command to run code-server
CMD ["code-server", "--bind-addr", "0.0.0.0:8833"]
