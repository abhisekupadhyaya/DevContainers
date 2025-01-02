FROM continuumio/miniconda3

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
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && adduser $USERNAME sudo \
    && echo "$USERNAME ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# Install VSCode server and set up environment
RUN curl -fsSL https://code-server.dev/install.sh | sh

COPY environment.yml /workspace/environment.yml
RUN conda env create -f environment.yml && conda clean -a

# Set proper permissions
RUN mkdir -p /root/.conda && \
    chown -R $USERNAME:$USERNAME /root/.conda && \
    chown -R $USERNAME:$USERNAME /workspace

USER $USERNAME

EXPOSE 11434

CMD ["code-server", "--bind-addr", "0.0.0.0:11434", "/workspace"]