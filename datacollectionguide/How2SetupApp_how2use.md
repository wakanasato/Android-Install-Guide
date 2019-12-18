# アプリの操作方法

アプリの使用方法として、次の方法を解説します。

* アプリアイコンの説明
* ログイン方法
* オフラインモードを適用する
* アタッチメント（添付ファイル）を任意のフィーチャへ追加する
* 属性情報を更新する
* オフラインモードの編集データをArcGIS Online と同期する
* 【番外】同期結果をマップビューアーから確認する

## アプリアイコンの説明

<div align="center">
 <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_startupApp.png" width="500px">
</div>

| アイコン | 概要 |
|---|---|
| ・・・ | ユーザーのログイン情報やオフラインマップ作成・データ同期などの機能を実現する（コンテキストドロワービューを表示する） | 
| ◎ | ユーザーの現在地を表示する | 
| ＋ | マップへ新しいフィーチャを追加する | 

アイコンを利用するほかに、表示しているフィーチャをクリックすることで、属性情報の表示やアタッチメントの追加が可能となる

## ログイン方法

1. コンテキスト ドロワー ビューを開く
1. [ログイン]を選択して次を入力する
     * ユーザー
     * パスワード
1. ご自身のアカウント情報が表示される

    <div align="left">
    <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_login.png" width="500px">
    </div>

## オフラインモードを適用する

1. コンテキスト ドロワー ビューを開く
1. [オフラインモード]を選択する

    <div align="left">
    <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/offlinemode.png" width="200px">
    </div>

1. オフラインで使用するデータダウンロード格納先を指定する
1. 範囲を絞り[ダウンロード」を選択してダウンロードを開始する

    <div align="left">
    <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_startdlmap.png" width="500px">
    </div>
   
1. ダウンロードが完了するとオフラインモードとして操作できる

    <div align="left">
    <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_offlinemodemapstart.png" width="300px">
    </div>

## アタッチメント（添付ファイル）を任意のフィーチャへ追加する

1. 任意のフィーチャを選択する
1. ポップアップを開く
1. 鉛筆のマークを選択して編集用のポップアップを表示する
    <div align="left">
    <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_openeditmode.png" width="300px">
    </div>

1. 鉛筆のマークから添付ファイルを選択する

    <div align="left">
    <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_editattachiment.png" width="300px">
    </div>

1. 次の属性情報を変更する
    * Condition（tree）
1. プロッピーのマークから保存する

    <div align="left">
    <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_saveupdate.png" width="200px">
    </div>

## オフラインモードの編集データを ArcGIS Online と同期する

1. コンテキスト ドロワー ビューを開く
1. [マップの同期]を選択する

    <div align="left">
    <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_synceditdata.png" width="200px">
    </div>

## 【番外】同期結果をマップビューアーから確認する

1. アプリで利用している Web マップ にアクセスする
1. 変更したフィーチャを選択する
1. Conditionとアタッチメントが追加されている

    <div align="left">
    <img src="https://s3-ap-northeast-1.amazonaws.com/apps.esrij.com/arcgis-dev/github/img/workshop/DataCollection/dc_webmaplooking.png" width="500px">
    </div>
    
    ※アタッチメントを削除する場合は、Web マップから操作する


[手順一覧のページ](./How2SetupApp_gaiyo.md#ハンズオンの手順)に戻る

