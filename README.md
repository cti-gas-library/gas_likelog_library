# GAS LikeLog Library

## 目的

iframe に埋め込めるいいね機能をスプレッドシートをデータソースにして実装できるライブラリ

## 導入手順

### スプレッドシート作成

- スプレッドシートに sheetName で指定したシートを作成
- 先頭行に各 ColumnName 入力

### スクリプト作成

- 拡張機能から AppScript を開く
- ライブラリから以下のスクリプト ID を検索しインポート
- スクリプト ID
  ```
  10vTUuQfTCuXRvZVzCxjCzFFqWIMCdDx6sDsuODgZ4vjVV5Q1xCqTagz8
  ```
- コードに以下のコードをコピー

  ```javascript:GASコード
  const likelog = () => {
    return LikeLogLibrary.create({
      sheetName: "タグ別",
      tagColumnName: "tag",
      likeColumnName: "like"
    });
  }

  const getLikeCount = (tag) => {
    return likelog().getLikeCount(tag);
  }

  const addLikeCount = (tag) => {
    return likelog().addLikeCount(tag);
  }

  const doGet = (e) => {
    return likelog().hookHandler(e);
  };
  ```

### スクリプトの公開設定

- スクリプトをデプロイしてウェブアプリとして公開

### ウェブアプリを外部サービスで表示

- デプロイ画面でコピーできるウェブアプリの URL を任意の iframe で表示する。
  ```html
  <iframe src="{ウェブアプリURL}" heigth="100%" width="100%" sandbox frameborder="no" loading="lazy"></iframe>
  ```
- 必要に応じて URL パラメータに tag をつけると複数設定することもできます！

  ```
  {ウェブアプリURL}?tag=tag_name
  ```

### 注意事項

- 自分のアカウントで実行を選択していない場合は初回に権限付与用のダイアログが表示されます。また、ウェブアプリの公開範囲を変更すれば、社内向け、個人用など閲覧者を制限することもできます。

## 開発方法

詳細は[Document](https://developers.google.com/apps-script/guides/clasp)を参照

[clasp を使って Google Apps Script の開発環境を構築してみた | DevelopersIO](https://dev.classmethod.jp/articles/vscode-clasp-setting/)  
[GAS を git 管理したいので、Clasp 環境を作る](https://zenn.dev/marusho/scraps/3579309aabf5eb)

### ログイン

```
clasp login
```

### 既存スクリプトを clone する

```
clasp clone {scriptId}
```

### GAS を開く

```
clasp open
```

### スクリプトを push する

```
clasp push
```

### スクリプトを pull する

```
clasp pull
```

### 状況確認

#### バージョン一覧

```
clasp versions
```

#### デプロイ一覧

```
clasp deployments
```

### 更新処理

#### 新規バージョン発行

```
clasp version "new version"
```
