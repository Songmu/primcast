---
audio: 1.mp3
title: podbardの紹介
date: 2024-09-06T00:49:39+09:00
description: podbardの紹介と導入方法、使い方について解説します。
---

## podbardとは
podbardは簡単にポッドキャストサイトを作るためのSite Generatorです。コマンドラインツールで、オーディオファイルを元にエピソードのMarkdownを生成し、最終的には静的なサイトを生成します。とにかく音源があれば、すぐにポッドキャストサイトを作成できます。

### 特色
- **手軽**: コマンドラインツールをインストール後、即始められます
- **簡潔**: 覚えることが少なく、すぐに使いこなせます
- **俊敏**: オーディオファイルを配置するだけでサイトが生成できます
- **自由**: 生成内容を自由にカスタマイズできます
- **ポータブル**: 静的サイトなので、ポッドキャスト配信サービスを使わずどこでもホスティングできます
- **仕様準拠**: ポッドキャスト仕様に準拠したRSSフィードを生成するため、あらゆるポッドキャストアプリで購読できます
- **OSS**: MITライセンスで公開されているため、自由に利用できます

### コンセプト
podbardは、ポッドキャストを独自サイトで配信したい人が、ポッドキャストを簡単に始められるようにするソフトウェアです。

音声ファイルを `audio/` ディレクトリに配置し、それに対応するエピソードファイルをMarkdown形式で `episode/` ディレクトリに配置するだけで、ポッドキャストサイトを生成できます。エピソードファイルは自動生成可能なので、最低限音声ファイルさえ配置すれば、すぐに最小構成のサイトを構築できます。

コンセプトは[Yattecast](https://r7kamura.github.io/yattecast/)に近いですが、podbardはGoで書かれており、コマンドラインツールを使ってサイトを再生する点が異なります。ゆくゆくはテンプレートリポジトリやGitHub Actionsを用意するかもしれません。

## 導入方法

Homebrewやgo installを使って `podbard` コマンドをインストールします。

```console
# Homebrew
$ brew install Songmu/tap/podbard

# go install
$ go install github.com/Songmu/podbard/cmd/podbard@latest
```

## 使い方

大まかな流れは以下のとおりです。`audio/` ディレクトリにオーディオファイルを配置するだけですぐにサイトの生成ができます。

1. サイト構築: `podbard init <dirname>` でサイトの雛形を作成します
2. 設定ファイル: `podbard.yaml` をあなたのサイトに合わせて編集します
3. 音声配置: `audio/` ディレクトリにオーディオファイルを配置します
4. エピーソードファイル作成: `podbard episode audio/1.mp3` コマンドでエピソードのMarkdownを生成します
5. サイトのビルド: `podbard build` コマンドでサイトをビルドします

### 1. サイト構築
`podbard init sitename` でサイトの雛形を作成します。雛形のディレクトリには以下のファイルが作成されます。

- **podbard.yaml**
    - 設定ファイル
- **index.md**
    - トップページ用のMarkdownファイル
- **episode/**
    - エピソードのMarkdownファイル格納ディレクトリ
- **audio/**
    - MP3やM4Aファイル格納ディレクトリ
- **template/**
    - Goのhtml/template形式のテンプレートファイル格納ディレクトリ
- **static/**
    - 静的ファイル格納ディレクトリ

#### テンプレートリポジトリ

`podbard init` コマンドを使わず、以下のテンプレートリポジトリを使うこともできます。これらは、GitHub Actionsの雛形も含まれているので便利です。

- <https://github.com/Songmu/podbard-starter>
    - GitHub Pages
- <https://github.com/Songmu/podbard-cloudflare-starter>
    - Cloudflare Pages + R2
- <https://github.com/Songmu/podbard-private-podcast-starter>
    - Cloudflare Pages + R2 (Private Podcast)

### 2. 設定ファイル
`podbard.yaml` を開いて適宜調整してください。`artwork`にはダミーの画像が指定されているので、それは適切な画像に差し替えてください。正方形で1400×1400px以上のJPEGまたはPNGファイルを指定してください。

### 3. 音声配置
`audio/` ディレクトリにオーディオファイルを配置します。ファイル形式は、MP3またはM4Aをサポートしています。

### 4. エピソードファイル作成
4で配置したオーディオに対応するエピソードのMarkdownファイルを作成します。例えば、`podbard episode audio/1.mp3` で1.mp3に対応するエピソードのMarkdownを生成します。エピソードファイルは、`episode/` ディレクトリに保存され、この場合は `episode/1.md` に保存されます。Markdown内には、エピソードのタイトルや説明、公開日時などの必要最低限の情報に加え、本文にShow Noteを記述できます。

### 5. サイトのビルド
サイトのビルドは `podbard build` コマンドで行います。ビルドされたファイルは `public/` ディレクトリに出力されます。このディレクトリを適切なホスティング環境にdeployすることで、ポッドキャストサイトが完成します。

## まとめ
podbardは、`audio/` ディレクトリに配置された音声ファイルから簡単にポッドキャストサイトを作成することができるツールです。ここでは最低限の使い方をざっと説明しましたが、詳細な使い方や設定方法については次回以降に解説していきます。
