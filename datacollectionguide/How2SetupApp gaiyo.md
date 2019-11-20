# Data Collection for .NET アプリ ハンズオン

<div align="center">
 <img src="https://developers.arcgis.com/example-apps/data-collection-dotnet/img/featured-img.png" width="500px">
</div>

</br>

# 概要

このドキュメントは、2019年8月に開催した [ArcGIS 開発者のための最新アプリ開発塾 2019](https://github.com/EsriJapan/workshops/tree/master/20190823_app-development-hands-on) セミナーで、[ArcGIS プラットフォームを活用した調査アプリケーション構築までのハンズオン](https://github.com/EsriJapan/workshops/blob/master/20190823_app-development-hands-on/02_ArcGIS_%E3%83%97%E3%83%A9%E3%83%83%E3%83%88%E3%83%95%E3%82%A9%E3%83%BC%E3%83%A0%E3%82%92%E6%B4%BB%E7%94%A8%E3%81%97%E3%81%9F%E8%AA%BF%E6%9F%BB%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E6%A7%8B%E7%AF%89%E3%81%BE%E3%81%A7%E3%81%AE%E3%83%8F%E3%83%B3%E3%82%BA%E3%82%AA%E3%83%B3.pdf) のセクションを実践できるように、当日の手順を画像付きで示しています。

ハンズオンでは、**街路樹診断の現地調査を行う** というシナリオを想定し、オフライン（インターネットが繋がらない）状態でも利用できるアプリを構築しました。
[ハンズオン時に使用した資料（PPT）](https://github.com/EsriJapan/workshops/blob/master/20190823_app-development-hands-on/02_ArcGIS_%E3%83%97%E3%83%A9%E3%83%83%E3%83%88%E3%83%95%E3%82%A9%E3%83%BC%E3%83%A0%E3%82%92%E6%B4%BB%E7%94%A8%E3%81%97%E3%81%9F%E8%AA%BF%E6%9F%BB%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E6%A7%8B%E7%AF%89%E3%81%BE%E3%81%A7%E3%81%AE%E3%83%8F%E3%83%B3%E3%82%BA%E3%82%AA%E3%83%B3.pdf)から当日の資料をご覧いただけます。


このドキュメントでは、ハンズオンに必要なマテリアルを提供しています。開発環境のみご自身でご準備いただき、ぜひ実践してみましょう。

# ハンズオンで使用するマテリアル

このハンズオンで使用するものは次の 4 つです

* ArcGIS for Developers（開発者アカウント）：ご準備ください
* Visual Studio 2017：ご準備ください
* サンプルプロジェクト（Data Collection for .NETアプリ）
* ダミーデータ

ローカライズ済みのサンプルプロジェクト及びダミーデータは [HandsOn_Data.zip](https://github.com/EsriJapan/workshops/raw/master/20190823_app-development-hands-on/HandsOn_Data.zip) からダウンロードできます。</br>
HandsOn_Data.zip を解凍すると以下の構成となっています。

| HandsOn_Data フォルダ配下 | 格納ファイルまたはプロジェクト | 備考 |
|---|---|---|
| 02_Data_Collection_Application | 190823_dev_school.ipynb | ここでは使用しません  |
|  | tree_inspection.gdb.zip | **使用します：ダミーデータ**  |
|  | data-collection-dotnet-master_ejLocalized | **使用します：サンプルプロジェクト**  |
| 03_Widget_Development  | 190823_dev_school.ipynb  | ここでは使用しません  |

ArcGIS for Developers（開発者アカウント）をお持ちでない方は「[開発者アカウントの作成](http://esrijapan.github.io/arcgis-dev-resources/guide/create-map/get-dev-account/)」から作成して、ご準備ください。アカウントは無償で作成できます。


# ハンズオンの手順

提供しているマテリアルを使用して、ハンズオンは次の順番で作業します。

 1. [アプリで使用する地図データの作成]()
 1. [地図データを反映した Data Collection for .NETアプリの実行]()
 1. [アプリの操作方法]()

（※別ページにリンクしてます）

## ハンズオンで使用したアプリについて

ハンズオンで使用したアプリは、米国Esri 社が GitHub で公開する *[Data Collection for .NET](https://developers.arcgis.com/example-apps/data-collection-dotnet/)* 
アプリを元に、ESRIジャパンにてローカライズしたものです。改修も行っており、フィーチャに対して画像を添付できる機能を追加しています。
アプリの技術的な仕様や改修内容については、次の内容をそれぞれご参照ください。

 * [アプリの仕様について（詳細）]()
 * [【応用】コード拡張]()

米国Esri社が公開する、[Data Collection for .NET](https://developers.arcgis.com/example-apps/data-collection-dotnet/) のページおよび [GitHub ソース](https://github.com/Esri/data-collection-dotnet)についてもぜひご参照ください。