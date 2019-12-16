# アプリの仕様について（詳細）

アプリはお客様自身でコードをカスタムし、利用することが可能です。アプリの利用を検討するときに、もう一歩踏み込んで知っておきたい内容を解説します。

* [編集可能なレイヤーについて](#アプリの仕様について編集可能なレイヤー)
* [アプリ起動時に作成される設定ファイル](#アプリの仕様についてアプリ起動時に作成される設定ファイル)
* [ローカライズ対応](#アプリの仕様についてローカライズ対応)
* [データについて](#データについて)
* [ポップアップ表示をカスタムする](# ポップアップ表示をカスタムする)


## 編集可能なレイヤーについて

アプリで編集可能なレイヤーは、Web マップに追加されているポイント レイヤーのうち最も上部にあるポイント レイヤーです。ポリゴンまたはポリラインのレイヤーは編集対象外です。

## アプリ起動時に作成される設定ファイル

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


## ローカライズ対応

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

## ポップアップ表示をカスタムする

アプリで表示するフィーチャのポップアップ構成は、Web マップの設定で変更できます。</br>
ポップアップの構成設定は、Web マップで定義している各レイヤーの[・・・]を選択し、[ポップアップの構成]から設定画面を開きます。</br>
ポップアップの詳しい内容は、[ArcGIS Online 逆引きガイド（PDF）](https://www.esrij.com/cgi-bin/wp/wp-content/uploads/documents/ArcGISOnline_user_guide.pdf)の「3-4. ポップアップの内容を変更したい」もご参照ください。

### ポップアップのタイトル

設定するポップアップのタイトルは、アプリからフィーチャを選択してポップアップを表示させたときに先頭に表示される項目です。</br>
ポップアップタイトルは、固定の文字列で設定することも、属性情報でフォーマットして表示することもできます。画面サイズを考慮して設定することを推奨します。

例えば、”保存樹木”という固定の文字列に、属性情報の樹木名称を組み合わせて表示したい場合は次のように定義します。</br>

``` 保存樹木: {trees}``` 

<div align="center">
 <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_popuptitle.png" width="300px">
</div>

### ポップアップに表示する項目（属性情報）

表示または編集できる属性情報の項目をカスタムすることができます。</br>
``` 表示：``` のドロップダウンで ```属性フィールドのリスト``` を選択すると、ウィンドウに表示する属性フィールドが表示されます。任意の属性情報を一度選択してから、右横の上下の矢印を操作すると、選択した属性情報の項目の表示順番を指定することができます。

<div align="center">
 <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_popuplistupdate.png" width="300px">
</div>

```属性フィールドの構成``` を選択すると、表示または編集する属性項目を詳細に設定することができます。</br>
フィーチャ サービスでは、フィーチャの更新日時や編集者の情報を記録するための属性情報があらかじめ作成されています。この情報もこの構成画面から表示できるように設定することができます。

<div align="center">
 <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_popuplistselect.png" width="300px">
</div>
