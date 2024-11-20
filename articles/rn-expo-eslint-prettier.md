---
title: "React Native（Expo）用にESLint、Prettier初期設定する"
emoji: "💻️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [reactnative, expo, eslint, prettier]
published: true
---

## ESLint

### インストール

VSCode の拡張機能をインストールする。

https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint

### 初期設定

```bash
npx expo lint
```

### 質問に回答

```bash
npx eslint --init
You can also run this command directly using 'npm init @eslint/config@latest'.
Need to install the following packages:
@eslint/create-config@1.4.0
Ok to proceed? (y) y

> rss-reader-app@1.0.0 npx
> create-config

@eslint/create-config: v1.4.0

✔ How would you like to use ESLint? · problems
✔ What type of modules does your project use? · commonjs
✔ Which framework does your project use? · react
✔ Does your project use TypeScript? · typescript
✔ Where does your code run? · browser
The config that you've selected requires the following dependencies:

eslint, globals, @eslint/js, typescript-eslint, eslint-plugin-react
✔ Would you like to install them now? · No / Yes
✔ Which package manager do you want to use? · npm
```

初期設定が完了すると、`.eslintrc.js` が生成される。

## Prettier

### インストール

```bash
npx expo install -- --save-dev prettier eslint-config-prettier eslint-plugin-prettier
```

### **.eslintrc.js を更新**

```jsx
module.exports = {
  extends: ["expo", "prettier"],
  plugins: ["prettier"],
  rules: {
    "prettier/prettier": "error",
  },
};
```

これで、`npx expo lint` を実行すると、Prettier の設定に準拠していない場合にエラーを検出するようになる。

### .prettierrc を更新

Prettier の設定を変更したい場合は、`.prettierrc` ファイルをプロジェクトのルートディレクトリに作成し、編集する。

```json
{
  "printWidth": 100,
  "tabWidth": 2,
  "singleQuote": true,
  "bracketSameLine": true
}
```

## ファイルを保存した時にフォーマットされるようにする

VSCode の `setting.json` に下記を追加する。

```json
{
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": "explicit"
  }
}
```
