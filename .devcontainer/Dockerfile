# 開発作業用コンテナ
# ほぼただの作業用Rocky Linux

# バージョンわからないのも困るので明記
FROM rockylinux:9.3

# ビルド時引数
ARG USER_NAME
ARG USER_UID
ARG USER_GID
ARG DOCKER_GID

# 実行時も引き継ぐ
ENV USER_UID=${USER_UID}
ENV USER_GID=${USER_GID}
ENV DOCKER_GID=${DOCKER_GID}

# 必要なツールのインストール
RUN dnf -y update && dnf -y install \
  dnf-plugins-core \
  ca-certificates \
  sudo \
  gnupg2 \
  unzip \
  git \
  mysql \
  iputils bind-utils

# ユーザの作成
RUN useradd -m -u ${USER_UID} -s /bin/bash ${USER_NAME} && \
  echo "${USER_NAME} ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Remiリポジトリを追加
RUN dnf -y install https://rpms.remirepo.net/enterprise/remi-release-9.rpm

# Dockerグループの作成
RUN groupadd -g ${DOCKER_GID} docker
RUN usermod -aG docker ${USER_NAME}

# DockerオフィシャルのGPGキーを追加
RUN install -m 0755 -d /etc/pki/rpm-gpg && \
  curl -fsSL https://download.docker.com/linux/centos/gpg -o /etc/pki/rpm-gpg/docker.asc

# Dockerのリポジトリを追加
RUN dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
RUN dnf -y update && dnf -y install docker-ce docker-ce-cli containerd.io docker-compose-plugin

# タイムゾーンの設定
ENV TZ=Asia/Tokyo
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# ENTRYPOINTの設定
COPY ./.devcontainer/entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

USER ${USER_NAME}
WORKDIR /workspace