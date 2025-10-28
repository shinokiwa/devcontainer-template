# devcontainer-template
自分的なVSCode DevContainerのテンプレート

## 概要

このリポジトリは、Rocky Linux 9 ベースの VSCode Dev Container 設定を提供します。

## 特徴

- **ベースOS**: Rocky Linux 9
- **Docker サポート**: Docker-in-Docker (DooD) によるコンテナ管理
- **開発ツール**: Git, Docker, Docker Compose などがプリインストール
- **VSCode 統合**: Docker 拡張機能が自動インストールされます

## 使い方

1. このリポジトリをクローン
```bash
git clone https://github.com/shinokiwa/devcontainer-template.git
cd devcontainer-template
```

2. VSCode で開く
```bash
code .
```

3. VSCode のコマンドパレット (Ctrl+Shift+P / Cmd+Shift+P) から:
   - "Dev Containers: Reopen in Container" を選択

4. コンテナが構築され、開発環境が起動します

## 詳細

詳しい設定については [.devcontainer/README.md](.devcontainer/README.md) を参照してください。
