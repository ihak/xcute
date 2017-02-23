# xcute

xcode utility

[![asciicast](https://asciinema.org/a/88109.png)](https://asciinema.org/a/88109)

## Installation

```
pip install xcute
```

## Usage

```
xcute list
```
```
+-------------------+-------------+-----------------+---------------+
|      Project      |    Scheme   |SDK| Configuration |
+-------------------+-------------+-----------------+---------------+
| SwiftIO.xcodeproj | SwiftIO_iOS | iphonesimulator |     Debug     |
| SwiftIO.xcodeproj | SwiftIO_iOS | iphonesimulator |    Release    |
| SwiftIO.xcodeproj | SwiftIO_iOS |     iphoneos    |     Debug     |
| SwiftIO.xcodeproj | SwiftIO_iOS |     iphoneos    |    Release    |
| SwiftIO.xcodeproj | SwiftIO_OSX |      macosx     |     Debug     |
| SwiftIO.xcodeproj | SwiftIO_OSX |      macosx     |    Release    |
| SwiftIO.xcodeproj |   TestApp   |      macosx     |     Debug     |
| SwiftIO.xcodeproj |   TestApp   |      macosx     |    Release    |
+-------------------+-------------+-----------------+---------------+
```
```
xcute list -s SWIFT_VERSION
```
```
+-------------------+-------------+-----------------+---------------+---------------+
|      Project      |    Scheme   |SDK| Configuration | SWIFT_VERSION |
+-------------------+-------------+-----------------+---------------+---------------+
| SwiftIO.xcodeproj | SwiftIO_iOS | iphonesimulator |     Debug     |      3.0      |
| SwiftIO.xcodeproj | SwiftIO_iOS | iphonesimulator |    Release    |      3.0      |
| SwiftIO.xcodeproj | SwiftIO_iOS |     iphoneos    |     Debug     |      3.0      |
| SwiftIO.xcodeproj | SwiftIO_iOS |     iphoneos    |    Release    |      3.0      |
| SwiftIO.xcodeproj | SwiftIO_OSX |      macosx     |     Debug     |      3.0      |
| SwiftIO.xcodeproj | SwiftIO_OSX |      macosx     |    Release    |      3.0      |
| SwiftIO.xcodeproj |   TestApp   |      macosx     |     Debug     |      3.0      |
| SwiftIO.xcodeproj |   TestApp   |      macosx     |    Release    |      3.0      |
+-------------------+-------------+-----------------+---------------+---------------+
```
```
xcute list -s SWIFT_VERSION -s ENABLE_BITCODE
```
```
+-------------------+-------------+-----------------+---------------+---------------+----------------+
|      Project      |    Scheme   |SDK| Configuration | SWIFT_VERSION | ENABLE_BITCODE |
+-------------------+-------------+-----------------+---------------+---------------+----------------+
| SwiftIO.xcodeproj | SwiftIO_iOS | iphonesimulator |     Debug     |      3.0      |NO|
| SwiftIO.xcodeproj | SwiftIO_iOS | iphonesimulator |    Release    |      3.0      |NO|
| SwiftIO.xcodeproj | SwiftIO_iOS |     iphoneos    |     Debug     |      3.0      |      YES|
| SwiftIO.xcodeproj | SwiftIO_iOS |     iphoneos    |    Release    |      3.0      |      YES|
| SwiftIO.xcodeproj | SwiftIO_OSX |      macosx     |     Debug     |      3.0      |NO|
| SwiftIO.xcodeproj | SwiftIO_OSX |      macosx     |    Release    |      3.0      |NO|
| SwiftIO.xcodeproj |   TestApp   |      macosx     |     Debug     |      3.0      |NO|
| SwiftIO.xcodeproj |   TestApp   |      macosx     |    Release    |      3.0      |NO|
+-------------------+-------------+-----------------+---------------+---------------+----------------+
```
Any setting you have in your scheme or target can be shown
```
xcute list -s arch
```
```
+-------------------+-------------+-----------------+---------------+--------+
|      Project      |    Scheme   |SDK| Configuration |  arch  |
+-------------------+-------------+-----------------+---------------+--------+
| SwiftIO.xcodeproj | SwiftIO_iOS | iphonesimulator |     Debug     | x86_64 |
| SwiftIO.xcodeproj | SwiftIO_iOS | iphonesimulator |    Release    | x86_64 |
| SwiftIO.xcodeproj | SwiftIO_iOS |     iphoneos    |     Debug     | arm64  |
| SwiftIO.xcodeproj | SwiftIO_iOS |     iphoneos    |    Release    | arm64  |
| SwiftIO.xcodeproj | SwiftIO_OSX |      macosx     |     Debug     | x86_64 |
| SwiftIO.xcodeproj | SwiftIO_OSX |      macosx     |    Release    | x86_64 |
| SwiftIO.xcodeproj |   TestApp   |      macosx     |     Debug     | x86_64 |
| SwiftIO.xcodeproj |   TestApp   |      macosx     |    Release    | x86_64 |
+-------------------+-------------+-----------------+---------------+--------+
```

You can also export CI config files - for example .travis.yml in this case you can use templates (you can customise your own templates of course).
```
xcute export --template=travis-simple
```
```
language: objective-c
osx_image: xcode8
before_script:
- carthage bootstrap --no-use-binaries
script:
- xcodebuild -project 'SwiftIO.xcodeproj' -scheme 'SwiftIO_iOS' -sdk iphoneos -configuration Debug build
- xcodebuild -project 'SwiftIO.xcodeproj' -scheme 'SwiftIO_iOS' -sdk iphoneos -configuration Release build
- xcodebuild -project 'SwiftIO.xcodeproj' -scheme 'SwiftIO_iOS' -sdk iphonesimulator -configuration Debug build
- xcodebuild -project 'SwiftIO.xcodeproj' -scheme 'SwiftIO_iOS' -sdk iphonesimulator -configuration Release build
- xcodebuild -project 'SwiftIO.xcodeproj' -scheme 'SwiftIO_OSX' -sdk macosx -configuration Debug build
- xcodebuild -project 'SwiftIO.xcodeproj' -scheme 'SwiftIO_OSX' -sdk macosx -configuration Release build
- xcodebuild -project 'SwiftIO.xcodeproj' -scheme 'TestApp' -sdk macosx -configuration Debug build
- xcodebuild -project 'SwiftIO.xcodeproj' -scheme 'TestApp' -sdk macosx -configuration Release build
```
## Contribution

```
git clone https://github.com/schwa/xcute.git
cd xcute
pip install -e .
```

## Distribution

```
python setup.py sdist
twine upload --skip-existing dist/*
```
