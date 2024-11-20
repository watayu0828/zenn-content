---
title: "Expo CLIインストール時のPermission deniedエラーの解決方法"
emoji: "💡"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [reactnative, expo]
published: true
---

## エラー文

```bash
npm error code EACCES
npm error syscall mkdir
npm error path /usr/local/lib/node_modules/eas-cli
npm error errno -13
npm error Error: EACCES: permission denied, mkdir '/usr/local/lib/node_modules/eas-cli'
npm error     at async mkdir (node:internal/fs/promises:858:10)
npm error     at async /usr/local/lib/node_modules/npm/node_modules/@npmcli/arborist/lib/arborist/reify.js:624:20
npm error     at async Promise.allSettled (index 0)
npm error     at async [reifyPackages] (/usr/local/lib/node_modules/npm/node_modules/@npmcli/arborist/lib/arborist/reify.js:325:11)
npm error     at async Arborist.reify (/usr/local/lib/node_modules/npm/node_modules/@npmcli/arborist/lib/arborist/reify.js:142:5)
npm error     at async Install.exec (/usr/local/lib/node_modules/npm/lib/commands/install.js:150:5)
npm error     at async Npm.exec (/usr/local/lib/node_modules/npm/lib/npm.js:207:9)
npm error     at async module.exports (/usr/local/lib/node_modules/npm/lib/cli/entry.js:74:5) {
npm error   errno: -13,
npm error   code: 'EACCES',
npm error   syscall: 'mkdir',
npm error   path: '/usr/local/lib/node_modules/eas-cli'
npm error }
npm error
npm error The operation was rejected by your operating system.
npm error It is likely you do not have the permissions to access this file as the current user
npm error
npm error If you believe this might be a permissions issue, please double-check the
npm error permissions of the file and its containing directories, or try running
npm error the command again as root/Administrator.
npm error A complete log of this run can be found in: /Users/ユーザー名/.npm/_logs/2024-11-20T10_14_44_933Z-debug-0.log
```

## 解決方法

以下のコマンドを実行してアクセス権を付与する。

```bash
sudo chown -R $(whoami) $(npm config get prefix)/{lib/node_modules,bin,share}
```

再度インストールコマンドを実行すると正常にインストールされる。
