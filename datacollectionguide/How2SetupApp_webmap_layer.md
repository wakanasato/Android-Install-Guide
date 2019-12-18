# アプリで使用する地図データの作成

アプリで使う地図データを作成します。<br>
以下の構成の Web マップを作成します。

<div align="center">
 <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_webmap.png" width="400px">
</div>

Web マップ作成手順は以下の通りです。

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

