# Change app icon in fluttter

## Step 1

- Download a image from internet and save in your system with a short name and .png extension

- Create a `assets` folder in your project root

- Move your downloaded image in this assets folder

## Step 2

### Open `pubspec.yaml` file and do following changes

- Add `flutter_launcher_icons: ^0.14.4` in `dev_dependencies`
- Add below code under dev_dependencies -

```yaml
dev_dependencies:
  flutter_launcher_icons: ^0.14.4

flutter_icons:
  android: true
  ios: true
  image_path: "assets/aicon.png"
```

#### Here `aicon.png` is my image file name

- Add this code in `flutter:`

```yaml
assets:
  - assets/aicon.png
```

## Step 3

### Open Terminal and run the following commands -

```yaml
flutter pub get
flutter pub run flutter_launcher_icons
flutter clean
flutter run
```
