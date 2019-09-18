# Data Collection for .NET アプリの設定と起動

<div align="center">
 <img src="https://developers.arcgis.com/example-apps/data-collection-dotnet/img/featured-img.png" width="500px">
</div>

</br>

# 概要

この内容は、[ArcGIS 開発者のための最新アプリ開発塾 2019](https://github.com/EsriJapan/workshops/tree/master/20190823_app-development-hands-on) の [ArcGIS プラットフォームを活用した調査アプリケーション構築までのハンズオン](https://github.com/EsriJapan/workshops/blob/master/20190823_app-development-hands-on/02_ArcGIS_%E3%83%97%E3%83%A9%E3%83%83%E3%83%88%E3%83%95%E3%82%A9%E3%83%BC%E3%83%A0%E3%82%92%E6%B4%BB%E7%94%A8%E3%81%97%E3%81%9F%E8%AA%BF%E6%9F%BB%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E6%A7%8B%E7%AF%89%E3%81%BE%E3%81%A7%E3%81%AE%E3%83%8F%E3%83%B3%E3%82%BA%E3%82%AA%E3%83%B3.pdf) のセクションで、サンプルアプリケーションを使用して実施したハンズオンの手順を示しています。</br>
ハンズオンでは、米国ESRI が公開する [Data Collection for .NET](https://developers.arcgis.com/example-apps/data-collection-dotnet/) を元に、ESRIジャパンにてローカライズしたサンプルプロジェクトを開発ツール（Visual Studio 2017）を使用してビルドし、ご自身で作成した地図データ（Web マップ）を適用してアプリケーションを起動しました。再現するための手順を gif を交えてご紹介しています。

このハンズオンで使用するものは次の2つです

* ArcGIS for Developers（開発者アカウント）
* Visual Studio 2017

ローカライズ済みのサンプルプロジェクトは [HandsOn_Data.zip](https://github.com/EsriJapan/workshops/blob/master/20190823_app-development-hands-on/HandsOn_Data.zip) からダウンロードできます。</br>
米国ESRI が公開する、[Data Collection for .NET](https://developers.arcgis.com/example-apps/data-collection-dotnet/) のページおよび [GitHub ソース](https://github.com/Esri/data-collection-dotnet)についてもぜひご参照ください。

なお、[ハンズオン時に使用した資料（PPT）](https://github.com/EsriJapan/workshops/blob/master/20190823_app-development-hands-on/02_ArcGIS_%E3%83%97%E3%83%A9%E3%83%83%E3%83%88%E3%83%95%E3%82%A9%E3%83%BC%E3%83%A0%E3%82%92%E6%B4%BB%E7%94%A8%E3%81%97%E3%81%9F%E8%AA%BF%E6%9F%BB%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E6%A7%8B%E7%AF%89%E3%81%BE%E3%81%A7%E3%81%AE%E3%83%8F%E3%83%B3%E3%82%BA%E3%82%AA%E3%83%B3.pdf)もご覧いただけます。

## ハンズオンのテーマ

ハンズオンで取り上げた調査アプリケーション（以下、アプリ）は、**街路樹の現地調査を行う** というテーマで進めました。アプリを動作させるためのデータとして、東京都練馬区の街路樹を想定したサンプルのファイルジオデータベースも [HandsOn_Data.zip](https://github.com/EsriJapan/workshops/blob/master/20190823_app-development-hands-on/HandsOn_Data.zip)
から公開しています。現地調査を行うときは、オフライン（インターネットが繋がらない）状態で利用するというケースを想定し、そのための設定もハンズオン中に解説しました。

# 手順

アプリを起動するために、大きく分けて次の 2 つのステップを作業します。

1.[地図データの準備](#1地図データの準備概要)  
2.[アプリの機能追加と設定](#2-アプリの機能追加と設定)


なお、アプリについてのデータや開発について踏み込んだ内容は以下の項目でご紹介しています。

* [他、アプリに関する知識](#他アプリに関する知識)

----
# 1.　地図データの準備（概要）

アプリで利用する地図データを作成します。ArcGIS には、地図データを作成する手段が複数ありますが、アプリケーションからも参照できる地図データを最も簡単に作成する方法は、ArcGIS Online というクラウド GIS を使用する方法です。</br>
ArcGIS Online では、**Webマップ**と呼ばれる地図データを作成できます。 Web マップには、地図上に表示したい情報をひとまとめにした”レイヤー”を重ねることで、目的に沿った地図を Web 上で作成することが可能です。</br>

レイヤーにはいくつか種類があります。ハンズオンでは、**ホスト フィーチャ レイヤー** というレイヤーを使用しました。これは、緯度経度や住所などの位置情報をデータとして保持している CSV ファイルやファイルジオデータベースなどをもとに ArcGIS Online で作成することができます。これは、オフラインのアプリケーションにも対応しているレイヤーです。

作成する Web マップの構成は次のようになります。

![Webマップのデータ構成](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_webmap.png) 

Webマップを作成します。</br>Web マップとホスト フィーチャ レイヤーの作成順序は問いません。（便宜上、ホスト フィーチャ レイヤーから作成します）背景地図は ArcGIS Online が配信している背景地図を利用します。</br>
★の項目は Web マップをオフライン対応のアプリで利用する場合は必ず設定する項目となります。

* [ホスト フィーチャ レイヤーを作成する](#ホスト-フィーチャ-レイヤーを作成する)
    * [ファイルジオデータベースからホストフィーチャレイヤーを作成する](#ファイルジオデータベースからホストフィーチャレイヤーを作成する)
    * [アプリで利用するための設定を適用する](#アプリで利用するための設定を適用する)
        * [添付ファイルを有効化するための設定](#添付ファイルを有効化するための設定)
        * [オフラインで使用するための設定★](#オフラインで使用するための設定)
        * [ドメインの設定](#ドメインの設定)
        * [シンボルの設定](#シンボルの設定)
* [Web マップを作成する](#Web-マップを作成する)
    * [レイヤー順序を変更する](#レイヤー順序を変更する)
    * [Web マップを保存する](#Web-マップを保存する)
    * [オフラインで使用するための設定を行う★](#オフラインで使用するための設定を行う)
* [アプリで使用するURL](#アプリで使用する-url)

------

## ホスト フィーチャ レイヤーを作成する

### ファイルジオデータベースからホストフィーチャレイヤーを作成する

[HandsOn_Data.zip](https://github.com/EsriJapan/workshops/blob/master/20190823_app-development-hands-on/HandsOn_Data.zip) ページより、[Download]ボタンを選択して、Zip ファイルを端末ローカルにダウンロードします。この Zipファイルを解凍した内容には次の Zip ファイルが含まれています。

* **tree_inspection.gdb.zip**</br>
Zip までのpath：C:\Users\<YourUsername>\HandsOn_Data\02_Data_Collection_Application

Zip ファイルの中身は **ファイルジオデータベース** です。Zip ファイルのまま利用します。</br>
データ構造や作成方法の詳しい内容は、[他、アプリに関する知識](#他アプリに関する知識) の [データについて：ファイルジオデータベースの作成方法](#データについてファイルジオデータベースの作成方法) をご参照ください。

***ArcGIS for Developers へログイン***

ArcGIS for Developers へログインします。開発者のためのダッシュボードが表示されるので、[manage Content]ボタンから、ArcGIS Online のアイテム一覧画面を開きます。

![ArcGIS for Developers からログイン、アイテム一覧ページまで](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_loginToList.gif) 

※言語表示が英語の方は [ArcGIS Online 逆引きガイド](http://www.dokairen-okinawa.jp/wp/wp-content/uploads/arcgis-online-e98086e5bc95e3818de382ace382a4e38389-e6b0b4e59c9fe9878ce3838de38383e38388e3818ae3818de381aae3828f.pdf)から"マイ プロフィールの設定”の項目を参考に日本語に設定します。

**ホストフィーチャレイヤーの作成**

画面左上の[アイテムの追加]ボタンより、[コンピューター上]を選択します。</br>
コンピューターからアイテムを追加のポップアップが表示されますので、[ファイルを選択]よりダウンロードした Zip ファイルを選択します。</br>
他、次の 2 つを指定または入力し[アイテムの追加]ボタンを選択します。

* コンテンツ：ファイル ジオデータべース
* タグ：テスト(任意)
* ※他はデフォルトのまま

![アイテム指定からサービス作成中の画面まで](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_createLayer.gif) 

アイテムを作成中、または作成が完了した画面は”アイテム詳細”画面と呼びます。

### アプリで利用するための設定を適用する

[アイテム詳細](https://doc.arcgis.com/ja/arcgis-online/manage-data/item-details.htm)画面を中心に、次の設定を行っていきます。

 * 添付ファイルを有効化するための設定
 * オフラインで使用するための設定★
 * ドメインの設定
 * シンボルの設定

#### 添付ファイルを有効化するための設定

’trees’のレイヤーに対して[添付ファイルの有効化]を選択します。ポップアップが表示されますので、[はい]を選択します。

![有効化の完了まで](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_activeAttachment.gif) 

※完了後は`trees`レイヤーの添付ファイルの設定は「添付ファイルの無効化」となります。

#### オフラインで使用するための設定★

アイテム詳細画面から、右上の[設定]タブを選択します。</br>
左上から[Feature Layer（ホスト）]を選択して、これについて定義しているセクションを表示します。</br>
次のチェックボックスを有効化し、[保存]ボタンを選択します。

```
編集

■ 編集の有効化★
■ 作成および更新されたフィーチャを記録
■ フィーチャの作成者および最終更新者を記録
■ 同期を有効化 (同期によるディスコネクト編集)★

・・・

データのエクスポート

■ 他のユーザーが別の形式にエクスポートすることを許可します。★　　

※★は必須です。それ以外は必要に応じて設定します。
```

![オフライン設定](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_offlineSetting.gif) 


#### ドメインの設定

ドメインリスト（ドロップダウンリスト）を設定します。</br>
アプリでは、ホストフィーチャレイヤーに設定したドメインリストを反映して利用することができます。

1. アイテム詳細画面から[データ]タブを選択します。画面の左右両端にある次の項目をそれぞれ次のように設定します。（順不同）

    * レイヤー：trees
    * 「フィールド」に切り替える

1. trees レイヤーの項目一覧が表示されたら、`condition` フィールドをクリックします
1. 右端に表示される[リストの作成]ボタンを選択しリスト入力画面を表示して次のように入力し、右下の[保存]を選択します。

    ラベル|コード
    ------|---
    良好|1
    普通|2
    不調|3
    枯死|4

![ドメイン一連の設定](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_createDomainList.gif) 

#### シンボルの設定

アイテム詳細画面から、[マップビューワー]で開くを選択します。
次の 2 つのレイヤーそれぞれのシンボルを設定します。

* trees：調査を想定した街路樹のポイントデータを定義したレイヤー
* neighbourhoods：調査範囲を想定したポリゴンデータを定義したレイヤー

treesレイヤー（変更対象のレイヤー）をクリックし、[スタイルの変更]ボタンをクリックします。［①表示する属性を選択］のドロップダウンから `Condition` を選択し、[完了]ボタンを選択します。

レイヤーの「・・・」メニューから[レイヤーの保存]を選択して、レイヤーの定義を変更します。

※neighbourhoodsレイヤーは同じく `NAME` を選択して同手順を繰り返します。

![シンボル変更](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_chSymbol_sized.gif)

## Web マップを作成する

### レイヤー順序を変更する

データをバインドしてドラッグし、ポイントレイヤーを最上部の順序に変更します。

![順番変更](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_chLayerOrder.gif) 


### Web マップを保存する

画面中央から[保存]ボタンを選択して、[名前を付けて保存]を選択します。　　
次の内容を入力し、[保存]を選択します。

* タイトル：街路樹調査アプリ
* タグ：test

![保存](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_saveMap.gif) 


※タイトルに入れた内容がWebマップのタイトルであり、アプリ内ではアプリ名称を表すような表示となります。

### オフラインで使用するための設定を行う★

Web マップのアイテム詳細画面を開いて、[設定]タブを選択します。[オフライン]のセクションで、次の項目がアクティブとなっていれば、オフラインで使用できるマップとなります。

![ビューワーからアイテム詳細画面→設定→オフラインで保存](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_offlinemap.gif) 

これで Web マップが完成です。

## アプリで使用する URL

アプリでは、作成した Web マップのアイテムを表す一意の ID (アイテムID )を含む URL を使用します。

![アイテム詳細画面のURL](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_webmapUrl.png) 

※Web マップのアイテム詳細画面から取得できる URL を使用します。マップビューアーから取得できる URL ではアプリに反映できませんのでご注意ください。

例：`https://satowakadevdev.maps.arcgis.com/home/item.html?id=40c59402c4c04b0793354f0606bc6c49`


----
# 2. アプリの機能追加と設定

[地図データの準備](#1地図データの準備概要) で作成した Web マップを反映しアプリを起動します。</br>
起動するまでの手順として次を説明します。

* [ログイン機能を利用するための設定（ ArcGIS for Developers による）](#ログイン機能を利用するための設定arcgis-for-developers-による)
    * [アプリを登録し、クライアント ID を入手する](#アプリを登録しクライアント-id-を入手する)
    * [リダイレクト URL を設定する](#リダイレクト-url-を設定する)
* [アプリで利用する情報](#アプリで利用する情報)
* [Configration.xml を設定してアプリにデータを反映する](#configrationxml-を設定してアプリにデータを反映する)

## ログイン機能を利用するための設定（ArcGIS for Developers による）

ArcGIS for Developers で「アプリケーションの登録」を行い、ログイン機能を利用できるようにします。

アプリケーションの登録は、ArcGIS for Developers のダッシュボード画面から行います。</br>
手順は、アイテム詳細画面の「App Launcher」から「Developers」のアイコンを選択し、「New Application」ボタンを選択します。または、ArcGIS for Developers のダッシュボード画面から「New Application」のボタンを選択します。

![アイテム詳細画面からダッシュボード、登録画面](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_devLauncher.gif) 

### アプリを登録し、クライアント ID を入手する

「New Application」のページでは、次の 3 つを入力し[Register New Application]を選択します。title に入力したページが表示して登録完了します。

* title：DataCollecton
* tag：test
* Description：データコレクションアプリ

※Description 以外は半角英数字で入力します

![入力から登録ボタン選択、アプリ登録完了](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_registration.gif) 

### リダイレクト URL を設定する

アプリの登録完了の画面から、[Authentication]タブを選択して、ページ最下部までスクロールします。[Redirect URIs]の項目に次を入力して、[Add]を選択します。

例：`DataCollection://oauth`

![リダイレクトURLの登録](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_redirectUrl.gif) 

みどりのチェックが表示されれば、利用可能な URL として登録ができます。

***注意***</br>
ブラウザによる翻訳機能を適用した状態では正しいリダイレクト URL が登録できません（余分なスペースが含まれてしまうため）。</br>
必ずデフォルトの言語設定のままURLの登録を行ってください。


### アプリで利用する情報

アプリでは、アプリケーションの登録により取得した次の ID および URL を使用します。

例：  
* クライアントID：g0biHDu8TD2G8XXX
* リダイレクトURL：DataCollection://oauth

![リダイレクトURLの登録](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_credentialInf.png) 

## Configration.xml を設定してアプリにデータを反映する

作成した次の ID および URL をアプリに反映します。

* Web マップのURL
* クライアントID
* リダイレクトURL

[HandsOn_Data.zip](https://github.com/EsriJapan/workshops/blob/master/20190823_app-development-hands-on/HandsOn_Data.zip) からダウンロードした中に含まれている、次のプロジェクトファイル（*.sln）を Visual Studio 2017 で開きます。

* **DataCollection.sln**</br>
sln ファイルまでの path：C:\Users\<YourUsername>\HandsOn_Data\02_Data_Collection_Application\data-collection-dotnet-master_ejLocalized\src

![リダイレクトURLの登録](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_startSln.gif)

'Configration.xml'を開きます。このファイルには、次の XML タグにそれぞれ ID および URL を設定します。

<div align="center">
 <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_settingInfo.png" width="800px">
</div>

設定が完了したら、必ずビルドを行います。開始からアプリを起動して、ご自身で作成した Web マップが表示されましたら起動完了です。Web マップが表示される前にログインの認証画面が表示される場合は、入力を行います。

<div align="center">
 <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_startupApp.png" width="800px">
</div>

----
# 他、アプリに関する知識

アプリはお客様自身でコードをカスタムし、利用することが可能です。アプリの利用を検討するときに、もう一歩踏み込んで知っておきたい内容を、カテゴリ別に以下でご説明します。

<データについて>
* [ファイルジオデータベースの作成方法](#データについてファイルジオデータベースの作成方法)

<アプリの仕様について>
* [最上部のポイントレイヤーのみ編集が可能](#アプリの仕様について最上部のポイントレイヤーのみ編集が可能)
* [アプリ起動時に作成される設定ファイル](#アプリの仕様についてアプリ起動時に作成される設定ファイル)
* [ローカライズ対応](#アプリの仕様についてローカライズ対応)

<開発について>
* [プロジェクト概要](#開発についてプロジェクト概要)
* [アタッチメント機能追加の実装内容](#アタッチメント機能追加の実装内容)

### データについて：ファイルジオデータベースの作成方法

 [HandsOn_Data.zip](https://github.com/EsriJapan/workshops/blob/master/20190823_app-development-hands-on/HandsOn_Data.zip) からダウンロードできるファイルジオデータベースは、米国ESRI が Data Collection for .NET のために作成した Web マップ（[Mobile_Data_Collection_WFL1](https://runtime.maps.arcgis.com/home/item.html?id=bb6855512ea642298cd6d3726c0c995a)）を元に、ESRIジャパンが街路樹調査を想定して再加工したファイルジオデータベースです。</br>
 このファイルジオデータベースは、ArcGIS Pro により作成しています。

![ファイルジオデータベースの内部構造](https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_dataConf.png) 


上記の構成図のとおり、Species・Trees、Trees・Inspections にはそれぞれ `Global ID` をキーにして、フィーチャクラスとテーブルを関連付たリレーションシップクラスを持たせています。
リレーションシップクラスは、ジオデータベース内のテーブルやフィーチャクラス間の関連付けを管理するものです。[ArcGIS Pro:リレーションの作成](http://desktop.arcgis.com/ja/arcmap/latest/manage-data/relationships/relationships-and-arcgis.htm) をご参照ください。

ファイルジオデータベースをもとに ArcGIS Online へホスト フィーチャ レイヤーを作成する場合は、必ず Zip 形式に圧縮します。

### アプリの仕様について：最上部のポイントレイヤーのみ編集が可能

Web マップで定義しているレイヤーの順序に基づいて、最上部に表示されているポイントデータのレイヤーが編集対象のレイヤーとなります。
ただし、ポイントのレイヤーの上にポリゴン、またはポリラインのレイヤーがある場合は、それらを除いて最上部にあるポイントレイヤーが編集対象となります。

### アプリの仕様について：アプリ起動時に作成される設定ファイル

アプリはオンライン・オフラインモードのステータスや、オフライン時のデータダウンロードパスを保つために、アプリ初回起動時に次のファイルが生成されます。(削除しても、ビルドされた内容に従って再作成されます)

* ファイル名：DataCollectionSettings.xml
* 作成パス：C:\Users\<YourUsername>\AppData\Roaming

※ AppData 配下のフォルダは、通常は非表示となっています。

***DataCollectionSettings.xml の内容***

内容は主に次の内容が XML 形式で定義されています。

* ConnectivityMode：アプリケーションの状態、オンラインまたはオフライン
* OAuthRefreshToken：OAuth 認証の更新トークン
* DownloadPath：モバイルマップパッケージのダウンロードパス
* SyncDate：モバイルマップパッケージが最後にダウンロードまたは同期された日付
* WebmapURL：アプリが参照する Web マップ

Web マップについての項目は、手動で編集することで再ビルドしなくても変更した Web マップを反映してアプリを使用することができます。

### アプリの仕様について：ローカライズ対応

米国ESRIが公開している GitHub の [Data Collection for .NET](https://developers.arcgis.com/example-apps/data-collection-dotnet/) では、次のファイルを編集することにより、ローカライズの実現に対応しています。

* **Resources.resx**</br>
C:\Users\<YourUsername>\HandsOn_Data\02_Data_Collection_Application\data-collection-dotnet-master_ejLocalized\src\DataCollection.Shared\LocalizedStrings

<div align="center">
 <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_translation.png" width="800px">
</div>

### 開発について：プロジェクト概要

**プロジェクト全体**

アプリは、.NET フレームワークに基づく WPF 形式のアプリとして構築されています。</br>
また、ソフトウェアアーキテクチャとして、MVVM パターン（MOdel-View-ViewModel）を使用して構築されています。

**プロジェクト構成**

Visual Studio からプロジェクトをロードすると、以下のように 2 つのプロジェクトから構成されていることがわかります。

<div align="center">
 <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_structure.png" width="800px">
</div>

* 共通プロジェクト（DataCollection.shared）の役割</br>
アプリを実行するための、主要な設定や処理を行っています。アプリはWPF向けに構築されていますが、WPF や Xamarin で同様のアプリを構築したい場合は、この共通プロジェクトを参照して構築することができます。

* WPFプロジェクト（DataCollection.WPF）の役割</br>
主に画面（Xaml）を定義しています。UI に何か他の項目を追加したい場合は、このプロジェクト内で該当の画面を定義しているファイルへ項目を追加します。

### アタッチメント機能追加の実装内容

[HandsOn_Data.zip](https://github.com/EsriJapan/workshops/blob/master/20190823_app-development-hands-on/HandsOn_Data.zip) からダウンロードできるプロジェクトは、ポイントレイヤーのフィーチャへ添付ファイルを付加する機能を追加実装しています。

<div align="center">
 <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_attachiment.png" width="800px">
</div>

この機能追加は、MVVM パターンに沿って、次の Xaml およびクラスファイルへ処理を追加しています。

* [IdentifiedFeaturePopup.xaml](#identifiedfeaturepopupxaml)</br>
C:\Users\<YourUsername>\HandsOn_Data\02_Data_Collection_Application\data-collection-dotnet-master_ejLocalized\src\DataCollection.WPF\Views
* [IdentifiedFeatureViewModel.cs](#identifiedfeatureviewmodelcs)</br>
C:\Users\<YourUsername>\HandsOn_Data\02_Data_Collection_Application\data-collection-dotnet-master_ejLocalized\src\DataCollection.Shared\ViewModels

それぞれ、ソースコードの変更箇所を解説します。

##### **IdentifiedFeaturePopup.xaml**

この Xaml ファイルには、ポップアップでフィーチャを参照するときと編集モードのときに表示する画面の 2 つが 1 つのファイルで定義してあります。添付ファイルについて表示する項目とボタンを追加しています。


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

変数 `attachimentList` は `IdentifiedFeatureViewModel` クラスに定義した内容を表示します。Image タグの `attachiment` はアタッチメントをサムネイルとして表示します。

選択したポイントフィーチャがすでにアタッチメントを 1 つ以上保持している場合は、アタッチメント名称を表示して、イメージ部分はサムネイルを表示します。(複数ある場合は、一番最新のアタッチメントのみを表示します)

(アタッチメントの削除機能はありません。Web マップから行います)

##### **IdentifiedFeatureViewModel.cs**

このクラスには、アプリ画面からポイントフィーチャを選択し、ポップアップとして表示する処理を行うときに必ず実行される処理がデフォルトで定義されています。また、フィーチャの属性内容を編集し、更新する処理も定義されています。

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

        attachimentList += _fullName;
        if (attachments.Count() > 1)
        {
            attachimentList += "、他";
        }
    }
    else
    {
        //ない場合は、ない旨のメッセージを詰める
        attachimentList = "添付ファイルはありません";
    }
}

```

`checkAttachment()`メソッドは、選択されたポイントのフィーチャを引数にとっています。
この引数からアタッチメントリストを取得し、ファイルの有無を判断しています。

**新規アタッチメントの登録**

`IdentifiedFeaturePopup.xaml` からアタッチメントを選択するボタンが選択されたら、エクスプローラーを開いて、任意の添付ファイルを選択します。選択されたファイルは、Runtime SDK のアタッチメントマネージャ（`AttachmentManager`）に渡すことで、対象のフィーチャに対して添付ファイルを追加することができます。

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
                    // ポップアップマネージャーのアタッチメントマネージャーをのAddAttachment()メソッドを使用してアタッチメントを追加する
                    // ■引数
                    // ①files[0] >file配列の0番目
                    // ②"image/png" > アタッチメント画像の種別
                    PopupManager.AttachmentManager.AddAttachment(files[0], "image/png");
                    ////////////////////////////////////////////////////////////////////////

                    // 表示ファイル名の取得
                    String _addFileName = Path.GetFileName("@" + files[0]);
                    attachimentList = _addFileName;

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

このプロジェクトは、MVVM パターンに従って構築されているため、画面へ処理結果を反映するためには、必ず次の処理をコーディングする必要があります。


```
// 定義済みのアタッチメント取得用
private string _attachimentList;

/// <summary>
/// View(画面)へ反映する変数を定義する
/// </summary>
public string attachimentList
{
    get { return _attachimentList; }
    set
    {
        _attachimentList = value;
        // 値が変更されたら呼ぶメソッドを実装する
        OnPropertyChanged();
    }
}

```

`attachimentList` は、新しく追加した変数です。処理を行った後の値が格納されます。</br>
`OnPropertyChanged()` メソッドが画面と処理をつなぐメソッドとなります。

