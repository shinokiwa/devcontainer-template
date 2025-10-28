# DevContainer 設定

このディレクトリには、VSCode Dev Container の設定ファイルが含まれています。

## 構成

### Dockerfile
- **ベースイメージ**: Rocky Linux 9
- **インストール済みツール**:
  - Docker CE (Docker Engine)
  - Docker Compose Plugin
  - Docker Buildx Plugin
  - Git, sudo, wget, curl, vim

### docker-compose.yml
- **Docker-in-Docker (DooD)**: ホストの Docker ソケット (`/var/run/docker.sock`) をマウント
- **ワークスペース**: `/workspace` にマウント

### devcontainer.json
- **VSCode 拡張機能**: Docker 拡張機能を自動インストール
- **ユーザー**: `vscode` (非rootユーザー)

## 使い方

1. このリポジトリをクローン
2. VSCode で開く
3. コマンドパレット (Ctrl+Shift+P / Cmd+Shift+P) を開く
4. "Dev Containers: Reopen in Container" を選択
5. コンテナが構築され、開発環境が起動します

## Docker の使用

コンテナ内で Docker コマンドを実行できます：

```bash
docker --version
docker ps
docker compose version
```

DooD (Docker-outside-of-Docker) 設定により、ホストの Docker デーモンを使用します。
