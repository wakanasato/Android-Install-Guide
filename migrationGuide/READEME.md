# �A�v���P�[�V�����̈ڍs�iAndroid�j
## �ڍs�K�C�h�ɂ���

���̈ڍs�K�C�h�́A���܂� ArcGIS Runtime SDK for Android �o�[�W���� 10.2.x ���g�p���ăA�v���P�[�V�������J������Ă����J���Ҍ����̃K�C�h�ł��B

ArcGIS Runtime SDK �o�[�W���� 100.x �͐V�����A�[�L�e�N�`�����g�p���ă[������J�����ꂽ������� ArcGIS Runtime �ł��B���̃o�[�W�����A�b�v�ɔ��� API �̍Đ݌v���s�Ȃ��Ă��܂��B���̃h�L�������g�ł́A�o�[�W���� 100.x �̕ύX�_�ɂ��Đ������܂��B

ArcGIS Runtime SDK for Android �Ɋւ��ẮA[ESRI�W���p�� ���i�y�[�W](https://www.esrij.com/products/arcgis-runtime-sdk-for-Android)�����Q�Ƃ��������B

�ȉ��́A�o�[�W���� 100.x �̎�ȕύX�_�ł��B

* __[Gradle�t�@�C���̕ύX](#Gradle �Q�ƃv���W�F�N�g�̕ύX)__
* __[�}�b�v�ƃV�[��](#�}�b�v�ƃV�[��)__
* __[�r���[](#�r���[)__
* __[���C���[ �N���X���̕ύX](#���C���[-�N���X���̕ύX)__
* __[�t�B�[�`�� ���C���[�̕\��](#�t�B�[�`��-���C���[�̕\��)__
* __[�t�B�[�`���̑���](#�t�B�[�`���̑���)__
* __[�ʑ����\��](#�ʑ����\��)__
* __[�O���t�B�b�N�X �I�[�o�[���C](#�O���t�B�b�N�X-�I�[�o�[���C)__
* __[�W�I���g���ƃW�I���g�� �r���_�[](#�W�I���g���ƃW�I���g��-�r���_�[)__
* __[�X�P�b�` �G�f�B�^�[](#�X�P�b�`-�G�f�B�^�[)__
* __[���[�_�u�� �p�^�[��](#���[�_�u��-�p�^�[��)__
* __[�u���b�N���g�p�����񓯊��v���O���~���O](#�u���b�N���g�p�����񓯊��v���O���~���O)__
* __[���m�̐�������](#���m�̐�������)__

## Gradle �Q�ƃv���W�F�N�g�̕ύX

Android Studio �̃r���h �c�[���� Gradle ���g�p���Amaven���|�W�g���ƃ��C�u�����̎Q�Ƃ�ύX���܂��B

```
    repositories {
        jcenter()
        maven {
            url 'https://esri.bintray.com/arcgis'
        }
    }
    dependencies {
        compile 'com.esri.arcgisruntime:arcgis-android:100.0.0'
    }
```

ArcGIS Runtime SDK for Android ���T�|�[�g����ŐV�̓�����́A[ESRI�W���p�� ���i�y�[�W�i������j](https://www.esrij.com/products/arcgis-runtime-sdk-for-Android/environments/)�����Q�Ƃ��������B


## �}�b�v�ƃV�[��

100.x �ł́A`AGSMap` �I�u�W�F�N�g�i2D�\���p�j�� `AGSScene` �I�u�W�F�N�g�i3D�\���p�j<sup>��1</sup> �� API �̃R�A�Ƃ��āAArcGIS �v���b�g�t�H�[���� Web GIS �@�\��v���ɗ��p�ł���悤�ɂȂ�܂����B

`AGSMap` �I�u�W�F�N�g�� `AGSScene` �I�u�W�F�N�g�� �A������\������ View �ƕ�������Ă��܂��B`AGSMap` �I�u�W�F�N�g�� `AGSScene` �I�u�W�F�N�g�ɂ� �A���샌�C���[�A�x�[�X�}�b�v�A�u�b�N�}�[�N���� ArcGIS �ŗL�̃f�[�^��ݒ�ł��A�A�v���P�[�V�����ŗ��p���邱�Ƃ��ł��܂��B

<sup>��1</sup> �o�[�W����100.0 �ł́A3D �֘A�̋@�\�̓x�[�^�@�\�Ƃ��Ē񋟂���Ă��܂�

## �r���[

`AGSMapView`�i2D�\���p�j�� `AGSSceneView`�i3D�\���p�j�́AUI �R���|�[�l���g�ł��B`AGSMapView` �N���X�� `map` �v���p�e�B�ɁA`AGSMap` �I�u�W�F�N�g���A`AGSMapSceneView` �N���X�� `scene` �v���p�e�B�ɂ� `AGSScene` �I�u�W�F�N�g��ݒ肵�܂��B

100.x �ł́A�ȉ��̂悤�Ƀ}�b�v��\�����܂��B
```javascript
// �x�[�X�}�b�v���w�肵�ă}�b�v��������
let map = AGSMap(basemap:AGSBasemap.imagery())
// �}�b�v�r���[�Ƀ}�b�v��ݒ�
self.mapView.map = map
```

## ���C���[ �N���X���̕ύX

�e���C���[�̃N���X�����ȉ��̂悤�ɕύX����Ă��܂��B

|���C���[|10.2.x �̃N���X��|100.x �̃N���X��|
|:--:|:--:|:--:|
|ArcGIS Server �_�C�i�~�b�N �}�b�v �T�[�r�X ���C���[|AGSDynamicMapServiceLayer|AGSArcGISMapImageLayer|
|�^�C�� �}�b�v �T�[�r�X ���C���[|AGSTiledMapServiceLayer|AGSArcGISTiledLayer|
|�^�C�� �p�b�P�[�W ���C���[|AGSLocalTiledLayer|AGSArcGISTiledLayer|

���o�[�W������ 100.0 �ł́A10.2.x �Œ񋟂���Ă����A�ȉ��̃��C���[���T�|�[�g����Ă��܂���̂ŁA�����ӂ��������B
* WMS �T�[�r�X ���C���[�i`AGSWMSLayer`�j
* WMTS �T�[�r�X ���C���[�i`AGSWMTSLayer`�j
* OpenStreetMap ���C���[�i`AGSOpenStreetMapLayer`�j
* Bing Maps ���C���[�i`AGSBingMapLayer`�j
* Web �^�C�� ���C���[�i`AGSWebTiledLayer`�j

100.x �ŃT�|�[�g����Ă��郌�C���[�̎�ނɂ��ẮA[ArcGIS Runtime SDK for Android: ���C���[�i�p��j](https://developers.arcgis.com/Android/latest/swift/guide/layers.htm)�����Q�Ƃ��������B

�쐬�����e���C���[�́A�ȉ��̕��@�Ń}�b�v�ɒǉ����܂��B
```javascript
// ���샌�C���[�Ƃ��ă}�b�v�ɒǉ�����
self.map.operationalLayers.addObject(arcgis_map_image_layer)

// �x�[�X�}�b�v�Ƃ��ă}�b�v�ɒǉ�����
self.map.basemap = AGSBasemap(baseLayer: arcgis_tiled_layer)
```


## �t�B�[�`�� ���C���[�̕\��

�t�B�[�`�� �T�[�r�X��[���̃��[�J���Ɋi�[���ꂽ�W�I�f�[�^�x�[�X�̃f�[�^���}�b�v�ɕ\������ɂ̓t�B�[�`�� ���C���[���g�p���܂��B
�t�B�[�`�� ���C���[��\������ɂ́A�͂��߂Ƀt�B�[�`�� �e�[�u�����쐬���܂��i�t�B�[�`�� �T�[�r�X�̃f�[�^���t�B�[�`�� ���C���[�ŕ\������ꍇ�� `AGSArcGISFeatureTable` �I�u�W�F�N�g�A�W�I�f�[�^�x�[�X�̃f�[�^��\������ꍇ�� `AGSGeodatabaseFeatureTable` �I�u�W�F�N�g���g�p���܂��j�B���ɍ쐬�����t�B�[�`�� �e�[�u���������Ƃ��� `AGSFeatureLayer` �I�u�W�F�N�g���쐬���A`AGSMap` �I�u�W�F�N�g�� `OperationalLayers` �ɒǉ����܂��B

���̃R�[�h�́A�t�B�[�`�� �T�[�r�X�̃f�[�^�� `AGSFeatureLayer` �Ƃ��ă}�b�v�ɒǉ�������@�������Ă��܂��B

```javascript
// �t�B�[�`�� �T�[�r�X�� URL ����t�B�[�`�� �e�[�u�����쐬
let featureTable = AGSServiceFeatureTable(url: URL(string: "https://services.arcgis.com/wlVTGRSYTzAbjjiC/arcgis/rest/services/all_Japan_shikuchoson/FeatureServer/0")!)
// �t�B�[�`�� �e�[�u������t�B�[�`�� ���C���[���쐬
let featureLayer = AGSFeatureLayer(featureTable: featureTable)
// �t�B�[�`�� ���C���[���}�b�v�̑��샌�C���[�ɒǉ�
self.map.operationalLayers.add(featureLayer)
```

## �t�B�[�`���̑���

�t�B�[�`���̌�����ҏW�̓t�B�[�`�� �e�[�u�� �i`AGSArcGISFeatureTable` �܂��� `AGSGeodatabaseFeatureTable`�j�ɑ΂��čs���܂��B

�t�B�[�`�� �T�[�r�X����쐬�����t�B�[�`�� �e�[�u���i`AGSArcGISFeatureTable`�j�̏ꍇ�A�t�B�[�`�� �e�[�u���̃t�B�[�`���́A�}�b�v��Ƀ����_�����O���邽�߂ɕK�v�ŏ����̏�񂾂����܂ނ悤�ɍœK������Ă��܂��B����ɂ��A�t�B�[�`����\�����邽�߂̑ҋ@���ԂƑш敝�̏���팸����܂��B�t�B�[�`���̕ҏW�₷�ׂĂ̑�������\������悤�ȏꍇ�͊��S�ȏ����擾���邽�߂ɁA[���[�_�u�� �p�^�[��](#���[�_�u��-�p�^�[��)�����g�p���āA�t�B�[�`���𖾎��I�Ƀ��[�h���Ă����K�v������܂��B


#### �t�B�[�`���̃��N�G�X�g ���[�h
�t�B�[�`�� �T�[�r�X����t�B�[�`�����擾����ꍇ�́A
���N�G�X�g ���[�h�̐ݒ�ɂ���ăt�B�[�`���̎擾�p�x�Ƃ�[����ł̃f�[�^�̃L���b�V�����@�𐧌䂵�܂��B���N�G�X�g ���[�h�ɂ́A`OnInteractionCache`�A `OnInteractionNoCache`�A`ManualCache` ������܂��B���N�G�X�g ���[�h�̓t�B�[�`�� �e�[�u���������������O�ɁA`AGSServiceFeatureTable` �� `featureRequestMode` �v���p�e�B���g�p���Đݒ�ł��܂��B

* `OnInteractionCache`: ���[�U�[�̑���ɂ��}�b�v�̕\���̈悪�ύX�����ƁA�t�B�[�`���������I�Ƀ��N�G�X�g����܂��B���N�G�X�g���ꂽ���ׂẴf�[�^�̓��[�J���ɃL���b�V������܂��B�f�[�^���L���b�V�����ꃋ���߁A���ɕ\�����ꂽ�̈�Ƀ}�b�v���ړ����Ă��A�ēx�t�B�[�`���̓��N�G�X�g����܂���B�T�[�o�[��̃f�[�^���ύX�����\�������Ȃ��ÓI�ȃf�[�^�ɓK�������[�h�ł��B
* `OnInteractionNoCache`: ���[�U�[�̑���ɂ��}�b�v�̕\���̈悪�ύX�����ƁA�t�B�[�`���������I�Ƀ��N�G�X�g����܂����A�L���b�V���͂���܂���B���ɕ\�����ꂽ�̈�Ƀ}�b�v���ړ�����ƁA�ēx�t�B�[�`�������N�G�X�g����܂��B�T�[�o�[��̃f�[�^���p���I�ɍX�V�����\��������ꍇ�ɓK�������[�h�ł��B
* `ManualCache`: ���[�U�[�ɂ��}�b�v����ł́A�t�B�[�`���͎����I�Ƀ��N�G�X�g����܂���B���̃��[�h���g�p����ꍇ�́A`AGSServiceFeatureTable` �� `populateFromService` ���\�b�h���g�p���Ė����I�Ƀf�[�^�����N�G�X�g����K�v������܂��B

  �ȉ��̃R�[�h�� `populateFromService` ���\�b�h���g�p���āA�T�[�o�[��̂��ׂẴt�B�[�`�����擾������@�̗�ł��B

  ```javascript
// �t�B�[�`���̌����p�����[�^�[��ݒ�
let params = AGSQueryParameters()
// ���ׂẴt�B�[�`�����擾����悤�ɏ�����ݒ�
params.whereClause = "1 = 1"
// �������ʂɃt�B�[�`���̂��ׂĂ̑������ioutFields �̔z��� "*" ���w��j���܂߂�
self.featureTable.populateFromService(with: params, clearCache: true, outFields: ["*"]) {(result, error) -> Void in
   if let error = error {
       // �t�B�[�`���̎擾�Ɏ��s
       print("Error:\(error.localizedDescription)")
   } else {
     �@// �t�B�[�`���̎擾�ɐ����i�t�B�[�`������\���j
       print(result?.featureEnumerator().allObjects.count ?? "0")
   }
}
```

���N�G�X�g ���[�h�̏ڍׂ́A
[ArcGIS Runtime SDK for Android: �t�B�[�`�� ���N�G�X�g ���[�h�i�p��j](https://developers.arcgis.com/Android/latest/swift/guide/layers.htm#GUID-925AD533-12E7-4E93-AB88-3F9577906818)�����Q�Ƃ��������B


#### �t�B�[�`���̕ҏW
�t�B�[�`���̕ҏW�̓t�B�[�`�� �e�[�u���ɑ΂��čs���܂��B�t�B�[�`�� �T�[�r�X�܂��̓W�I�f�[�^�x�[�X�̃f�[�^����쐬�����t�B�[�`�� �e�[�u���̂ǂ����ҏW����ꍇ���������@�ɈႢ�͂���܂���B

�t�B�[�`���̕ҏW���@�́A
[ArcGIS Runtime SDK for Android: �t�B�[�`���̕ҏW�i�p��j](https://developers.arcgis.com/Android/latest/swift/guide/edit-features.htm)�����Q�Ƃ��������B

#### �t�B�[�`���̌���
�t�B�[�`���̌����̓t�B�[�`�� �e�[�u���ɑ΂��čs���܂��B�t�B�[�`�� �T�[�r�X�܂��̓W�I�f�[�^�x�[�X�̃f�[�^����쐬�����t�B�[�`�� �e�[�u���̂ǂ����ҏW����ꍇ���������@�ɈႢ�͂���܂���B�������s���ɂ�
`AGSArcGISFeatureTable` �܂��� `AGSGeodatabaseFeatureTable` �N���X�� `queryFeaturesWithParameters` ���\�b�h���g�p���܂��B

���̃R�[�h�́A�t�B�[�`�� �T�[�r�X����쐬�����t�B�[�`�� �e�[�u������t�B�[�`��������������@�������Ă��܂��B
```javascript
featureTable.queryFeatures(with: queryParameters, fields: .loadAll, completion:{ (result, error) -> Void in
           if let error = error {   
               print("Error:\(error.localizedDescription)")
           } else {
               let enumr = result?.featureEnumerator()
               for feature in enumr! {
                   // �������ʂ̃t�B�[�`�����擾
                   let feature = feature as! AGSArcGISFeature
               }
           }
       })
```

## �ʑ����\��

�}�b�v��œ���̏ꏊ���^�b�v���āA���̈ʒu�ɂ���t�B�[�`�������ׂẴ��C���[���猟�����Ď擾���邱�Ƃ��ł��܂��B���̑���̓r���[�ɑ΂��čs���܂��B���̃R�[�h�́A`AGSMapView` �N���X�� `identifyLayers` ���\�b�h���g�p���ăt�B�[�`�����擾������@�������Ă��܂��B
```javascript
self.mapView.identifyLayers(atScreenPoint: screenPoint, tolerance: 10, returnPopupsOnly: true, completion: { (results, error)  -> Void in
    if let error = error {
        print(error)
    } else {
        for identifyLayerResult in results! {
            for geoElement in identifyLayerResult.geoElements {
                // AGSGeoElement �I�u�W�F�N�g�̎擾
            }
        }
    }
})
```

## �O���t�B�b�N�X �I�[�o�[���C

�O���t�B�b�N�́A�}�b�v��Ɉꎞ�I�ȃf�[�^��\�����邽�߂Ɏg�p����܂��B`AGSMapView` �� `AGSSceneView` �I�u�W�F�N�g�ɂ̓O���t�B�b�N��\�����邽�߂̃O���t�B�b�N�X �I�[�o�[���C�i`AGSGraphicsOverlay`�j���܂܂�Ă��܂��B
�O���t�B�b�N�X �I�[�o�[���C���g�p���邱�ƂŁA�}�b�v��̃��C���[�̏������ύX����Ă��A�O���t�B�b�N����ɍŏ�ʂɕ\������܂��B�ڍׂ́A[ArcGIS Runtime SDK for Android: �O���t�B�b�N�X �I�[�o�[���C�̒ǉ��i�p��j](https://developers.arcgis.com/Android/latest/swift/guide/add-graphics-overlays-to-your-app.htm)�����Q�Ƃ��������B

���̃R�[�h�́A`AGSMapView` �I�u�W�F�N�g�ɁA�O���t�B�b�N�X �I�[�o�[���C���g�p���ăO���t�B�b�N��ǉ�������@�������Ă��܂��B

```javascript
// �W�I���g���ƃV���{����ݒ肵�ăO���t�B�b�N���쐬
let pointGraphic = AGSGraphic(geometry: pointGeometry, symbol: poitnSymbol, attributes: nil)
// �O���t�B�b�N�X �I�[�o�[���C�ɍ쐬�����O���t�B�b�N��ǉ�
let graphicsOverlay = AGSGraphicsOverlay()
graphicsOverlay.graphics.add(pointGraphic)
// AGSMapView �� GraphicsOverlays �ɍ쐬�����O���t�B�b�N�X �I�[�o�[���C��ǉ�
self.mapView.graphicsOverlays.add(graphicsOverlay)
```

## �W�I���g���ƃW�I���g�� �r���_�[

`AGSGeometry` �I�u�W�F�N�g�̃R���X�g���N�^���g�p����ƁA���m�̍��W���g�p���ăW�I���g�����쐬�ł��܂����A�쐬��ɂ��̃W�I���g����ύX���邱�Ƃ͂ł��܂���B

�W�I���g�� �r���_�[�i`AGSGeometryBuilder`�j���g�p����ƁA�[������V�����W�I���g�����쐬������A�����̃W�I���g������ɁA�W�I���g����ύX���邱�Ƃ��ł��܂��B�ڍׂ́A[ArcGIS Runtime SDK for Android: �W�I���g���̕ҏW�i�p��j](https://developers.arcgis.com/Android/latest/swift/guide/edit-geometries.htm)�����Q�Ƃ������� �B

## �X�P�b�` �G�f�B�^�[
�X�P�b�` �G�f�B�^�[�i`AGSSketchEditor`�j���g�p����ƁA���[�U�[���}�b�v��őΘb�I�ɃW�I���g�����X�P�b�`���邱�Ƃ��ł��܂��B

���̃R�[�h�́A`AGSSketchEditor` �̎g�p���@�̗�������Ă��܂��B

```javascript
// �}�b�v �r���[�ɃX�P�b�` �G�f�B�^�[��ݒ�
self.sketchEditor = AGSSketchEditor()
self.mapView.sketchEditor =  
// �W�I���g���̎�ނ�ݒ肵�ăX�P�b�`���J�n
self.sketchEditor
self.sketchEditor.start(with: AGSGeometryType.polygon)
// �X�P�b�`���̃W�I���g���̍X�V���Ď�
NotificationCenter.default.addObserver(self, selector: #selector(ViewController.respondToGeometryChanged), name: NSNotification.Name.AGSSketchEditorGeometryDidChange, object: nil)

�E�E�E�E�E�E

func respondToGeometryChanged() {
  // �W�I���g�����X�V���ꂽ�ۂ̏���
}
```

## ���[�_�u�� �p�^�[��

�f�[�^��񓯊��Ń��[�h���ď�Ԃ�����������}�b�v�⃌�C���[���̃��\�[�X�́A���[�_�u�� �p�^�[�����̗p����Ă��܂��B�e���\�[�X�̃v���p�e�B�ɃA�N�Z�X����ɂ́A���[�_�u�� �p�^�[�����g�p���āA���\�[�X�����[�h���ꂽ��ɃA�N�Z�X���邱�Ƃ���������܂��B���[�_�u�� �p�^�[���́A���[�h��Ԃ̐U�镑�������ψ�ɂ��Ċ���ѐ����������邱�ƂŁA�񓯊�������薾���I�ɂ��܂��B���[�_�u�� �p�^�[���ł́A�e���\�[�X�͎����I�Ƀ��\�[�X�̏�Ԃ����[�h���܂���B�����́A�J���҂������I�Ɏ��s�����Ƃ��ɁA�x�����[�h���܂��B
�e���\�[�X�̏�Ԃ́A`NotLoaded�i���[�h���J�n���Ă��Ȃ�`�A`Loading�i���[�h���j`�A`Loaded�i���[�h�ɐ����j`�A`FailedToLoad�i���[�h�Ɏ��s�j` �̂����ꂩ�ŊĎ����邱�Ƃ��ł��܂��B

�ڍׂ́A[ArcGIS Runtime SDK for Android: ���[�_�u�� �p�^�[���i�p��j](https://developers.arcgis.com/Android/latest/swift/guide/loadable-pattern.htm)�����Q�Ƃ��������B

���̃R�[�h�́A���[�_�u�� �p�^�[���̊�{�I�Ȏg�p���@�̗�������Ă��܂��B
```javascript
self.featureLayer.load(completion: {(error) -> Void in
    if let error = error {
        print(error)
    }else {
        // �t�B�[�`�� ���C���[�̃��[�h�ɐ���
    }
})
```

## �u���b�N���g�p�����񓯊��v���O���~���O

�񓯊���������s���郁�\�b�h�́A�����u���b�N�������Ƃ��Ď󂯎��܂��B�u���b�N�͑��삪����Ɋ��������Ƃ��A�܂��́A�G���[�����������Ƃ��ɌĂяo����܂��B���삪��������ƁA���̑���̌��ʂ��u���b�N�ɓn����܂��B����ȊO�̏ꍇ�̓G���[���n����܂��B
����́A�f���Q�[�g���g�p���Ċe�񓯊�����̌��ʂƃG���[���n���h�����O���Ă��� 10.2.x �̃v���O���~���O���@��u�������܂��B

���̃R�[�h�́A��Ƃ��Ē[���� GPS �̈ʒu���̎擾�J�n�̑��쌋�ʂ��n���h�����O������@�������Ă��܂��B
```javascript
self.mapView.locationDisplay.start(completion: { (error) -> Void in
  if let error = error {
    // GPS �̈ʒu���̎擾�Ɏ��s
    print("Error:\(error.localizedDescription)")
  } else {
    // GPS �̈ʒu���̎擾�ɐ���
  }
})
```
## ���m�̐�������
���o�[�W���� 100.0 �ł̊��m�̐����������A[ArcGIS Runtime SDK for Android: �����[�X �m�[�g�i�p��j](https://developers.arcgis.com/Android/latest/swift/guide/release-notes.htm#GUID-2D204730-60B6-4004-BCB1-63F654F70AA3)�ɋL�ڂ���Ă��܂��̂ŁA���Q�Ƃ��������B

## �֘A�����N
* [ArcGIS Runtime SDK for Android: �����[�X �m�[�g�i�p��j](https://developers.arcgis.com/Android/latest/swift/guide/release-notes.htm)
