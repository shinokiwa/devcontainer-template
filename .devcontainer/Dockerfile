FROM rockylinux:9

# Install basic tools and Docker
RUN dnf install -y \
    git \
    sudo \
    wget \
    curl \
    vim \
    && dnf clean all

# Install Docker
RUN dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo \
    && dnf install -y \
    docker-ce \
    docker-ce-cli \
    containerd.io \
    docker-buildx-plugin \
    docker-compose-plugin \
    && dnf clean all

# Create a non-root user
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# Add user to docker group
RUN usermod -aG docker $USERNAME

USER $USERNAME
