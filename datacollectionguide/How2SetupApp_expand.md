# 【応用】コード拡張

米国Esri社で公開している [Data Collection for .NET](https://developers.arcgis.com/example-apps/data-collection-dotnet/) は、オープンソースであるためご自身で開発することにより機能を拡張し利用することができます。</br>
[HandsOn_Data.zip](https://github.com/EsriJapan/workshops/raw/master/20190823_app-development-hands-on/HandsOn_Data.zip) で提供しているサンプルプロジェクトでは、アプリ内でアタッチメント追加機能（各フィーチャに画像ファイル情報を追加する）を実装しています。

アタッチメント追加機能の実装方法を以下で解説します。

* [プロジェクト概要](#プロジェクト概要)
* [アタッチメント機能追加の実装内容](#アタッチメント機能追加の実装内容)


## プロジェクト概要

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

## アタッチメント機能追加の実装内容

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

## IdentifiedFeaturePopup.xaml

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

##  **IdentifiedFeatureViewModel.cs**

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


[手順一覧のページ](./How2SetupApp_gaiyo.md#ハンズオンの手順)に戻る

