# Data Collection for .NET アプリ

<div align="center">
 <img src="https://developers.arcgis.com/example-apps/data-collection-dotnet/img/featured-img.png" width="500px">
</div>

</br>

# 概要

このドキュメントでは、米国ESRIがオープンソースとして提供している [Data Collection for .NET](https://developers.arcgis.com/example-apps/data-collection-dotnet/) アプリについてご紹介します。

## Data Collection for .NET アプリとは

ArcGIS プラットフォームを使用して、現地調査に活用できるサンプルアプリケーションです。アプリはRuntime SDK for .NET を使用して構築されおり、オンライン/オフラインどちらのネットワーク状況で使用したい場合でも対応できます。
オフラインでも使用できる仕組みについては、[サービス連携パターン](https://www.esrij.com/products/arcgis-runtime-sdk-for-dotnet/details/offline-apps/patterns/)をご参照ください。

## 使用方法（開発時）

アプリを使用するためには、アプリが参照するデータ作成および、統合開発環境（Visual Studio 2017）が必要です。</br>
以下の順番で設定方法・実行方法を解説します。作業用のデータとサンプルコードを提供しており、これらのデータやコードに沿って解説します。次のセクションからダウンロードしてご利用ください。

 * [地図データの作成]()
 * [アプリの実行]()
 * [アプリの使い方](#pend)

    特筆すべきアプリの仕様や ESRI ジャパンでの拡張内容については、以下をご参照ください。

    * [アプリの仕様について（詳細）]()
    * [【応用】コード拡張]()

## 準備するもの

このドキュメントで解説に使用するデータおよびソースコードは、ESRIジャパンでローカライズ・拡張したコードを使用します。

このハンズオンで使用するものは次の4つです

* ArcGIS for Developers（開発者アカウント）：ご準備ください
* Visual Studio 2017：ご準備ください
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

ArcGIS for Developers（開発者アカウント）をお持ちでない方は「[開発者アカウントの作成](http://esrijapan.github.io/arcgis-dev-resources/guide/create-map/get-dev-account/)」から作成して、ご準備ください。アカウントは無償で作成できます。

ローカライズしていないデータを入手したい場合は、米国ESRIのGitHubからご利用ください。


### ハンズオン実施しました

2019年8月に開催した [ArcGIS 開発者のための最新アプリ開発塾 2019](https://github.com/EsriJapan/workshops/tree/master/20190823_app-development-hands-on) セミナーでは、[ArcGIS プラットフォームを活用した調査アプリケーション構築までのハンズオン](https://github.com/EsriJapan/workshops/blob/master/20190823_app-development-hands-on/02_ArcGIS_%E3%83%97%E3%83%A9%E3%83%83%E3%83%88%E3%83%95%E3%82%A9%E3%83%BC%E3%83%A0%E3%82%92%E6%B4%BB%E7%94%A8%E3%81%97%E3%81%9F%E8%AA%BF%E6%9F%BB%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E6%A7%8B%E7%AF%89%E3%81%BE%E3%81%A7%E3%81%AE%E3%83%8F%E3%83%B3%E3%82%BA%E3%82%AA%E3%83%B3.pdf) のセクションで、このドキュメントの内容を実施しました。</br>

上記のドキュメントもぜひご参照ください。


## 使用方法（運用時）

アプリは
[Data Collection for .NET](https://developers.arcgis.com/example-apps/data-collection-dotnet/) アプリはオープンソースで提供されているため、そのまま業務で使用することが可能です。
その場合は、ArcGIS Runtime SDK で開発したアプリの機能に沿って、ライセンスをご購入いただきます。内容は、弊社の開発製品[ライセンスページ](https://www.esrij.com/products/arcgis-runtime-sdk-for-dotnet/details/license/)をご覧ください。

※開発・検証は無償～ご利用いただけます。