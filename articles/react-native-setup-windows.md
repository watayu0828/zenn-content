---
title: "WindowsにReactNativeの開発環境を構築する"
emoji: "💻️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [reactnative, windows]
published: true
---

## Chocolatey のインストール

Chocolatey は、Windows 向けのパッケージマネージャー。

ソフトウェアの依存関係を含め、簡単にソフトウェアのインストール・アップデートをすることができる。

[Chocolatey - The package manager for Windows](https://chocolatey.org/)

次のコマンドをコマンドプロンプト（管理者権限）で実行する。

```bash
@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
```

インストールが終わったら、コマンドプロンプトを再起動して、インストールがうまくいったか確認する。

```bash
choco -v
```

```
2.0.0
```

## Node.js のインストール

Node.js は、V8 JavaScript エンジンをベースとした JavaScript ランタイム環境。

Node.js は、サーバーサイドでの JavaScript 実行に特化しており、非同期 I/O 処理をサポートしている。また、npm(Node Package Manager)というパッケージマネージャーを含んでおり、多くのライブラリやフレームワークが利用できる。

[Node.js](https://nodejs.org/en)

次のコマンドをコマンドプロンプト（管理者権限）で実行する。

```bash
choco install -y nodejs-lts
```

インストールが終わったら、コマンドプロンプトを再起動してインストールがうまくいったか確認する。

```bash
node --version
```

```
v18.16.1
```

npm もインストールされたか確認するために次のコマンドを実行する。

```bash
npm --version
```

```
9.5.1
```

## Python のインストール

React Native のビルドシステムは Python を使っている。

Python は、AI やアプリ開発などに用いられている高水準インタプリタ型汎用プログラミング言語。Web アプリケーション、データ分析、人工知能、機械学習などの分野で広く使用されている。

次のコマンドをコマンドプロンプト（管理者権限）で実行する。

```bash
choco install -y python
```

インストールが終わったら、コマンドプロンプトを再起動してインストールがうまくいったか確認する。

```bash
python --version
```

```
Python 3.11.4
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

## JDK のインストール

Reeact Native で Android アプリを開発する場合は JDK（Java Development Kit）が必要になる。

次のコマンドをコマンドプロンプト（管理者権限）で実行する。

```bash
choco install -y microsoft-openjdk11
```

インストールが終わったら、コマンドプロンプトを再起動してインストールがうまくいったか確認する。

```bash
java -version
```

```
openjdk version "11.0.18" 2023-01-17 LTS
OpenJDK Runtime Environment Microsoft-7208460 (build 11.0.18+10-LTS)
OpenJDK 64-Bit Server VM Microsoft-7208460 (build 11.0.18+10-LTS, mixed mode)
```

## Android Studio のインストールとセットアップ

### Android Studio のインストール手順

1. 公式ページから Android Studio をダウンロード

   [Android Studio 公式](https://developer.android.com/studio)

2. インストーラーを起動後「Next」を押下して次の画面に進む
3. 「Android Virtual Device」にチェックを入れ、次の画面に進む
4. Android Studio のインストールを指定し、次の画面に進む
5. スタートメニューを設定する画面が出るので、「Install」を押してインストールを開始する
6. インストール完了後、「Start Android Studio」にチェックが入っていることを確認して「Finish」を押す

### Android Studio のセットアップ

1. 初回起動時、セットアップウィザードが表示されるので「Custom」を選択して次に進む
2. UI テーマをお好みで選択する
3. SDK コンポーネントのセットアップ画面が表示されるので、「Performance (Intel ® HAXM)と Android Virtual Device」の項目にチェックを入れ次に進み、セットアップを完了させる

### Android SDK のインストール

1. Android Studio のホーム画面右下の「Configure」から「SDK Manager」を選択する
2. 「SDK Platforms」タブ画面右下の「Show Package Details」にチェックを入れる
3. 次の内容を選択する
   - Android SDK Platform 34
   - Intel x86 Atom_64 System Image または Google APIs Intel x86 Atom System Image
4. 「SDK Tools」タブ画面右下の「Show Package Details」にチェックを入れる
5. 「Android SDK Build-Tools」を展開し、「33.0.0」にチェックを入れる
6. 最後に「Apply」を押してインストールを開始する

### Android Studio の環境変数設定

React Native は、ネイティブコードでアプリを構築するために環境変数を設定する必要がある。

1. Windows のスタートメニューを右クリックし、「システム」を選択する
2. 画面右の関連設定にある「システム詳細設定」を開く
3. 「詳細設定」タブの「環境変数」を押下する
4. ユーザー環境変数の「新規」を押下する
5. 変数名と変数値を次のように入力して登録する

   変数名：ANDROID_HOME

   変数値：Android SDK へのパス　例）C:\Users\<ユーザー名>\AppData\Local\Android\Sdk

6. 変数「Path」の編集画面を開き、platform-tools へのパスをリストに追加する

   例）C:\Users\<ユーザー名>\AppData\Local\Android\Sdk\platform-tools

7. 上記が完了したら、コマンドプロンプトを開き次のコマンドを実行する

   ```bash
   adb
   ```

   環境変数設定がうまくいっていれば、次のような結果が表示される。

   ```
   Android Debug Bridge version 1.0.41
   Version 30.0.3-6597393
   Installed as C:\Users\<ユーザー名>\AppData\Local\Android\Sdk\platform-tools\adb.exe
   ```

## プロジェクトの作成

コマンドプロンプトを管理者権限で開き、プロジェクトを作成したいパスまで移動して次のコマンドを実行する。

```bash
npx react-native init [プロジェクト名]
```

「Run instruction」が表示されれば作成完了。

「TypeError: cli.init is not a function for react native」と出た場合は、バージョンを指定して実行する。

```bash
npx react-native init [プロジェクト名] --version 0.68.2
```

## 仮想デバイスの作成

1. Android Studio のホーム画面右下の「Configure」から「AVD Manager」を選択する
2. 「Create Virtual Device」からデバイスを押下する
3. 任意のデバイスを選択し次の画面に進む
4. 「x86 Images」タブの Target が「Android API 33 (Google APIs)」のものを選択し次の画面へ進む
5. 「Finish」を押下で完了

## React Native アプリケーションを実行する

1. コマンドプロンプトを管理者権限で開き、作成したプロジェクトのディレクトリに移動する
2. 次のコマンドを実行し、Metro を開始する

   ```bash
   npx react-native start
   ```

3. 新しくコマンドプロンプトを管理者権限で開き、作成したプロジェクトのディレクトリに移動する
4. 次のコマンドを実行しアプリケーションを開始する

   ```bash
   npx react-native run-android
   ```

すべてが正しく設定されていると、Android エミュレータが起動する。
