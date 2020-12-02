# household accounts app

ログイン認証機能を持った家計簿アプリです。

スマホサイズにも対応しています。

## デモ

デモ動画です。

![vueApp-demoGIF](https://user-images.githubusercontent.com/66013439/100846756-402e2d80-34c2-11eb-85a2-87c222e66ecd.gif)

## 特徴

全5ページで構成されています。

ログインページではユーザーの認証機能があります。

新規登録ページではユーザー情報の保存機能があります。

入力ページでは、支出額などのデータを保存する機能があります。

カレンダーページでは、保存したデータの一覧・追加・削除機能があります。

レポートページでは、カテゴリーごとに月の支出額に対する割合を表示します。

## 必要条件

Node.js 12.18.3

## インストール

下記リンクよりNode.jsをインストールできます。

<https://nodejs.org/en/>

## 使い方

下記リンクより実際にこちらのアプリケーションを試すことができます。

<https://householdaccounts-vueapp.web.app/#/>

* ### ログインページ
ページ中央にテスト用のEmailアドレスとパスワードがありますので、よろしければご活用ください。

* ### 新規登録ページ
新しいアカウントを作る場合は、新規登録ページでEmailアドレスとパスワードを入力して、新規登録してください。
「ログアウト」ボタンをクリックしてログアウトすることができます。

* ### 入力ページ
日付、カテゴリー、支出額、メモなどを入力して「記録する」ボタンを押すことで、入力したデータを保存します。

* ### カレンダーページ
カレンダーに、入力したデータの一覧が表示されます。カレンダーの日付をタップすることでモーダルが出現し、データの追加を行うことができます。
また、カレンダーの「<<」、「>>」や、「today」、「次の月」、「前の月」をクリックすることで、表示するカレンダーの月を変えられます。
さらに、カレンダーページ下部にその月の内訳が一覧で出ます。各ブロックの[x]ボタンをクリックすることで、データの削除ができます。

* ### レポートページ
カテゴリーごとに、その月の総支出額に対する割合が%表示されます。
また、円グラフで確認することもできます。


## メモ

カテゴリーの種類を追加する機能や、入力したデータを更新する機能はありません。

## 作成者情報

* 只浦三四郎
* sanshirou1110_0508@yahoo.co.jp

## ライセンス
MITライセンス

→ LICENSE.txt
