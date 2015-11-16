# smartcrop-android
smartcrop implementation in Java(Android)

This library will analyze best crop position and size by calculating some features; edge, skin tone, staturation and face.


## Screenshot


## Usage

### With [RxJava](https://github.com/ReactiveX/RxJava)(+[RxAndroid](https://github.com/ReactiveX/RxAndroid))

```java

SmartCrop
    .analyzeWithObservable(Options.DEFAULT.cropSquareSize(200), selectedImage)
    .subscribeOn(Schedulers.computation())
    .observeOn(AndroidSchedulers.mainThread())
    .subscribe(new Action1<CropResult>() {
        @Override
        public void call(CropResult cropResult) {
            // do what you want
        }
    });

```

### Without Rx

> But I recommend using RxJava or background thread because it took some times(about 500ms in 2013 Nexus5) so that it may stop the UI refresh and make bad UX.

```java
// this code will block about 500ms
CropResult cropResult = SmartCrop.analyze(Options.DEFAULT.cropSquareSize(200), selectedImage);

```


[CropResult.java](https://github.com/QuadFlask/smartcrop-android/blob/master/library/src/main/java/com/github/quadflask/smartcrop/CropResult.java)

```java
public class CropResult {
    public final Crop topCrop; // The best crop x, y, width, height and score
    public final List<Crop> crops;
    public final Bitmap debugImage;
    public final Bitmap resultImage; // cropped image from original image. Size is same with options.cropWidth/Height
}

```


## How to add dependency?

This library is not released in Maven Central, but instead you can use [JitPack](https://jitpack.io)

add remote maven url

```groovy
repositories {
    maven {
        url "https://jitpack.io"
    }
}
```

then add a library dependency

```groovy
dependencies {
    compile 'com.github.QuadFlask:smartcrop-android:v.0.0.0'
}
```

or, you can manually download `aar` and put into your project's `libs` directory.

and add dependency

```groovy
dependencies {
    compile(name:'[arrFileName]', ext:'aar')
}
```

> check out [latestVersion] at [releases](https://github.com/QuadFlask/smartcrop-android/releases)


## Performance

> Tested with Nexus5(2013) 

```javascript
```


## License

```
Copyright 2014-2015 QuadFlask

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
