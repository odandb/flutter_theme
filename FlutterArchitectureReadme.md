<a href="https://www.odandb.com/">
    <img src="https://www.odandb.com/wp-content/uploads/2017/01/logo-black1.png" alt="logo" title="" align="right" height="60" />
</a>

<a href="https://flutter.dev/">
    <img src="https://flutter.dev/assets/flutter-lockup-4cb0ee072ab312e59784d9fbf4fb7ad42688a7fdaea1270ccf6bbf4f34b7e03f.svg" alt="logo" title="" align="left" height="60" />
</a>

OD&B Flutter App Architecture
======================

This document is a proposal for organizing files in a Flutter application.

#### Default Flutter app folder ####
<details><summary>Show</summary>

```
your_name_app/
  .idea/ 
  .vscode/ 
  android/
  build/
  ios/
  lib/
  test/
  .gitignore
  .metadata
  .packages
  myapp_app.iml
  pubspec.lock
  pubspec.yaml
  README.md
```

</details>

#### Proposed architecture Flutter app without default folders or files ####
```
your_name_app/
  assets/
    styles/
    images/
    i18n/
    animation/
  coverage/
  doc/
  lib/
    core/
      services/ // List of application services
        user_service.dart
    guards/     // List of guards
        user_is_connected.dart
    model/      // Models and interfaces
    pages/
                // List of application pages with their module, blocs and views .
      page1/
                // Example: page1_module.dart === module in Angular
                // Example: page1_bloc.dart === component in Angular
                // Example: page1_widget.dart === view in Angular
    shared/
      shared_bloc/
                // Example: Form validation bloc
      directives/
      pipes/
    theme/
                // Folder that contains design files such as colors and font styles
      colors.dart
      device_size.dart
      others.dart
      style.dart
      theme_data.dart
      theme.dart
    intl.dart   // File that loads the application's translation system
    main.dart   // Source file for launching the application
    routes.dart // File that manages the routing system with navigation paths
  test/
```

#### `pubspec.yaml` ####

```yaml
name: your_name_app
description: your_descrpition_app.

version: 1.0.0+1

environment:
  sdk: ">=2.1.0 <3.0.0"

dependencies:
  flutter:
    sdk: flutter
  intl:
  intl_translation:

dev_dependencies:
  flutter_driver:
    sdk: flutter
  test: any

flutter:
  uses-material-design: true
  assets:
    - assets/images/
    - assets/i18n/
    - assets/animation/

  fonts:
    # - family: Schyler
    #   fonts:
    #     - asset: fonts/Schyler-Regular.ttf
    #     - asset: fonts/Schyler-Italic.ttf
    #       style: italic
    # - family: Trajan Pro
    #   fonts:
    #     - asset: fonts/TrajanPro.ttf
    #     - asset: fonts/TrajanPro_Bold.ttf
    #       weight: 700
```