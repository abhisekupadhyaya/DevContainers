FROM node:20-bullseye

WORKDIR /workspace

# Install necessary tools
RUN apt-get update && apt-get install -y \
    curl \
    git \
    build-essential \
    sudo \
    && rm -rf /var/lib/apt/lists/*

# Create non-root user
ARG USERNAME=vscode
ARG USER_UID=1500
ARG USER_GID=1500

RUN if getent group $USER_GID > /dev/null 2>&1; then \
        groupmod -n $USERNAME $(getent group $USER_GID | cut -d: -f1); \
    else \
        groupadd --gid $USER_GID $USERNAME; \
    fi \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && adduser $USERNAME sudo \
    && echo "$USERNAME ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# Install VSCode server
RUN curl -fsSL https://code-server.dev/install.sh | sh

# Set up Node.js environment
COPY package*.json ./
RUN npm install && \
    npm cache clean --force

# Set proper permissions
RUN chown -R $USERNAME:$USERNAME /workspace

USER $USERNAME

# Configure npm to use custom directory for global packages
ENV NPM_CONFIG_PREFIX=/home/$USERNAME/.npm-global
RUN mkdir -p /home/$USERNAME/.npm-global

# Install global Node.js development tools
RUN npm install -g nodemon typescript ts-node

EXPOSE 11434
CMD ["code-server", "--bind-addr", "0.0.0.0:11434", "/workspace"]
