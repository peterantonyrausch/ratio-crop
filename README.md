# RatioCrop
Take or select picture, crops images with aspect ratio and get base64.

### Installation
1. Install the Cordova and Ionic Native plugins:
```
$ ionic cordova plugin add cordova-plugin-camera
$ npm install --save @ionic-native/camera

$ ionic cordova plugin add cordova-plugin-ratio-crop
$ npm install --save ionic-cordova-plugin-ratio-crop

$ ionic cordova plugin add com-badrit-base64
$ npm install --save @ionic-native/base64
```

2. Add plugins to _providers_ section on your app's module
```js
import { RatioCrop } from 'ionic-cordova-plugin-ratio-crop';
import { Base64 } from '@ionic-native/base64';
import { Camera } from '@ionic-native/camera';

...

@NgModule({
  declarations: [
    MyApp
  ],
  imports: [
    ...
  ],
  bootstrap: [IonicApp],
  entryComponents: [
    MyApp
  ],
  providers: [
    ...
    Camera,
    RatioCrop,
    Base64,
    ...
  ]
})
export class AppModule { }
```

### Supported platforms
* Android
* iOS

### Usage

```js
import { Camera } from '@ionic-native/camera';
import { RatioCrop, RatioCropOptions } from 'ionic-cordova-plugin-ratio-crop';
import { Base64 } from '@ionic-native/base64';

...

private cropOptions: RatioCropOptions = {
    quality: 75,
    targetWidth: 1080,
    targetHeight: 1080,
    widthRatio: -1,
    heightRatio: -1
  };

... 

constructor(
    private camera: Camera,
    private crop: RatioCrop,
    private base64: Base64) { }

...

takePicture() {
    return this.camera.getPicture({
      destinationType: this.camera.DestinationType.FILE_URI,
      encodingType: this.camera.EncodingType.JPEG,
      mediaType: this.camera.MediaType.PICTURE,
      sourceType: this.camera.PictureSourceType.CAMERA,
      allowEdit: false,
      correctOrientation: true
    })
      .then((fileUri) => {
        return this.crop.ratioCrop(fileUri, this.cropOptions);
      })
      .then((path) => {
        return this.base64.encodeFile(path);
      })
  }

  selectPicture() {
    return this.camera.getPicture({
      allowEdit: false,
      sourceType: this.camera.PictureSourceType.PHOTOLIBRARY,
      mediaType: this.camera.MediaType.PICTURE,
      destinationType: this.camera.DestinationType.FILE_URI
    })
      .then((fileUri) => {
        return this.crop.ratioCrop(fileUri, this.cropOptions);
      })
      .then((path) => {
        return this.base64.encodeFile(path);
      })
  }
  
```

### Credits
- https://github.com/peterantonyrausch/cordova-plugin-ratio-crop
- https://github.com/peterantonyrausch/ratio-crop
- https://github.com/apache/cordova-plugin-camera
- https://github.com/hazemhagrass/phonegap-base64
- https://github.com/jeduan/cordova-plugin-crop
- https://github.com/obeza/cordova-plugin-crop-with-ratio
- https://github.com/qwerqwermhc/Crop
