
##resas2arcgis を使ってみようハンズオン

  1.	ArcGIS for Developers アカウント作成(事前)※未作成者は受付時対応

  以下のサイトから [Get a Free Account] をクリックします(登録にはメールアドレスが必要です)。<br>
  <https://developers.arcgis.com/>

  1.	シェープファイルをダウンロード(ArcGIS Open Data フィルタリング)
 
  オープンデータ カタログ サイトの [ArcGIS Open Data](http://opendata.arcgis.com/)から市区町村の境界データをダウンロードします。<br>
  [全国市区町村界データ](http://arcg.is/2iTeKD9)のページにアクセス。<br>
  選んだ都道府県でフィルタリングをしてシェープファイルでダウンロードします。

  1.	シェープファイルを ArcGIS Online にホスト(フィーチャ レイヤー作成)
 
  [ArcGIS のページ](https://www.arcgis.com/home/)にアクセスして、ステップ１で作成したアカウントでサイン インします。<br>
　ページ上部の [マイ コンテンツ] を選択後、[アイテムの追加] でローカルのシェープファイルをアップロードします。<br>
　※「このファイルをホストレイヤーとして公開します」にチェックが入っていることを確認してください！

  1.	公開設定

  アップロードするとアイテム ページが開きます。ページ右の [共有] をクリックして、アクセス権を [すべての人に公開 (パブリック)] に変更します。

  1.	編集可能設定

  そのままアイテム ページの [設定] タブを開きます。[Feature Layer (ホスト) 設定] の「編集の有効化」にチェックを入れます。<br>
  これで API 経由でのデータ入力が可能になります。

  1.	フィーチャ レイヤーの REST エンドポイント URL の取得(コピー)

  [概要] タブに戻り、「レイヤー」セクションにある [サービスの URL] をクリックします。<br>
  このリンク先の URL が ArcGIS の REST エンドポイントになるので、メモしておきます。

  1.	フィールド追加(RESAS データの入力先)

  フィーチャ レイヤーの属性テーブルに RESAS データを入力するためのフィールド(カラム)を新規追加します。<br>
  [概要] タブに戻り、[マップ ビューアーで開く] をクリックして、マップ ビューアーを開きます。<br>
  画面左の [コンテンツ] 上のレイヤー名にカーソルを合わせて、テーブル アイコンをクリックして属性テーブルを開きます。<br>
  テーブル上部の [オプション] > [フィールドの追加] を選択して、RESAS データを入力するフィールドを追加します。

  1.	resas2arcgis(Heroku)アクセス先

  resas2arcgis のサービスへ接続するために、以下のURLへアクセスします。<br>
  <https://resas2arcgis.herokuapp.com>

  1.	resas2arcgis(Heroku)パラメーター入力

  RESAS API のデータをArcGIS の指定のフィーチャ レイヤーに入力するために、以下のパラメータを入力します。

   *	RESAS API URL：入力したデータのRESAS API のURLを指定します。
   *	RESAS Mapping field：ArcGIS のフィーチャ レイヤーへ入力したい、RESAS データのフィールド名を入力します。
   *	RESAS API Key　：RESAS API を使用するためのKey (個人で取得)を入力します。
   *	ArcGIS Online Feature Layer：ArcGIS の　フィーチャ レイヤーのURLを入力します。取得方法は[7.フィーチャ レイヤー](#)の REST エンドポイント URL の取得(コピー)を参照してください。
   *	Specified RESAS API Data hierarchy：RESAS API のデータ内の階層を入力します。フィーチャレイヤーへ入力したいデータの階層を指定します。
   *	Specified ArcGIS Feature Layer field : unique Field：RESAS API のデータとマッピングさせたいArcGIS フィーチャ レイヤーのフィールド名を入力します。
   *	Specified ArcGIS Feature Layer field : new Data Filed :　ArcGIS のフィーチャレイヤーで新たに更新したいフィールドを指定します。

  1.	実行

  画面下部の[転送]ボタンを押下します。

  1.	データの追加の確認(テーブルを見る)

  アイテム ページに戻り、[データ] タブを開きます。<br>
  属性テーブルを閲覧し、入力したデータが追加されているか確認してみてください。

  1.	(ビジュアライズ)※デモのみです。もくもくタイムにトライしてみてください。

  参考ページ：<br>
  [ArcGIS Online 上のデータを可視化するための方法](http://bit.ly/2jnqSZi)<br>
  [データ可視化のワークフロー](http://bit.ly/2k6EI2Y)

