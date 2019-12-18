# 地図データを反映したアプリの実行

このドキュメントでは、[地図データの作成](#)で作成したWeb マップをサンプルコードに適用して実行する設定を行います。

1.  [ログイン機能を利用するための設定](#1-ログイン機能を利用するための設定)
    - 1_1. [アプリを登録し、クライアント ID を入手する](#1_1-アプリを登録しクライアント-id-を入手する)
    - 1_2. [リダイレクト URL を設定する](#1_2-リダイレクト-url-を設定する)
1.  [アプリで利用する情報](#2-アプリで利用する情報)
1.  [Configration.xml を設定してアプリからデータを参照できるようにする](#3-configrationxml-を設定してアプリから-web-マップを参照できるようにする)

アプリには ArcGIS にログインするための機能が実装済みです。<br>
この機能を有効にするための設定から行います。このログイン機能とは、ArcGIS にログインするための機能です。公開範囲が限られたセキュアなデータにアクセスする場合や、オフライン時に背景地図を任意の範囲で切り出す操作を行う場合に、認証を行うことで利用できるようになります。

## 1. ログイン機能を利用するための設定

ArcGIS for Developers で「アプリの登録」を行い、ログイン機能を利用できるようにします。

アプリの登録は、ArcGIS for Developers のダッシュボード画面から行います。</br>
手順は、アイテム詳細画面の「App Launcher」から「Developers」のアイコンを選択し、「New Application」ボタンを選択します。または、ArcGIS for Developers のダッシュボード画面から「New Application」のボタンを選択します。

![アイテム詳細画面からダッシュボード、登録画面](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_devLauncher.gif)
アイテム詳細画面からアプリの登録画面表示までの手順

### 1_1. アプリを登録し、クライアント ID を入手する

「New Application」のページでは、次の 3 つを入力し[Register New Application]を選択します。</br>
アプリの登録を完了し、クラアイント ID を取得します。

* title：DataCollecton
* tag：test
* Description：データコレクションアプリ

※Description 以外は半角英数字で入力します

![入力から登録ボタン選択、アプリ登録完了](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_registration.gif)


### 1_2. リダイレクト URL を設定する

アプリの登録完了の画面から、[Authentication]タブを選択して、[Redirect URIs]の項目に以下を入力し、[Add]を選択します。

`DataCollection://oauth`

![リダイレクトURLの登録](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_redirectUrl.gif)

緑のチェックが表示されれば、利用可能な URL として登録ができます。

***注意***</br>
ブラウザの翻訳機能は使用しない状態の画面で URL の登録を行ってください。

## 2. アプリで利用する情報

アプリでは、登録した内容からクライアント ID およびリダイレクト URL を使用します。

例：
* クライアントID（Client ID）：g0biHDu8TD2G8XXX
* リダイレクトURL（Current Redirect URIs）：DataCollection://oauth

![リダイレクトURLの登録](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_credentialInf.png)

## 3. Configration.xml を設定してアプリから Web マップを参照する

`Configration.xml` ファイルには、参照する Web マップと ArcGIS と認証情報を行うための情報を設定します。</br>

作成したクライアント ID、リダイレクト URL、Web マップの URL をアプリに設定します。
**DataCollection.sln** を Visual Studio 2017 で開きます。

![リダイレクトURLの登録](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_startSln.gif)

'Configration.xml'を開きます。次の XML タグにクライアント ID 等を設定します。

* \<WebmapURL> Web マップの URL \</WebmapURL>
* \<AppClientID> クライアント ID \</AppClientID>
* \<RedirectURL> リダイレクト URL \</RedirectURL>

<div align="center">
 <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_settingInfo.png" width="800px">
</div>

設定が完了したら、必ずビルドを行います。実行後 ログインの認証画面が表示された場合は、開発者アカウントのユーザー ID とパスワードを入力します。

<div align="center">
 <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_startupApp.png" width="800px">
</div>


[手順一覧のページ](./How2SetupApp_gaiyo.md#ハンズオンの手順)に戻る
