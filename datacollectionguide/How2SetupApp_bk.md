# Data Collection for .NET アプリの設定と起動

<div align="center">
 <img src="https://developers.arcgis.com/example-apps/data-collection-dotnet/img/featured-img.png" width="500px">
</div>

</br>

# 概要


このドキュメントは、ArcGIS プラットフォームを使用して、現地調査に活用できるサンプルアプリケーション（以下、アプリ）を起動するまでの手順を示しています。

2019年8月に開催した [ArcGIS 開発者のための最新アプリ開発塾 2019](https://github.com/EsriJapan/workshops/tree/master/20190823_app-development-hands-on) セミナーでは、[ArcGIS プラットフォームを活用した調査アプリケーション構築までのハンズオン](https://github.com/EsriJapan/workshops/blob/master/20190823_app-development-hands-on/02_ArcGIS_%E3%83%97%E3%83%A9%E3%83%83%E3%83%88%E3%83%95%E3%82%A9%E3%83%BC%E3%83%A0%E3%82%92%E6%B4%BB%E7%94%A8%E3%81%97%E3%81%9F%E8%AA%BF%E6%9F%BB%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E6%A7%8B%E7%AF%89%E3%81%BE%E3%81%A7%E3%81%AE%E3%83%8F%E3%83%B3%E3%82%BA%E3%82%AA%E3%83%B3.pdf) のセクションで、このドキュメントの内容を実施しました。</br>
また、アプリを構築する目的として、**街路樹診断の現地調査を行う** というシナリオを想定し、オフライン（インターネットが繋がらない）状態でも利用できるアプリを構築しました。

アプリは、米国Esri社が公開する [Data Collection for .NET](https://developers.arcgis.com/example-apps/data-collection-dotnet/) を元に、ESRIジャパンにてローカライズしています。

ハンズオンでは、ローカライズしたプロジェクトをダウンロードいただき、このプロジェクトについて Visual Studio 2017（統合開発環境）を使用してビルドし、ご自身で作成・設定した地図データ（Web マップ）を適用してアプリを起動しました。</br>
以下では再現するための手順を gif を交えてご紹介しています。

**ハンズオンで使用するもの**

このハンズオンで使用するものは次の4つです

* ArcGIS for Developers（開発者アカウント）
* Visual Studio 2017
* ローカライズ済みのサンプルプロジェクト
* ダミーデータ

ローカライズ済みのサンプルプロジェクト及びダミーデータは [HandsOn_Data.zip](https://github.com/EsriJapan/workshops/raw/master/20190823_app-development-hands-on/HandsOn_Data.zip) からダウンロードできます。</br>
HandsOn_Data.zip を解凍すると以下の構成となっています。

| HandsOn_Data フォルダ配下 | 格納ファイルまたはプロジェクト | 備考 |
|---|---|---|
| 02_Data_Collection_Application | 190823_dev_school.ipynb | ここでは使用しません  |
|  | tree_inspection.gdb.zip | **使用します：ダミーデータ**  |
|  | data-collection-dotnet-master_ejLocalized | **使用します：ローカライズ済みのサンプルプロジェクト**  |
| 03_Widget_Development  | 190823_dev_school.ipynb  | ここでは使用しません  |

**その他参考ソース**

* 米国Esri社が公開する、[Data Collection for .NET](https://developers.arcgis.com/example-apps/data-collection-dotnet/) のページおよび [GitHub ソース](https://github.com/Esri/data-collection-dotnet)についてもぜひご参照ください。
*[ハンズオン時に使用した資料（PPT）](https://github.com/EsriJapan/workshops/blob/master/20190823_app-development-hands-on/02_ArcGIS_%E3%83%97%E3%83%A9%E3%83%83%E3%83%88%E3%83%95%E3%82%A9%E3%83%BC%E3%83%A0%E3%82%92%E6%B4%BB%E7%94%A8%E3%81%97%E3%81%9F%E8%AA%BF%E6%9F%BB%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E6%A7%8B%E7%AF%89%E3%81%BE%E3%81%A7%E3%81%AE%E3%83%8F%E3%83%B3%E3%82%BA%E3%82%AA%E3%83%B3.pdf)もご覧いただけます。

*ハンズオンで使用したアプリの機能拡張した内容について、以下で別途ご紹介しています。手順以外にアプリについてｘｘｘｘ

 * [その他のアプリに関する補足事項](#その他のアプリに関する補足事項)
  　  * [アプリの仕様について](#アプリの仕様について)
     * [データについて](#データについて)
     * [機能拡張などの開発について](#機能拡張などの開発について)


# 手順

アプリを起動するために、大きく分けて次の 2 つのステップを行います。

1.[地図データの準備](#1地図データの準備)  
2.[アプリの機能追加と設定](#2-アプリの機能追加と設定)

----
# 1.　地図データの準備

アプリで利用する地図データ（Web マップ）を作成します。</br>
作成する Web マップの構成は次のようになります。

<div align="center">
 <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_webmap.png" width="400px">
</div>

Web マップは以下の手順で作成します。</br>

1. [ホスト フィーチャ レイヤーを作成する](#1-ホスト-フィーチャ-レイヤーを作成する)
    - 1_1.  [ファイル ジオデータベースからホスト フィーチャ レイヤーを作成する](#1_1-ファイル-ジオデータベースからホスト-フィーチャ-レイヤーを作成する)
    - 1_2.  [アプリで利用するための設定を適用する](#1_2-アプリで利用するための設定を適用する)
        - 1_2_1. [添付ファイルを有効化するための設定](#1_2_1-添付ファイルを有効化するための設定)
        - 1_2_2. [オフラインで使用するための設定](#1_2_2-オフラインで使用するための設定)
        - 1_2_3. [ドメインの設定](#1_2_3-ドメインの設定)
        - 1_2_4. [シンボルの設定](#1_2_4-シンボルの設定)
1. [Web マップを作成する](#2-web-マップを作成する)
    - 2_1. [レイヤー順序を変更する](#2_1-レイヤー順序を変更する)
    - 2_2. [Web マップを保存する](#2_2-web-マップを保存する)
    - 2_3. [オフラインで使用するための設定を行う](#2_3-オフラインで使用するための設定を行う)
1. [アプリで使用するURL](#3-アプリで使用する-url)

------

## 1. ホスト フィーチャ レイヤーを作成する

### 1_1. ファイル ジオデータベースからホスト フィーチャ レイヤーを作成する

***ArcGIS for Developers へログイン***

[ArcGIS for Developers](https://developers.arcgis.com/) へログインします。開発者のためのダッシュボードが表示されるので、[Manage Content]ボタンから、ArcGIS Online のアイテム一覧画面を開きます。

![ArcGIS for Developers からログイン、アイテム一覧ページまで](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_login.gif)
※言語表示が英語の方は [ArcGIS Online 逆引きガイド](https://www.esrij.com/cgi-bin/wp/wp-content/uploads/documents/ArcGISOnline_user_guide.pdf)の ”1-1. ArcGIS Onlineへサインイン” に記載されている ”マイ プロフィールの設定” の項目を参考に日本語に設定してください。


以下の画面がアイテム一覧ページです。

<div align="center">
 <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_itemlist.png" width="400px">
</div>

**ホスト フィーチャ レイヤーの作成**

アイテム一覧ページ画面左上の[アイテムの追加]ボタンより、[コンピューター上]を選択します。</br>
コンピューターからアイテムを追加のポップアップが表示されますので、[ファイルを選択]より **tree_inspection.gdb.zip** を選択します。</br>
次の 2 つを指定または入力し[アイテムの追加]ボタンを選択します。

* コンテンツ：ファイル ジオデータべース
* タグ：テスト(任意)

その他の設定項目はデフォルトのままで構いません。

![アイテム指定からサービス作成中の画面まで](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_createLayer.gif)

次の画面が”[アイテム詳細](https://doc.arcgis.com/ja/arcgis-online/manage-data/item-details.htm)”画面です。

<div align="center">
 <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_itemDetail.png" width="400px">
</div>

### 1_2. アプリで利用するための設定を適用する

アイテム詳細画面を中心に、以下の設定を行っていきます。

 * 添付ファイルを有効化するための設定
 * オフラインで使用するための設定
 * ドメインの設定
 * シンボルの設定

#### 1_2_1. 添付ファイルを有効化するための設定

’trees’のレイヤーに対して[添付ファイルの有効化]を選択します。ポップアップに対して[はい]を選択します。

![有効化の完了まで](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_activeAttachment.gif)

#### 1_2_2. オフラインで使用するための設定

アイテム詳細画面から、右上の[設定]タブを選択します。</br>
設定タブの画面に遷移したら、左上から[Feature Layer（ホスト）]を選択します。
次のチェックボックスを有効化し、[保存]ボタンを選択します。

```
編集

■ 編集の有効化
■ 作成および更新されたフィーチャを記録
■ フィーチャの作成者および最終更新者を記録
■ 同期を有効化 (同期によるディスコネクト編集)

(中略)

データのエクスポート

■ 他のユーザーが別の形式にエクスポートすることを許可します。

```

![オフライン設定](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_offlineSetting.gif)


#### 1_2_3. ドメインの設定

ドメイン（ドロップダウンリスト）を以下の手順で設定します。</br>

 1. アイテム詳細画面から [データ] タブを選択します。
 1. 左端の [レイヤー] のドロップダウンから [trees] を選択します。
 1. 右端の [フィールド] をクリックします。
 1. trees レイヤーの属性フィールドの一覧が表示されたら、`condition` フィールドをクリックします。
 1. 右端に表示される [リストの作成] ボタンを選択しリスト入力画面を表示して次のように入力し、右下の [保存] を選択します。

    ラベル|コード
    ------|---
    良好|1
    普通|2
    不調|3
    枯死|4

![ドメイン一連の設定](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_createDomainList.gif)

#### 1_2_4. シンボルの設定

アイテム詳細画面から、[マップビューアー]で開くを選択します。
次の 2 つのレイヤーそれぞれのシンボルを設定します。

* trees：調査を想定した街路樹のポイントデータを定義したレイヤー
* neighbourhoods：調査範囲を想定したポリゴンデータを定義したレイヤー

trees レイヤー（変更対象のレイヤー）をクリックし、[スタイルの変更]ボタンをクリックします。［①表示する属性を選択］のドロップダウンから `Condition` を選択し、[完了]ボタンを選択します。

レイヤーの [その他のオプション] (「・・・」のアイコン) をクリックし、[レイヤーの保存]を選択して、変更を保存します。

※neighbourhoods レイヤーには、［①表示する属性を選択］で `NAME` を選択し、同じ手順を繰り返します。

![シンボル](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_chSymbol00sized.gif)

## 2. Web マップを作成する

### 2_1. レイヤー順序を変更する

tree レイヤーの表示順序を変更するために、レイヤーの左端をドラッグして最上部に移動させます。

![順番変更](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_chLayerOrder.gif)


### 2_2. Web マップを保存する

画面中央上部の[保存]ボタンを選択して、[名前を付けて保存]を選択します。</br>
以下の2つの項目は必ず入力し、[保存]を選択します。

* タイトル：街路樹調査アプリ
* タグ：test

![保存](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_saveMap.gif)


### 2_3. オフラインで使用するための設定を行う

Web マップのアイテム詳細画面を開いて、[設定]タブを選択します。[オフライン]のセクションで、次の項目を有効化します。

```
オフラインモードの有効化
```

![ビューワーからアイテム詳細画面→設定→オフラインで保存](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_offlinemap.gif)

以上で Web マップの作成は終了です。

## 3. アプリで使用する URL

アプリでは、作成した Web マップのアイテムを表す一意の ID（アイテム ID）を含む URL を使用します。

![アイテム詳細画面のURL](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_webmapUrl.png)

※Web マップのアイテム詳細画面から取得できる URL を使用します。[マップビューアー](https://enterprise.arcgis.com/ja/portal/latest/use/view-maps.htm)から取得できる URL ではアプリから Web マップを参照できませんのでご注意ください。

例：`https://satowakadevdev.maps.arcgis.com/home/item.html?id=40c59402c4c04b0793354f0606bc6c49`


----
# 2. アプリの機能追加と設定

アプリで利用する”地図データ”の設定とデフォルトで実装されている”ログイン機能”を使用するための設定を行います。以下の手順で設定します。

1.  [ログイン機能を利用するための設定](#1-ログイン機能を利用するための設定)
    - 1_1. [アプリを登録し、クライアント ID を入手する](#1_1-アプリを登録しクライアント-id-を入手する)
    - 1_2. [リダイレクト URL を設定する](#1_2-リダイレクト-url-を設定する)
1.  [アプリで利用する情報](#2-アプリで利用する情報)
1.  [Configration.xml を設定してアプリからデータを参照できるようにする](#3-configrationxml-を設定してアプリから-web-マップを参照できるようにする)

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

----
# その他のアプリに関する補足事項

アプリはお客様自身でコードをカスタムし、利用することが可能です。アプリの利用を検討するときに、もう一歩踏み込んで知っておきたい内容を解説します。

## アプリの仕様について

* [最上部のポイントレイヤーのみ編集が可能](#アプリの仕様について編集可能なレイヤー)
* [アプリ起動時に作成される設定ファイル](#アプリの仕様についてアプリ起動時に作成される設定ファイル)
* [ローカライズ対応](#アプリの仕様についてローカライズ対応)

### アプリの仕様について：編集可能なレイヤー

アプリで編集可能なレイヤーは Web マップに追加されているポイント レイヤーのうち最も上部にあるポイント レイヤーです。ポリゴンまたはポリラインのレイヤーは編集対象外です。

### アプリの仕様について：アプリ起動時に作成される設定ファイル

アプリは参照する Web マップや ArcGIS への接続情報、オンライン・オフラインモードのステータスや、オフライン時のデータダウンロードパスなどの情報を保つために、アプリ初回起動時に次のファイルが生成されます。(削除しても、ビルドされた内容に従ってアプリ起動時に再作成されます)

* ファイル名：DataCollectionSettings.xml
* 作成されるファイルのパス：C:\Users\<YourUsername>\AppData\Roaming

※ AppData フォルダは、通常は非表示となっています。

アプリは、起動時に上記のファイルの内容を読み込んで動作します。このファイルには、`Configration.xml` の内容がコピーされています。</br>
Visual Studio での挙動確認時に別の Webマップを参照する場合は、一度上記のファイルを削除します。</br>
また、ビルドした後、アプリ利用中などに他の Web マップを参照する場合は、上記のファイルを編集し、参照先の Web マップ URL を変更して利用できます（再ビルドは不要）。

***DataCollectionSettings.xml の内容***

主に次の内容が XML 形式で定義されています。

* ConnectivityMode：アプリの状態、オンラインまたはオフライン
* OAuthRefreshToken：OAuth 認証の更新トークン
* DownloadPath：モバイルマップパッケージのダウンロードパス
* SyncDate：モバイルマップパッケージが最後にダウンロードまたは同期された日付
* WebmapURL：アプリが参照する Web マップ


### アプリの仕様について：ローカライズ対応

米国Esri社が公開している GitHub の [Data Collection for .NET](https://developers.arcgis.com/example-apps/data-collection-dotnet/) では、次のファイルを編集することにより、ローカライズすることができます。

* **Resources.resx**</br>
HandsOn_Data\02_Data_Collection_Application\data-collection-dotnet-master_ejLocalized\src\DataCollection.Shared\LocalizedStrings

<div align="center">
 <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_translation.png" width="800px">
</div>


## データについて

アプリで利用するホスト フィーチャ レイヤーは、ファイル ジオ データベースをもとに作成しています。</br>
 [HandsOn_Data.zip](https://github.com/EsriJapan/workshops/raw/master/20190823_app-development-hands-on/HandsOn_Data.zip) からダウンロードできるファイル ジオデータベースは、米国Esri社が Data Collection for .NET のために作成した Web マップ（[Mobile_Data_Collection_WFL1](https://runtime.maps.arcgis.com/home/item.html?id=bb6855512ea642298cd6d3726c0c995a)）を元に、ESRIジャパンが街路樹調査を想定して再加工したファイル ジオデータベースです。</br>
 このファイル ジオデータベースは、ArcGIS Pro を使用して作成しています。

![ファイル ジオデータベースの内部構造](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_dataConf.png)

上記の構成図のとおり、Trees（フィーチャクラス）と Species（テーブル）、Trees（フィーチャクラス）と Inspections（テーブル）にはそれぞれ `Global ID` をキーにして、フィーチャクラスとテーブルを関連付けたリレーションシップクラスを作成しています。
リレーションシップクラスは、ジオデータベース内のテーブルやフィーチャクラス間の関連付けを管理するものです。詳細は [ArcGIS Pro:リレーションシップと ArcGIS](http://desktop.arcgis.com/ja/arcmap/latest/manage-data/relationships/relationships-and-arcgis.htm) をご参照ください。


## 機能拡張などの開発について

米国Esri社で公開している [Data Collection for .NET](https://developers.arcgis.com/example-apps/data-collection-dotnet/) は、オープンソースであるためご自身で開発することにより機能を拡張し利用することができます。</br>
[HandsOn_Data.zip](https://github.com/EsriJapan/workshops/raw/master/20190823_app-development-hands-on/HandsOn_Data.zip) で提供しているサンプルプロジェクトでは、アプリ内でアタッチメント追加機能（各フィーチャに画像ファイル情報を追加する）を実装しています。

アタッチメント追加機能の実装方法を以下で解説します。

* [プロジェクト概要](#プロジェクト概要)
* [アタッチメント機能追加の実装内容](#アタッチメント機能追加の実装内容)


### プロジェクト概要

アプリは、.NET の WPF のアプリとして開発されています。</br>
MVVM パターン（Model-View-ViewModel）を使用して開発されています。

**プロジェクト構成**

Visual Studio でプロジェクトをロードすると、2 つのプロジェクトから構成されていることがわかります。

<div align="center">
 <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_structure.png" width="800px">
</div>

* 共通プロジェクト（DataCollection.shared）の役割</br>
アプリを実行するための、主要な設定や処理を行っています。アプリはWPF向けに構築されていますが、UWP や Xamarin で開発する場合でもこのプロジェクトを参照して構築することができます。

* WPFプロジェクト（DataCollection.WPF）の役割</br>
主に画面（Xaml）を定義しています。UI に何か他の項目を追加したい場合は、このプロジェクト内で該当画面を定義しているファイルへ項目を追加します。

### アタッチメント機能追加の実装内容

ポイントレイヤーのフィーチャへ添付ファイル（アタッチメント）を付加する機能を追加実装しています。

<div align="center">
 <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_attachiment.png" width="800px">
</div>

この機能追加は、MVVM パターンに沿って、次の Xaml およびクラスファイルへ処理を追加しています。

* [IdentifiedFeaturePopup.xaml](#identifiedfeaturepopupxaml)</br>
\HandsOn_Data\02_Data_Collection_Application\data-collection-dotnet-master_ejLocalized\src\DataCollection.WPF\Views
* [IdentifiedFeatureViewModel.cs](#identifiedfeatureviewmodelcs)</br>
\HandsOn_Data\02_Data_Collection_Application\data-collection-dotnet-master_ejLocalized\src\DataCollection.Shared\ViewModels

それぞれ、ソースコードの変更箇所を解説します。

### IdentifiedFeaturePopup.xaml

この Xaml ファイルには、ポップアップでフィーチャを参照するときと編集モードのときに表示する 2 つの画面が 1 つのファイルで定義してあります。添付ファイルについて表示する項目とボタンを追加しています。

```
// コード抜粋：ポップアップ表示にアタッチメントの有無及びファイル名称とサムネイルを表示できるようにする

<!-- Popup user control in View Mode -->
・・・
<Grid Background="White">
    <Grid.RowDefinitions>
        <RowDefinition Height="*"/>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="Auto"/>
        <!--  ej update：1 行追加-->
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="40"/>
        <!-- ej update-->
    </Grid.RowDefinitions>

・・・

<!-- ej add-->
<Grid Background="White" Grid.Row="3">
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="*"/>
        <ColumnDefinition Width="40"/>
    </Grid.ColumnDefinitions>
    <TextBlock Name="textblock" Margin="10, 10, 10, 0" Text="{Binding attachimentList}"/>
    <Image Source="{Binding Path=attachiment}" Width="50" Height="30" HorizontalAlignment="Right"/>
</Grid>
<!-- ej add-->

// コード抜粋：ポップアップの編集画面にアタッチメントのファイル名称とサムネイルを表示、アタッチメント選択ボタンを追加する

<!--Popup user control in Edit Mode-->
・・・
<Grid.RowDefinitions>
    <RowDefinition Height="*"/>
    <RowDefinition Height="Auto"/>
    <RowDefinition Height="Auto"/>
    <!-- ej update：1 行追加-->
    <RowDefinition Height="Auto"/>
    <RowDefinition Height="40"/>
    <!-- ej update-->

・・・

<!-- ej add-->
<Grid Background="Orange" Grid.Row="3">
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="*"/>
        <ColumnDefinition Width="40"/>
    </Grid.ColumnDefinitions>
    <TextBlock Name="textblockedit" Margin="10, 10, 10, 0" Text="{Binding attachimentList}"/>
    <Image Source="{Binding Path=attachiment}" Width="50" Height="30" HorizontalAlignment="Right"/>
    <Button Content="&#xE70F;" FontFamily="Segoe MDL2 Assets" FontSize="15" Width="30" Height="30" Style="{StaticResource MenuButtonStyle}"
        HorizontalAlignment="Right" Margin="0, 0, 10, 0" Grid.Column="1" Command="{Binding AttachmentCommand}"
            ToolTip="{Binding ., Converter={StaticResource LocalizationConverter}, ConverterParameter=EditRecord_Tooltip}"/>
</Grid>
<!-- ej add-->

```

`<TextBlock>`タグに定義している `attachmentList` 変数は `IdentifiedFeatureViewModel` クラスに定義した内容を指定しています。`<Image>` タグの `attachiment` 変数も同じクラスに定義しています。Image タグがバインドしている変数は、アタッチメントをサムネイルとして表示するようにしています。

アプリから一度に付加できるアタッチメントは 1 つですが、各フィーチャへは複数のアタッチメントが登録可能です。
ひとつのフィーチャに対して複数のアタッチメントがある場合は、最新のファイル名とサムネイルを 1 件のみ表示します。

アタッチメントの削除機能はありません。Web マップから行います。登録したアタッチメントを削除したい場合は、ArcGIS Online から行います。
操作方法は、[ArcGIS Online 逆引きガイド](https://www.esrij.com/cgi-bin/wp/wp-content/uploads/documents/ArcGISOnline_user_guide.pdf)の ”4-12. 属性を編集したい”を参考にしてください。

###  **IdentifiedFeatureViewModel.cs**

このクラスには、選択されたポイントフィーチャの属性情報など検索する処理が実装されています。</br>
コンストラクタ（`IdentifiedFeatureViewModel()`）が呼び出しされたときにアタッチメントの有無を検査するメソッドを追加しました。

**既存アタッチメントの参照**

```

// 定義済みのコンストラクタ
public IdentifiedFeatureViewModel(Feature feature, FeatureTable featureTable, ConnectivityMode connectivityMode)
{
    if (feature != null)
    {
        Feature = feature;
        PopupManager = new PopupManager(new Popup(feature, featureTable.PopupDefinition));
        Fields = FieldContainer.GetFields(PopupManager);
        FeatureTable = featureTable;
        ConnectivityMode = connectivityMode;

        // アタッチメントをチェックする(EJ_add)
        checkAttachment(feature);

    }
}

・・・

/// <summary>
/// フィーチャのアタッチメントの有無をチェックする
///
/// by esrijapan
/// </summary>
/// <param name="pFeature"></param>
public async void checkAttachment(Feature pFeature)
{
    ArcGISFeature arcGISFeature = (ArcGISFeature)pFeature;
    IReadOnlyList<Attachment> attachments = await arcGISFeature.GetAttachmentsAsync();

    if (attachments.Count() > 0)
    {
        // アタッチメントが存在するなら、最初の1つだけを表示する(複数ある場合は"他"をつける)
        String _fullName = attachments.First().Name;

        // サムネイルを表示する
        Stream x = await attachments.First().GetDataAsync();
        var source = new BitmapImage();
        source.BeginInit();
        source.StreamSource = x;
        source.EndInit();
        attachiment = source;

        attachmentList += _fullName;
        if (attachments.Count() > 1)
        {
            attachmentList += "、他";
        }
    }
    else
    {
        //ない場合は、ない旨のメッセージを詰める
        attachmentList = "添付ファイルはありません";
    }
}

```

`checkAttachment()`メソッドは、選択されたポイントのフィーチャを引数にとっています。
この引数からアタッチメントリストを取得し、ファイルの有無を判断しています。

**アタッチメントの登録**

`IdentifiedFeaturePopup.xaml` からアタッチメントを選択するボタンが選択されたら、エクスプローラーを開いて、任意の添付ファイルを選択します。選択されたファイルは、ArcGIS Runtime SDK for .NET のアタッチメントマネージャ（`AttachmentManager`）に渡すことで、対象のフィーチャに対してアタッチメントを追加することができます。

```
/// <summary>
/// コマンド（ボタン選択時の処理）のための変数
/// wrote by esrijapan
/// </summary>
// アタッチメントをアプリに一時保存するためのコマンド
private ICommand _attachmentCommand;

/// <summary>
/// アタッチメント選択ボタンを押されたときに行う処理
///  1.エクスプローラを開く
///  2.PopupManagerのAttachmentManagerで、アタッチメントを追加する
/// </summary>
public ICommand AttachmentCommand
{
    get
    {
        return _attachmentCommand ?? (_attachmentCommand = new DelegateCommand(
            (x) =>
            {
                // エクスプローラーを開く
                OpenFileDialog ofd = new OpenFileDialog();
                ofd.Title = "JPEGファイルを開く";
                //複数ファイルを選択できるようにする
                ofd.Multiselect = false;
                // [ファイルの種類] ボックスに表示される選択肢を設定する
                ofd.Filter = "JPEGファイル(*.jpg;*.jpeg)|*.jpg;*.jpeg";

                //ダイアログを表示
                string[] files = null;
                if (ofd.ShowDialog() == DialogResult.OK)
                {
                    //選択されたファイル名を変数にセット
                    files = ofd.FileNames;
                    ////////////////////////////////////////////////////////////////////////
                    // ポップアップマネージャーのアタッチメントマネージャーのAddAttachment()メソッドを使用してアタッチメントを追加する
                    // ■引数
                    // ①files[0] >file配列の0番目
                    // ②"image/png" > アタッチメント画像の種別
                    PopupManager.AttachmentManager.AddAttachment(files[0], "image/png");
                    ////////////////////////////////////////////////////////////////////////

                    // 表示ファイル名の取得
                    String _addFileName = Path.GetFileName("@" + files[0]);
                    attachmentList = _addFileName;

                    // サムネイルを表示する
                    var source = new BitmapImage();
                    source.BeginInit();
                    source.UriSource = new Uri(files[0]);
                    source.EndInit();
                    attachiment = source;

                }
                else
                {
                    // 「キャンセル」が選択されたときの処理
                    // なにもしない
                }
            }));
    }
}

```

**画面へ値を反映する**
このプロジェクトは、MVVM パターンに従って構築されているため、画面へ処理結果を反映するためには、次の処理をコーディングする必要があります。

```
// 定義済みのアタッチメント取得用
private string _attachmentList;

/// <summary>
/// View(画面)へ反映する変数を定義する
/// </summary>
public string attachmentList
{
    get { return _attachmentList; }
    set
    {
        _attachmentList = value;
        // 値が変更されたら呼ぶメソッドを実装する
        OnPropertyChanged();
    }
}

```

`attachmentList` は、新しく追加した変数です。処理を行った後の値が格納されます。</br>
プロパティが変更されたときは `OnPropertyChanged()` を使用します。
