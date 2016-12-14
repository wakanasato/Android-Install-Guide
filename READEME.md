# インストールガイド（Android）

　このインストール ガイドでは、初めて ArcGIS Runtime SDK for Android を使用してモバイル マッピング アプリケーションを構築する開発者の方に最も基本的な開発手順を紹介します。
　このインストール ガイドをお読み頂くことで、ArcGIS Runtime SDK for Android を使用したモバイル マッピング アプリケーション開発の基礎を理解することができます。

## ArcGIS Runtime SDK for Android とは

　ArcGIS Runtime SDK for Android を使うと ArcGIS の機能を Android のネイティブ アプリとして実装することができます。
この SDK には API やリファレンス、サンプルコードなどが含まれています。
詳細は [ArcGIS Runtime SDK for Android](http://www.esrij.com/products/arcgis-runtime-sdk-for-android/) をご参照ください。

## ArcGIS Runtime SDK for Android の開発環境

ここでは次の開発環境にて ArcGIS Runtime SDK for Android を用いたモバイル マッピング アプリケーションの開発手順を説明します。
開発手順を進める前に以下の開発環境をご使用のマシンにセットアップしてください。

* JDK(Java Development Kit) ※
* Android Studio
* Android 4.0.1 以降

※ JDK 5 または JDK 7 が必要です。Android 5.0 以上をターゲットとする場合は JDK 7 が必要です。

ArcGIS Runtime SDK for Android がサポートする最新の動作環境につきましては[動作環境](http://www.esrij.com/products/arcgis-runtime-sdk-for-android/environments/)をご参照ください。

## モバイル マッピング アプリケーションの開発

ここでは、ArcGIS Runtime SDK for Android を使ってモバイル マッピング アプリケーションを作成するための基本的な手順を説明します。

### プロジェクトの作成

まず Android Studio 上に新しいプロジェクトを作成します。

1.Android Studio を起動し [Start a new Android Studio project] をクリックします。すでに Android Studio のプロジェクトが開いている場合は Android Studio のメニューから [File] → [New Project] をクリックします。

![](img_android/1.StartupAndroid.png)

2.[Application name] にアプリケーションの名称を入力します。ここでは「HelloVersion100」としています。
[Company Domain] にドメインを、[Project Location] に作成するディレクトリを入力して [Next] をクリックします。
ここではドメインを「tutorials.esri.com」としています。

![](img_android/2.makeProject.png)

3.[Phone and Tablet] のみにチェックを入れ [Minimum SDK] のドロップダウン リストから 「API 16: Android 4.1」を選択して [Next] をクリックします。

![](img_android/3.choseAndroidVersion.png)

4.Activity を選択します。ここでは「Empty Activity」を選択して [Next] をクリックします。

![](img_android/4.choseActivity.png)

5.[Finish] をクリックします。

![](img_android/5.makeActivity.png)

6.以上で新しいプロジェクトが作成されます。

![](img_android/6.finish_startProject.png)

### ArcGIS Runtime SDK の設定

次に ArcGIS Runtime SDK for Android の API を使えるようにするための設定を行います。

1.まずはこのアプリケーションが使用する機能に対して権限を付与します。
Project ツールウィンドウ で「Android」を選択して「Manifests」フォルダの AndroidManifest.xml をダブルクリックして開きます。
インターネットへのアクセス許可するための Permission を追加します。使用する機能に応じて、必要な Permission を追加してください。

```
<uses-permission android:name="android.permission.INTERNET" />
<uses-feature android:glEsVersion="0x00020000" android:required="true" />
```

2.Project ツールウィンドウ で「Project」を選択して build.gradle をダブルクリックして開きます。
ArcGIS の Maven リポジトリの URL を追加します。

```
allprojects {
    repositories {
        jcenter()
        // esri arcgis maven リポジトリの追加
        maven {
            url 'https://esri.bintray.com/arcgis'
        }
    }
}
```

3.Project ツールウィンドウ で「Android」を選択して [Gradle Scripts] の下にある build.gradle (Module: app) をダブルクリックして開きます。dependencies セクション内に「compile 'com.esri.arcgisruntime:arcgis-android:100.0.0'」を追加します。

```
dependencies {
    compile 'com.esri.arcgisruntime:arcgis-android:100.0.0'
    …
}
```

4.ツールバーの [Sync Project with Gradle Files] または build.gradle を変更した後に表示されるメッセージの右にある [Sync Now] をクリックします。


これで準備が整いました。

### 地図表示の実装

ArcGIS の機能を実装する準備ができたので、アプリケーションに ArcGIS Online のベースマップを表示するための実装を加えます。

1.Project ツールウィンドウで [app] → [res] → [layout] と展開し activity_main.xml をダブルクリックして開きます。

2.左下の [Text] タブをクリックして XML 形式で開きます。TextView 部分を全て削除して以下の MapView エレメントを追加します。

```
<com.esri.arcgisruntime.mapping.view.MapView
    android:id="@+id/mapView"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent" >
</com.esri.arcgisruntime.mapping.view.MapView>
```

3.Project ツールウィンドウで [app] → [res] → [java] と展開し MainActivity クラスを ダブルクリックして開き、地図表示のためのコードを設定します。

* MainActivity クラスへ次のクラスをインポートします。

```
import com.esri.arcgisruntime.mapping.view.MapView;
import com.esri.arcgisruntime.mapping.Map;
import com.esri.arcgisruntime.mapping.Basemap;
```
* MainActivity クラスの先頭に次のクラス変数宣言を追加します。

```
private MapView mMapView;
```
* onCreate() メソッド内の setContentView() を呼び出している後に以下のコードを追加します。
このコードは、レイアウトに定義している MapView の参照を取得し、ベースマップのタイプや初期表示の範囲、縮尺レベルを設定した地図を MapView に設定します。
ここではベースマップに設定し、初期表示範囲は永田町付近を表示するようにしています。

```
mMapView = (MapView) findViewById(R.id.mapView);
Map map = new Map(Basemap.Type.TOPOGRAPHIC, 34.0405, -118.2450, 8);
mMapView.setMap(map);
```
* MainActivity クラスへ onPause() メソッド(一時停止)と onResume() メソッド(再開)を追加します。2つのメソッドへはそれぞれ次のコードを追加します。

```
@Override
protected void onPause(){
    mMapView.pause();
    super.onPause();
}
@Override
protected void onResume(){
    super.onResume();
    mMapView.resume();
}
```

* MainActivity は以下のようになります。

4.ツールバーの [Make Project] または [Build] メニューから [Make Project] をクリックします。

### モバイル マッピング アプリケーションの実行

ベースマップを表示するアプリケーションが作成できたので Android 端末にインストールして実行します。

1.ツールバーの [Run ‘app’] をクリックします。

2.接続しているデバイスを選択し [OK] をクリックします。

3.アプリケーションが起動しロサンゼルス付近の地図が表示されます。
スワイプやピンチイン/ピンチアウトで地図を移動したり拡大/縮小したりすることができます。

