---
title: "Google Apps Script のローカル開発環境を構築する"
emoji: "💻️"
type: "tech"
topics: [gas, clasp, googleappsscript, typescript]
published: true
---

## 概要

Google Apps Script（以下、GAS）をローカルで開発するための環境構築手順を説明します。

ローカル環境を構築することで、VSCode などのエディタでコードを書くことができ、Git でバージョン管理も可能になります。

## 前提条件

この記事では、Node.js および npm がすでにインストールされていることを前提とします。

## 1. clasp のインストール

npm を使って `clasp` をグローバルにインストールします。

```bash
npm install -g @google/clasp
```

インストールが完了したら、以下のコマンドで `clasp` のバージョンを確認できます。

```bash
clasp -v
```

## 2. Google Apps Script API の有効化

`clasp` を使用するには、Google Apps Script API を有効にする必要があります。

以下のリンクにアクセスし、GAS API を有効にしてください。

[https://script.google.com/home/usersettings](https://script.google.com/home/usersettings)

「Google Apps Script API」の項目をオンに切り替えます。

## 3. Google アカウントへのログイン

ローカル環境から GAS プロジェクトを操作するために、Google アカウントで `clasp` にログインします。

```bash
clasp login
```

このコマンドを実行するとブラウザが開き、Google アカウントの選択と `clasp` への権限の許可を求められます。

許可すると、認証情報がローカルに保存されます。

## 4. プロジェクトの作成またはクローン

### 新規プロジェクトを作成する場合

新しい GAS プロジェクトを作成するには、作業したいディレクトリで以下のコマンドを実行します。

```bash
clasp create --title "MyProject" --type standalone
```

`--title` でプロジェクト名を指定します。
`--type` オプションで、`standalone`, `sheets`, `docs`, `forms` などのプロジェクトタイプを指定することもできます。

コマンドを実行すると、カレントディレクトリに `.clasp.json` と `appsscript.json` の 2 つのファイルが作成されます。

### 既存のプロジェクトをクローンする場合

すでに存在する GAS プロジェクトをローカルにコピー（クローン）することもできます。

GAS エディタの「プロジェクトの設定」画面でスクリプト ID を確認してください。

スクリプト ID を使って、以下のコマンドを実行します。

```bash
clasp clone <スクリプトID>
```

## 5. プロジェクトのディレクトリ構成

TypeScript で開発する場合、ソースコード (`src`) とコンパイル後の JavaScript (`dist`) を分離するのが一般的です。

### ディレクトリの作成

`clasp create` を実行した後、以下のコマンドでディレクトリを作成し、`appsscript.json` を移動します。

```bash
mkdir src
mkdir dist
mv appsscript.json dist/appsscript.json
```

### .clasp.json の編集

`clasp` が `dist` フォルダ内のコンパイル済み JavaScript を参照するように、`.clasp.json` ファイルを編集して `rootDir` プロパティを追加します。

```json
{
  "scriptId": "YOUR_SCRIPT_ID",
  "rootDir": "dist"
}
```

### .gitignore の作成

Git を使用する場合、`node_modules` フォルダや `dist` フォルダ、`.clasp.json` を無視するために `.gitignore` ファイルを作成します。

```gitignore
node_modules/
dist/
.clasp.json
```

## 6. TypeScript と ESLint の環境構築

TypeScript で開発し、ESLint でコード品質を保つための環境を整えます。

### npm の初期化と依存パッケージのインストール

プロジェクトディレクトリで npm を初期化し、必要なパッケージをインストールします。

```bash
npm init -y
npm i -D typescript @types/google-apps-script @types/node
npm i -D eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin eslint-config-prettier prettier
```

### tsconfig.json の作成

TypeScript の設定ファイル `tsconfig.json` をプロジェクトルートに作成します。

```json
{
  "compilerOptions": {
    "target": "ES2019",
    "lib": ["es2019"],
    "types": ["google-apps-script"],
    "module": "CommonJS",
    "moduleResolution": "node",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "rootDir": "./src",
    "outDir": "./dist"
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

### .eslintrc.json の作成

ESLint の設定ファイル `.eslintrc.json` をプロジェクトルートに作成します。

```json
{
  "root": true,
  "parser": "@typescript-eslint/parser",
  "plugins": ["@typescript-eslint/eslint-plugin"],
  "extends": ["eslint:recommended", "plugin:@typescript-eslint/recommended", "prettier"],
  "env": {
    "node": true
  },
  "ignorePatterns": ["dist", "node_modules"]
}
```

### package.json にスクリプトを追加

`package.json` ファイルの `"scripts"` に以下のコマンドを追加すると、開発が便利になります。

```json
"scripts": {
  "build": "tsc",
  "push": "npm run build && clasp push",
  "lint": "eslint 'src/**/*.ts'",
  "lint:fix": "eslint 'src/**/*.ts' --fix"
}
```

## 7. コードの編集

`src` フォルダ内に `ts` ファイルを作成してコードを記述します。

```typescript
function myFunction() {
  Logger.log("Hello, World!");
}
```

## 8. コードのコンパイルとアップロード

ローカルで編集した `ts` ファイルを GAS プロジェクトに反映させるには、まずコンパイルを行い、次にプッシュします。

### 1. コンパイル（TypeScript -> JavaScript）

```bash
npx tsc
```

（または`package.json` に `build` を追加した場合は `npm run build` を実行する）

このコマンドにより、`src` フォルダ内の TypeScript ファイルが `dist` フォルダに JavaScript ファイルとして出力されます。

### 2. アップロード（JavaScript -> GAS）

```bash
clasp push
```

（または`package.json` に `push` を追加した場合は `npm run push` を実行する）

`clasp push` は `.clasp.json` の `rootDir` に基づいて `dist` フォルダ内のファイルを GAS プロジェクトにアップロードします。

## GAS エディタで編集した内容を取得する場合

GAS エディタで直接編集した内容をローカルに反映させるには、以下のコマンドを実行します。

```bash
clasp pull
```

これにより、GAS プロジェクトの最新のコードがローカルにダウンロードされます。
