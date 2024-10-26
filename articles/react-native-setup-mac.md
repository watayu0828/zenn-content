---
title: "MacにReactNativeの開発環境を構築する"
emoji: "💻️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [reactnative, mac]
published: true
---

## Homebrew のインストール

### 1. Homebrew の公式サイトに飛び、インストール用のコマンドをコピーする

https://brew.sh/ja/

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### 2. コピーしたコマンドをターミナルに貼り付けて実行する

### 3. パスワードを聞かれるので入力して続行

### 4. **`==> Installation successful!` が表示されたらインストール完了**

### 5. パスを通すため、上記完了時に表示される `==> Next steps:` に従って、コマンドを実行する

```bash
==> Next steps:
- Run these commands in your terminal to add Homebrew to your PATH:
    echo >> /Users/<<Macのユーザー名>>/.zprofile
    echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/<<Macのユーザー名>>/.zprofile
    eval "$(/opt/homebrew/bin/brew shellenv)"
- Run brew help to get started
- Further documentation:
    https://docs.brew.sh

```

### 6. ターミナルに `brew help` と打って、ヘルプが表示されればインストール完了

## Node.js のインストール

```bash
brew install node
```

Homebrew を使わない場合は、[Node.js 公式サイト](https://nodejs.org/en/)から LTS 版をインストールする。

## Watchman のインストール

```bash
brew install watchman
```

## Xcode のインストール

```bash
xcode-select --install
```

## Ruby のインストール

```bash
brew install ruby
```

### PATH を通す

```bash
export PATH="/opt/homebrew/opt/ruby/bin:$PATH"
```

### 新規のターミナルを開いてバージョンを確認する

```bash
ruby -v
```

## CocoaPods のインストール

```bash
sudo gem install cocoapods
```

```bash
pod –version
```

## React Native CLI のインストール

React Native CLI は、React Native アプリケーションを作成するためのコマンドラインインターフェース（CLI）。React Native アプリの作成、ビルド、テスト、デプロイに使用できる。

React Native CLI は、React Native 開発に必要な開発ツールをインストールするために使用される npm パッケージ。

```bash
npm install -g react-native-cli
```

インストールが終わったら、次のコマンドを実行してインストールがうまくいったか確認する。

```bash
react-native --version
```

```
react-native-cli: 2.0.1
react-native: n/a - not inside a React Native project directory
```
