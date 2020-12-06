# household accounts app

ログイン認証機能を持った家計簿アプリです。

スマホサイズにも対応しています。

## デモ

デモ動画です。

![vueApp-demoGIF](https://user-images.githubusercontent.com/66013439/100846756-402e2d80-34c2-11eb-85a2-87c222e66ecd.gif)

## 特徴

全5ページで構成されています。

* 新規登録ページでは、メールアドレスと6文字以上のパスワードを入力することで、新しいアカウントをfirebase authenticationに保存することができます。その際cloud firestore のusersコレクションにユーザーのuidと同名のドキュメントを作成し、その中のフィールドにユーザーのemailアドレスとパスワードを保存しています。

* ログインページでは、firebase authentication に保存してあるユーザー情報と入力したユーザー情報を照らし合わせて、該当するユーザーがいればアプリケーションにログインできるような仕組みにしています。
ログインに成功すれば、vuexにユーザーのuidを保存し、cloud firestore からそのuidと一致したドキュメントにあるpostDataというサブコレクション内のドキュメントデータを取得してvuexに保存します。

※postDataはフロント側で初めて支出額の入力が行われた時に作成されます。

* 入力ページでは入力したデータをcloud firestoreにある、ユーザーのuidと一致したドキュメント内のpostDataサブコレクションに保存します。

* カレンダーページではユーザーの保存した支出額などのデータをcloud firestoreから取得し、データの一覧・追加・削除が可能です。

* レポートページではcloud firestore から取得してきたデータをjavascriptライブラリのchartkickを用いて円グラフにしています。
また、データを計算してカテゴリー別の割合を表示しています。

以下はcloud firestoreの内部構造です。

<img width="567" alt="firestore_image" src="https://user-images.githubusercontent.com/66013439/101278871-ab00a100-3801-11eb-8161-093f5a125f1b.png">

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
ログイン後は、「ログアウト」ボタンが表示されるので、そちらをクリックしてログアウトすることができます。

* ### 新規登録ページ
新しいアカウントを作る場合は、新規登録ページでEmailアドレスと6文字以上の英数字でパスワードを入力して、新規登録してください。

* ### 入力ページ
日付、カテゴリー、支出額、メモなどを入力して「記録する」ボタンを押すことで、入力したデータを保存します。

* ### カレンダーページ
カレンダーに、入力したデータの一覧が表示されます。カレンダーの日付をタップすることでモーダルが出現し、データの追加を行うことができます。
また、カレンダーの「<<」、「>>」や、「today」、「次の月」、「前の月」をクリックすることで、表示するカレンダーの月を変えられます。
さらに、カレンダーページ下部にその月の内訳が一覧で出ます。各ブロックの[x]ボタンをクリックすることで、データの削除ができます。

* ### レポートページ
カテゴリーごとに、その月の総支出額に対する割合が%表示されます。
また、円グラフで一括して確認することもできます。


## メモ

カテゴリーの種類を追加する機能や、入力したデータを更新する機能はありません。

## 作成者情報

* 只浦三四郎
* sanshirou1110_0508@yahoo.co.jp

## ライセンス
MITライセンス

→ LICENSE.txt
