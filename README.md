# あらゆる現実のはなし (arayuru-genjitu-blog)

Yukara Ikemiya のブログレポジトリです。  
Hugo と [Casper Two](https://github.com/eueung/hugo-casper-two) テーマ（Git submodule）を用いて構築されており、GitHub Pages でホスティングされています。

- **公開 URL**: [https://yukara-ikemiya.github.io/arayuru-genjitu-blog/](https://yukara-ikemiya.github.io/arayuru-genjitu-blog/)
- **英語トップ**: [https://yukara-ikemiya.github.io/arayuru-genjitu-blog/en/](https://yukara-ikemiya.github.io/arayuru-genjitu-blog/en/)
- **対応 Hugo バージョン**: v0.165.0 以降（Extended 版推奨）

---

## 目次

1. [環境の準備・セットアップ](#1-環境の準備セットアップ)
2. [ローカル開発サーバーの起動](#2-ローカル開発サーバーの起動)
3. [記事の作成・執筆手順](#3-記事の作成執筆手順)
4. [サイトのビルドとデプロイ](#4-サイトのビルドとデプロイ)
5. [主要コマンド一覧](#5-主要コマンド一覧)

---

## 1. 環境の準備・セットアップ

### Hugo の準備
Hugo v0.165.0 以上の実行ファイルを用意し、パスを通すか直接実行できるようにしてください。

### レポジトリのクローン
本レポジトリはテーマを Git Submodule として管理しています。サブモジュールを含めてクローンします。

```bash
git clone --recursive https://github.com/yukara-ikemiya/arayuru-genjitu-blog.git
```

既にクローン済みの場合は、以下でサブモジュールを初期化・更新します。

```bash
git submodule update --init --recursive
```

---

## 2. ローカル開発サーバーの起動

ローカルでプレビューを確認しながら執筆・編集できます。ファイルの変更を検知してブラウザが自動リロードされます。

```bash
# 通常起動（公開記事のみ）
hugo server

# 下書き（draft: true）を含めてプレビュー
hugo server -D
```

- **日本語サイト**: `http://localhost:1313/`
- **英語サイト**: `http://localhost:1313/en/`

---

## 3. 記事の作成・執筆手順

本ブログは **多言語対応（日本語 `ja` / 英語 `en`）** になっています。

### ファイルの命名規則と配置場所
`content/post/` ディレクトリ内に、同じベース名（日付やスラッグ）で日本語版と英語版のペアを作成します。

- 日本語記事: `content/post/YYYYMMDD.ja.md`
- 英語記事: `content/post/YYYYMMDD.en.md`

> **Note**: ファイルのベース名（`YYYYMMDD`）を一致させることで、Hugo が自動的に言語切り替えリンク（`JA / EN`）を紐付けます。

### フロントマターのフォーマット

各 Markdown ファイルの先頭に以下のメタデータ（YAML 形式）を記述します。

```yaml
---
author: "Yukara Ikemiya"
authorAvatar: img/yukara_profile.jpg
date: 2024-01-01
title: "記事のタイトル"
linktitle: "記事のタイトル"
image: post/img/YYYYMMDD/eyecatch.jpg

tags:
  - "ai"
  - "deep learning"
categories:
  - "Technology"

weight: 10
draft: false
---
```

#### 主なパラメータ説明
- `title`: 記事のタイトル（※ コロン `:` を含む場合は必ず `""` で囲んでください）
- `linktitle`: ナビゲーション等に表示される短いタイトル
- `date`: 公開日（`YYYY-MM-DD`）
- `image`: アイキャッチ画像のパス（例: `post/img/20231224/sunoai_cover.jpg`）
- `tags`: タグ一覧（小文字・ハイフン区切り推奨）
- `categories`: カテゴリ（`Technology`, `Diary`, `Food` 等）
- `draft`: 下書きフラグ（`true` の場合は `hugo server -D` のみ表示され、本番ビルドには含まれません）

### 画像・動画の配置と挿入方法

- **記事専用の画像/動画**: `content/post/img/` 配下に配置します。
  - Markdown / HTML 内での指定: `<img src="/post/img/YYYYMMDD/filename.jpg" />`
- **サイト共通の画像**: `static/img/` 配下に配置します。
  - Markdown / HTML 内での指定: `<img src="/img/profile.png" />`

---

## 4. サイトのビルドとデプロイ

本ブログは `docs/` ディレクトリの内容を GitHub Pages で公開しています。

### 1. 静的サイトのビルド
以下のコマンドを実行して `docs/` ディレクトリに HTML 等を生成します。

```bash
hugo --cleanDestinationDir
```

### 2. Git へのコミット & プッシュ
ビルド完了後、変更をコミットしてリモートの `main` ブランチにプッシュすると GitHub Pages に自動反映されます。

```bash
git add .
git commit -m "Add new post: YYYYMMDD"
git push origin main
```

---

## 5. 主要コマンド一覧

| コマンド | 説明 |
| :--- | :--- |
| `hugo server` | ローカル開発サーバーを起動 |
| `hugo server -D` | 下書き（`draft: true`）を含むローカル開発サーバーを起動 |
| `hugo --cleanDestinationDir` | 本番用ビルドを実行（`docs/` をクリーンアップして再生成） |
| `hugo version` | Hugo のバージョンを確認 |
| `git submodule update --remote` | テーマのサブモジュールを最新コミットに更新 |