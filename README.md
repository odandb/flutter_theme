<a href="https://www.odandb.com/">
    <img src="https://www.odandb.com/wp-content/uploads/2017/01/logo-black1.png" alt="logo" title="" align="right" height="60" />
</a>

<a href="https://flutter.dev/">
    <img src="https://flutter.dev/assets/flutter-lockup-4cb0ee072ab312e59784d9fbf4fb7ad42688a7fdaea1270ccf6bbf4f34b7e03f.svg" alt="logo" title="" align="left" height="60" />
</a>

OD&B Flutter Custom Theme
======================

Flutter Custom Theme is a tool to organize and use your own theme for a Flutter application.

* We define the **general themes** of the application as for example: Light Theme and Dark Theme.
* We define the **color variables**.
* We define the variables for the **font styles**.
* We define our conditions for **screen sizes** as for example: Mobile, Tablet, Desktop.

**The goal is to facilitate the implementation of the design within the application.**

## Installation ##

##### 1. Create a folder theme in `your_name_app_folder/lib` folder :

``` sh
mkdir theme
```

##### 2. Change folder and choose `theme` folder :

``` sh
cd ./theme
```

##### 3. Create this files in `theme` folder :

``` sh
touch theme.dart theme_data.dart colors.dart style.dart device_size.dart others.dart
```

##### 4. Copy the following blocks into the corresponding files and customize them according to your application :

<details><summary><b>theme.dart</b></summary>

``` dart
import 'package:flutter/material.dart';
import 'package:your_name_app_folder/theme/theme_data.dart';
import 'package:your_name_app_folder/theme/colors.dart';
import 'package:your_name_app_folder/theme/style.dart';
import 'package:your_name_app_folder/theme/others.dart';

class CustomTheme() {
  static final CustomTheme _singleton = CustomTheme._internal();

  factory CustomTheme {
    return _singleton;
  }
  
  static final ThemeData themeData = customThemeData;
  static final ThemeData themeDark = customThemeDataDark;
  static final CustomColors colors = CustomColors();
  static final CustomTextStyle style = CustomTextStyle();
  static final CustomImageBanner customImageBanner = CustomImageBanner();
  static final CustomFormSize customFormSize = CustomFormSize();

  CustomTheme._internal();
}
```

</details>

<details><summary><b>theme_data.dart</b></summary>

``` dart
import 'package:flutter/material.dart';
import 'package:your_name_app_folder/theme/colors.dart';

final ThemeData customThemeData = ThemeData(
  brightness: Brightness.light,
  primaryColor: CustomColors().white,
  primaryTextTheme: TextTheme(
    title: TextStyle(color: Colors.white),
  ),
);

final ThemeData customThemeDataDark = ThemeData(
  brightness: Brightness.dark,
);
```

</details>

<details><summary><b>colors.dart</b></summary>

``` dart
import 'package:flutter/material.dart';

class CustomColors {
  final MaterialColor white = const MaterialColor(
    0xFF252850,
    const <int, Color>{
      10: const Color(0x19ffffff),
      20: const Color(0x33ffffff),
      30: const Color(0x4cffffff),
      40: const Color(0x66ffffff),
      50: const Color(0x7fffffff),
      60: const Color(0x99ffffff),
      70: const Color(0xb2ffffff),
      80: const Color(0xccffffff),
      90: const Color(0xe5ffffff),
      100: const Color(0xffffffff)
    }
  );
  
  final Color info = const Color(0xff4a90e2);
  final Color danger = const Color(0xffea2322);
}
```

</details>

<details><summary><b>style.dart</b></summary>

``` dart
import 'package:flutter/material.dart';
import 'package:your_name_app_folder/theme/colors.dart';
import 'package:your_name_app_folder/theme/device_size.dart';

class CustomTextStyle {
  final extraLargeTextSizeTablet = 50.0;
  final xlargeTextSizeTablet = 40.0;
  final largeTextSizeTablet = 30.0;
  final mediumTextSizeTablet = 25.0;
  final bodyTextSizeTablet = 20.0;

  final extraLargeTextSizePhone = 30.0;
  final xlargeTextSizePhone = 32.0;
  final largeTextSizePhone = 26.0;
  final mediumTextSizePhone = 20.0;
  final bodyTextSizePhone = 16.0;

  TextStyle titleAppBar(BuildContext context) {
    return TextStyle(
      fontSize: DeviceSize(context).isTablet()
          ? extraLargeTextSizeTablet
          : extraLargeTextSizePhone,
      fontWeight: FontWeight.bold,
      color: Colors.white,
      fontFamily: 'Mansalva',
    );
  }

  TextStyle Dark_H2 = const TextStyle(
    fontFamily: 'SFProDisplay',
    color: Color(0xffffffff),
    fontSize: 60,
    fontWeight: FontWeight.w300,
    fontStyle: FontStyle.normal,
    letterSpacing: -1.447059,
    );
}
```

</details>

<details><summary><b>device_size.dart</b></summary>

``` dart
import 'package:flutter/material.dart';
import 'dart:io' show Platform;

class DeviceSize {
  BuildContext context;
  static final DeviceSize _singleton = DeviceSize._internal();

  factory DeviceSize(BuildContext context) {
    _singleton.context = context;
    return _singleton;
  }

  ///
  /// ## Basic Method  ##
  ///
  ///
  /// ### Landscape ###
  ///
  /// Check if the device is using landscape
  ///
  /// -----------------------------------------------------------------
  /// 
  /// #### Return ####
  /// ```dart
  /// return bool (true or false);
  /// ```
  /// 
  /// -----------------------------------------------------------------
  /// 
  /// #### Function ####
  /// ```dart
  /// bool isLandscape() {
  ///   return MediaQuery.of(context).orientation == Orientation.landscape;
  /// }
  /// ```
  ///
  bool isLandscape() {
    return MediaQuery.of(context).orientation == Orientation.landscape;
  }

  ///
  /// ## Basic Method  ##
  ///
  ///
  /// ### Portrait ###
  ///
  /// Check if the device is using portrait
  ///
  /// -----------------------------------------------------------------
  /// 
  /// #### Return ####
  /// ```dart
  /// return bool (true or false);
  /// ```
  /// 
  /// -----------------------------------------------------------------
  /// 
  /// #### Function ####
  /// ```dart
  /// bool isPortrait() {
  ///   return MediaQuery.of(context).orientation == Orientation.portrait;
  /// }
  /// ```
  ///
  bool isPortrait() {
    return MediaQuery.of(context).orientation == Orientation.portrait;
  }

  ///
  /// ## Basic Method  ##
  ///
  ///
  /// ### Mobile ###
  ///
  /// Check if the device is a mobile with default size
  ///
  /// -----------------------------------------------------------------
  /// 
  /// #### Return ####
  /// ```dart
  /// return bool (true or false);
  /// ```
  /// 
  /// -----------------------------------------------------------------
  ///
  /// #### Params checking ####
  /// - **320** >= width <= **768**
  /// - height <= **1024**
  /// 
  /// -----------------------------------------------------------------
  /// 
  /// #### Function ####
  /// ```dart
  /// bool isMobile() {
  ///   if (isPortrait()) {
  ///     return (MediaQuery.of(context).size.width.round() >= 320 &&
  ///             MediaQuery.of(context).size.width.round() <= 768 &&
  ///             MediaQuery.of(context).size.height.round() <= 1024 
  ///         ? true
  ///         : false);
  ///   } else {
  ///     return (MediaQuery.of(context).size.width.round() <= 1024 &&
  ///             MediaQuery.of(context).size.height.round() >= 320 &&
  ///             MediaQuery.of(context).size.height.round() <= 768
  ///         ? true
  ///         : false);
  ///   }
  /// }
  /// ```
  ///
  bool isMobile() {
    if (isPortrait()) {
      return (MediaQuery.of(context).size.width.round() >= 320 &&
              MediaQuery.of(context).size.width.round() <= 768 &&
              MediaQuery.of(context).size.height.round() <= 1024 
          ? true
          : false);
    } else {
      return (MediaQuery.of(context).size.width.round() <= 1024 &&
              MediaQuery.of(context).size.height.round() >= 320 &&
              MediaQuery.of(context).size.height.round() <= 768
          ? true
          : false);
    }
  }

  ///
  /// ## Basic Method  ##
  ///
  ///
  /// ### Tablet ###
  ///
  /// Check if the device is a tablet with default size
  ///
  /// -----------------------------------------------------------------
  /// 
  /// #### Return ####
  /// ```dart
  /// return bool (true or false);
  /// ```
  /// 
  /// -----------------------------------------------------------------
  ///
  /// #### Params checking ####
  /// - **768** >= width < **1024**
  /// - height <= **1024**
  /// 
  /// -----------------------------------------------------------------
  /// 
  /// #### Function ####
  /// ```dart
  /// bool isMobile() {
  ///   if (isPortrait()) {
  ///     return (MediaQuery.of(context).size.width.round() >= 768 &&
  ///             MediaQuery.of(context).size.width.round() < 1024 &&
  ///             MediaQuery.of(context).size.height.round() <= 1024 
  ///         ? true
  ///         : false);
  ///   } else {
  ///     return (MediaQuery.of(context).size.width.round() <= 1024 &&
  ///             MediaQuery.of(context).size.height.round() >= 768 &&
  ///             MediaQuery.of(context).size.height.round() < 1024
  ///         ? true
  ///         : false);
  ///   }
  /// }
  /// ```
  ///
  bool isTablet() {
    if (isPortrait()) {
      return (MediaQuery.of(context).size.width.round() >= 768 &&
              MediaQuery.of(context).size.width.round() < 1024 &&
              MediaQuery.of(context).size.height.round() <= 1024
          ? true
          : false);
    } else {
      return (MediaQuery.of(context).size.width.round() <= 1024 &&
              MediaQuery.of(context).size.height.round() >= 768 &&
              MediaQuery.of(context).size.height.round() < 1024
          ? true
          : false);
    }
  }

  ///
  /// ## Basic Method  ##
  ///
  ///
  /// ### Desktop ###
  ///
  /// Check if the device is a desktop with default size
  ///
  /// -----------------------------------------------------------------
  /// 
  /// #### Return ####
  /// ```dart
  /// return bool (true or false);
  /// ```
  /// 
  /// -----------------------------------------------------------------
  ///
  /// #### Params checking ####
  /// - width >= **1024**
  /// - height >= **1024**
  /// 
  /// -----------------------------------------------------------------
  /// 
  /// #### Function ####
  /// ```dart
  /// bool isDesktop() {
  ///   return (MediaQuery.of(context).size.width.round() >= 1024 &&
  ///           MediaQuery.of(context).size.height.round() >= 1024
  ///       ? true
  ///       : false);
  /// }
  /// ```
  ///
  bool isDesktop() {
    return (MediaQuery.of(context).size.width.round() >= 1024 &&
            MediaQuery.of(context).size.height.round() >= 1024
        ? true
        : false);
  }

  ///
  /// ## Basic Method  ##
  ///
  ///
  /// ### IOS OS ###
  ///
  /// Check if the device is an ios OS
  ///
  /// -----------------------------------------------------------------
  /// 
  /// #### Return ####
  /// ```dart
  /// return bool (true or false);
  /// ```
  /// 
  /// -----------------------------------------------------------------
  /// 
  /// #### Function ####
  /// ```dart
  /// bool isIOS() {
  ///   return Platform.isIOS;
  /// }
  /// ```
  ///
  bool isIOS() {
    return Platform.isIOS;
  }

  ///
  /// ## Basic Method  ##
  ///
  ///
  /// ### Android OS ###
  ///
  /// Check if the device is an android OS
  ///
  /// -----------------------------------------------------------------
  /// 
  /// #### Return ####
  /// ```dart
  /// return bool (true or false);
  /// ```
  /// 
  /// -----------------------------------------------------------------
  /// 
  /// #### Function ####
  /// ```dart
  /// bool isAndroid() {
  ///   return Platform.isAndroid;
  /// }
  /// ```
  ///
  bool isAndroid() {
    return Platform.isAndroid;
  }

  ///
  /// ## Basic Method  ##
  ///
  ///
  /// ### Mac OS ###
  ///
  /// Check if the device is an mac OS
  ///
  /// -----------------------------------------------------------------
  /// 
  /// #### Return ####
  /// ```dart
  /// return bool (true or false);
  /// ```
  /// 
  /// -----------------------------------------------------------------
  /// 
  /// #### Function ####
  /// ```dart
  /// bool isMacOS() {
  ///   return Platform.isMacOS;
  /// }
  /// ```
  ///
  bool isMacOS() {
    return Platform.isMacOS;
  }

  ///
  /// ## Basic Method  ##
  ///
  ///
  /// ### Linux OS ###
  ///
  /// Check if the device is an linux OS
  ///
  /// -----------------------------------------------------------------
  /// 
  /// #### Return ####
  /// ```dart
  /// return bool (true or false);
  /// ```
  /// 
  /// -----------------------------------------------------------------
  /// 
  /// #### Function ####
  /// ```dart
  /// bool isLinux() {
  ///   return Platform.isLinux;
  /// }
  /// ```
  ///
  bool isLinux() {
    return Platform.isLinux;
  }

  ///
  /// ## Basic Method  ##
  ///
  ///
  /// ### Windows OS ###
  ///
  /// Check if the device is an windows OS
  ///
  /// -----------------------------------------------------------------
  /// 
  /// #### Return ####
  /// ```dart
  /// return bool (true or false);
  /// ```
  /// 
  /// -----------------------------------------------------------------
  /// 
  /// #### Function ####
  /// ```dart
  /// bool isWindows() {
  ///   return Platform.isWindows;
  /// }
  /// ```
  ///
  bool isWindows() {
    return Platform.isWindows;
  }

  ///
  /// ## Apple Devices ##
  ///
  ///
  /// ### Iphone ###
  ///
  /// Check if the device is one of Iphone models
  ///
  /// -----------------------------------------------------------------
  ///
  /// #### Params checking ####
  /// - **375** >= width <= **414**
  /// - **568** >= height <= **896**
  /// 
  /// -----------------------------------------------------------------
  /// 
  /// #### Return ####
  /// ```dart
  /// return bool (true or false);
  /// ```
  /// 
  /// -----------------------------------------------------------------
  /// 
  /// #### Function ####
  /// ```dart
  /// bool isIPhone() {
  ///   if (isIOS()) {
  ///     if (isPortrait()) {
  ///       return (MediaQuery.of(context).size.width.round() >= 375 &&
  ///               MediaQuery.of(context).size.width.round() <= 414 &&
  ///               MediaQuery.of(context).size.height.round() >= 568 &&
  ///               MediaQuery.of(context).size.height.round() <= 896
  ///           ? true
  ///           : false);
  ///     } else {
  ///       return (MediaQuery.of(context).size.width.round() >= 568 &&
  ///               MediaQuery.of(context).size.width.round() <= 896 &&
  ///               MediaQuery.of(context).size.height.round() >= 375 &&
  ///               MediaQuery.of(context).size.height.round() <= 414
  ///           ? true
  ///           : false);
  ///     }
  ///   } else {
  ///     return false;
  ///   }
  /// }
  /// ```
  ///
  bool isIPhone() {
    if (isIOS()) {
      if (isPortrait()) {
        return (MediaQuery.of(context).size.width.round() >= 375 &&
                MediaQuery.of(context).size.width.round() <= 414 &&
                MediaQuery.of(context).size.height.round() >= 568 &&
                MediaQuery.of(context).size.height.round() <= 896
            ? true
            : false);
      } else {
        return (MediaQuery.of(context).size.width.round() >= 568 &&
                MediaQuery.of(context).size.width.round() <= 896 &&
                MediaQuery.of(context).size.height.round() >= 375 &&
                MediaQuery.of(context).size.height.round() <= 414
            ? true
            : false);
      }
    } else {
      return false;
    }
  }

  ///
  /// ## Apple Devices ##
  ///
  ///
  /// ### Ipad ###
  ///
  /// Check if the device is one of Ipad models
  ///
  /// -----------------------------------------------------------------
  ///
  /// #### Params checking ####
  /// - **768** >= width <= **1024**
  /// - **1024** >= height <= **1366**
  /// 
  /// -----------------------------------------------------------------
  /// 
  /// #### Return ####
  /// ```dart
  /// return bool (true or false);
  /// ```
  /// 
  /// -----------------------------------------------------------------
  /// 
  /// #### Function ####
  /// ```dart
  ///  bool isIPad() {
  ///     if (isIOS()) {
  ///       if (isPortrait()) {
  ///         return (MediaQuery.of(context).size.width.round() >= 768 &&
  ///                 MediaQuery.of(context).size.width.round() <= 1024 &&
  ///                 MediaQuery.of(context).size.height.round() >= 1024 &&
  ///                 MediaQuery.of(context).size.height.round() <= 1366
  ///             ? true
  ///             : false);
  ///       } else {
  ///         return (MediaQuery.of(context).size.width.round() >= 1024 &&
  ///                 MediaQuery.of(context).size.width.round() <= 1366 &&
  ///                 MediaQuery.of(context).size.height.round() >= 768 &&
  ///                 MediaQuery.of(context).size.height.round() <= 1024
  ///             ? true
  ///             : false);
  ///       }
  ///     } else {
  ///       return false;
  ///     }
  ///   }
  /// ```
  ///
  bool isIPad() {
    if (isIOS()) {
      if (isPortrait()) {
        return (MediaQuery.of(context).size.width.round() >= 768 &&
                MediaQuery.of(context).size.width.round() <= 1024 &&
                MediaQuery.of(context).size.height.round() >= 1024 &&
                MediaQuery.of(context).size.height.round() <= 1366
            ? true
            : false);
      } else {
        return (MediaQuery.of(context).size.width.round() >= 1024 &&
                MediaQuery.of(context).size.width.round() <= 1366 &&
                MediaQuery.of(context).size.height.round() >= 768 &&
                MediaQuery.of(context).size.height.round() <= 1024
            ? true
            : false);
      }
    } else {
      return false;
    }
  }


  ///
  /// ## Apple Devices ##
  ///
  ///
  /// ### Apple Watch ###
  ///
  /// Check if the device is one of Apple Watch models
  ///
  /// -----------------------------------------------------------------
  ///
  /// #### Params checking ####
  /// - **136** >= width <= **184**
  /// - **170** >= height <= **224**
  /// 
  /// -----------------------------------------------------------------
  /// 
  /// #### Return ####
  /// ```dart
  /// return bool (true or false);
  /// ```
  /// 
  /// -----------------------------------------------------------------
  /// 
  /// #### Function ####
  /// ```dart
  /// bool isAppleWatch() {
  ///   if (isIOS()) {
  ///     return (MediaQuery.of(context).size.width.round() >= 136 &&
  ///             MediaQuery.of(context).size.width.round() <= 184 &&
  ///             MediaQuery.of(context).size.height.round() >= 170 &&
  ///             MediaQuery.of(context).size.height.round() <= 224
  ///         ? true
  ///         : false);
  ///   } else {
  ///     return false;
  ///   }
  /// }
  /// ```
  ///
  bool isAppleWatch() {
    if (isIOS()) {
      return (MediaQuery.of(context).size.width.round() >= 136 &&
              MediaQuery.of(context).size.width.round() <= 184 &&
              MediaQuery.of(context).size.height.round() >= 170 &&
              MediaQuery.of(context).size.height.round() <= 224
          ? true
          : false);
    } else {
      return false;
    }
  }

  ///
  /// ## Apple Devices ##
  ///
  ///
  /// ### Apple TV ###
  ///
  /// Check if the device is one of Apple TV models
  ///
  /// -----------------------------------------------------------------
  ///
  /// #### Params checking ####
  /// - width >= **1920**
  /// - height >= **1080**
  /// 
  /// -----------------------------------------------------------------
  /// 
  /// #### Return ####
  /// ```dart
  /// return bool (true or false);
  /// ```
  /// 
  /// -----------------------------------------------------------------
  /// 
  /// #### Function ####
  /// ```dart
  /// bool isAppleTV() {
  ///   if (isIOS()) {
  ///     return (MediaQuery.of(context).size.width.round() >= 1920 &&
  ///             MediaQuery.of(context).size.height.round() >= 1080
  ///         ? true
  ///         : false);
  ///   } else {
  ///     return false;
  ///   }
  /// }
  /// ```
  ///
  bool isAppleTV() {
    if (isIOS()) {
      return (MediaQuery.of(context).size.width.round() >= 1920 &&
              MediaQuery.of(context).size.height.round() >= 1080
          ? true
          : false);
    } else {
      return false;
    }
  }

  ///
  /// ## Android Devices ##
  ///
  ///
  /// ### Android Phone ###
  ///
  /// Check if the device is one of Android Phone models
  ///
  /// -----------------------------------------------------------------
  ///
  /// #### Params checking ####
  /// - **360** >= width <= **412**
  /// - **640** >= height <= **760**
  /// 
  /// -----------------------------------------------------------------
  /// 
  /// #### Return ####
  /// ```dart
  /// return bool (true or false);
  /// ```
  /// 
  /// -----------------------------------------------------------------
  /// 
  /// #### Function ####
  /// ```dart
  /// bool isAndroidPhone() {
  ///   if (isAndroid()) {
  ///     if (isPortrait()) {
  ///       return (MediaQuery.of(context).size.width.round() >= 360 &&
  ///               MediaQuery.of(context).size.width.round() <= 412 &&
  ///               MediaQuery.of(context).size.height.round() >= 640 &&
  ///               MediaQuery.of(context).size.height.round() <= 760
  ///           ? true
  ///           : false);
  ///     } else {
  ///       return (MediaQuery.of(context).size.width.round() >= 640 &&
  ///               MediaQuery.of(context).size.width.round() <= 760 &&
  ///               MediaQuery.of(context).size.height.round() >= 360 &&
  ///               MediaQuery.of(context).size.height.round() <= 412
  ///           ? true
  ///           : false);
  ///     }
  ///   } else {
  ///     return false;
  ///   }
  /// }
  /// ```
  ///
  bool isAndroidPhone() {
    if (isAndroid()) {
      if (isPortrait()) {
        return (MediaQuery.of(context).size.width.round() >= 360 &&
                MediaQuery.of(context).size.width.round() <= 412 &&
                MediaQuery.of(context).size.height.round() >= 640 &&
                MediaQuery.of(context).size.height.round() <= 760
            ? true
            : false);
      } else {
        return (MediaQuery.of(context).size.width.round() >= 640 &&
                MediaQuery.of(context).size.width.round() <= 760 &&
                MediaQuery.of(context).size.height.round() >= 360 &&
                MediaQuery.of(context).size.height.round() <= 412
            ? true
            : false);
      }
    } else {
      return false;
    }
  }

  ///
  /// ## Android Devices ##
  ///
  ///
  /// ### Android Tablet ###
  ///
  /// Check if the device is one of Android Tablet models
  ///
  /// -----------------------------------------------------------------
  ///
  /// #### Params checking ####
  /// - **600** >= width <= **900**
  /// - **960** >= height <= **1280**
  /// 
  /// -----------------------------------------------------------------
  /// 
  /// #### Return ####
  /// ```dart
  /// return bool (true or false);
  /// ```
  /// 
  /// -----------------------------------------------------------------
  /// 
  /// #### Function ####
  /// ```dart
  /// bool isAndroidTablet() {
  ///   if (isAndroid()) {
  ///     if (isPortrait()) {
  ///       return (MediaQuery.of(context).size.width.round() >= 600 &&
  ///               MediaQuery.of(context).size.width.round() <= 900 &&
  ///               MediaQuery.of(context).size.height.round() >= 960 &&
  ///               MediaQuery.of(context).size.height.round() <= 1280
  ///           ? true
  ///           : false);
  ///     } else {
  ///       return (MediaQuery.of(context).size.width.round() >= 960 &&
  ///               MediaQuery.of(context).size.width.round() <= 1280 &&
  ///               MediaQuery.of(context).size.height.round() >= 600 &&
  ///               MediaQuery.of(context).size.height.round() <= 900
  ///           ? true
  ///           : false);
  ///     }
  ///   } else {
  ///     return false;
  ///   }
  /// }
  /// ```
  ///
  bool isAndroidTablet() {
    if (isAndroid()) {
      if (isPortrait()) {
        return (MediaQuery.of(context).size.width.round() >= 600 &&
                MediaQuery.of(context).size.width.round() <= 900 &&
                MediaQuery.of(context).size.height.round() >= 960 &&
                MediaQuery.of(context).size.height.round() <= 1280
            ? true
            : false);
      } else {
        return (MediaQuery.of(context).size.width.round() >= 960 &&
                MediaQuery.of(context).size.width.round() <= 1280 &&
                MediaQuery.of(context).size.height.round() >= 600 &&
                MediaQuery.of(context).size.height.round() <= 900
            ? true
            : false);
      }
    } else {
      return false;
    }
  }

  ///
  /// ## Android Devices ##
  ///
  ///
  /// ### Chrome Book ###
  ///
  /// Check if the device is one of Chrome Book models
  ///
  /// -----------------------------------------------------------------
  ///
  /// #### Params checking ####
  /// - width >= **1280**
  /// - height >= **768**
  /// 
  /// -----------------------------------------------------------------
  /// 
  /// #### Return ####
  /// ```dart
  /// return bool (true or false);
  /// ```
  /// 
  /// -----------------------------------------------------------------
  /// 
  /// #### Function ####
  /// ```dart
  /// bool isChromeBook() {
  ///   if (isAndroid()) {
  ///     return (MediaQuery.of(context).size.width.round() >= 1280 &&
  ///             MediaQuery.of(context).size.height.round() >= 768
  ///         ? true
  ///         : false);
  ///   } else {
  ///     return false;
  ///   }
  /// }
  /// ```
  ///
  bool isChromeBook() {
    if (isAndroid()) {
      return (MediaQuery.of(context).size.width.round() >= 1280 &&
              MediaQuery.of(context).size.height.round() >= 768
          ? true
          : false);
    } else {
      return false;
    }
  }

  DeviceSize._internal();
}

```

</details>

<details><summary><b>others.dart</b></summary>

``` dart
import 'package:flutter/material.dart';
import 'package:your_name_app_folder/theme/device_size.dart';

class CustomImageBanner {
  static const ExtraLargeTextSizeImageBannerTablet = 500.0;
  static const ExtraLargeTextSizeImagebannerPhone = 240.0;

  double height(BuildContext context) {
    return DeviceSize(context).isTablet()
        ? ExtraLargeTextSizeImageBannerTablet
        : ExtraLargeTextSizeImagebannerPhone;
  }
}

class CustomFormSize {
  static const ExtraLargeTextSizeFormTablet = 300.0;
  static const ExtraLargeTextSizeFormPhone = 200.0;

  double width(BuildContext context) {
    return DeviceSize(context).isTablet()
        ? ExtraLargeTextSizeFormTablet
        : ExtraLargeTextSizeFormPhone;
  }
}
```

</details>

## Usage

Following steps:

#### 1. Prepare your `main.dart` file:

  

``` dart
  import 'package:flutter/material.dart';
  import 'package:your_name_app_folder/theme/theme.dart';

  void main(List<String> args) {
    runApp(MyApp());
  }

  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        title: 'your_app_name_title',
        debugShowCheckedModeBanner: false, //Show banner debug change by true; Default == true;
        theme: CustomTheme.themeData, // Example with custom theme light mode
        darkTheme: CustomTheme.themeDark, // Example with custom theme dark mode
      );
    }
  }
  ```

#### 2. Example in `home.dart` file:

  ##### 2.1 Need to import :
  

``` dart
    import 'package:your_name_app_folder/theme/theme.dart';
  ```

  ##### 2.2 Using custom style, custom image banner and custom color :
  

``` dart
    import 'package:flutter/material.dart';
    import 'package:your_name_app_folder/theme/theme.dart';

    class HomePage extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Center(
            child: Text(
              'your_name_app_title',
              style: CustomTheme.style.titleAppBar(context), // Example with custom style
            ),
          ),
        ),
        body: SingleChildScrollView(
          child: Column(
            children: [
              Imagebanner('assets/images/lake.jpg'),
              Column(
                crossAxisAlignment: CrossAxisAlignment.center,
                mainAxisAlignment: MainAxisAlignment.center,
                children: <Widget>[
                  Container(
                    padding: const EdgeInsets.only(top: 30, left: 80, right: 80),
                    child: FittedBox(
                      alignment: Alignment.center,
                      fit: BoxFit.scaleDown,
                      child: Text(
                        'your_name_app_title',
                        style: TextStyle(
                          color: CustomTheme.colors.blue[100], // Custom color
                          fontSize: CustomTheme.style.bodyTextSizePhone // Custom font size
                          ), // TextStyle
                      ), // Text
                    ), // FittedBox
                  ), // Container
                ],
              ), // Column
            ],
          ), // Column
        ), // SingleChildScrollView
      ); // Scaffold
    }
  }
  ```

#### 3. Example with `ImageBanner` in others theme :

  ##### 3.1 Need to import :
  

``` dart
    import 'package:myapp/theme/theme.dart';
  ```

  ##### 3.2 Check if the device is a tablet :
  

``` dart
  import 'package:flutter/material.dart';
  import 'package:myapp/theme/theme.dart';

  class Imagebanner extends StatelessWidget {
    final String _imagePath;

    Imagebanner(this._imagePath);
    @override
    Widget build(BuildContext context) {
      final int width = MediaQuery.of(context).size.width.round();

      return Container(
        constraints: BoxConstraints.expand(
          height: CustomTheme.customImageBanner.height(context), 
          // Example of use for the image banner in relation to the size of the device
        ),
        decoration: BoxDecoration(
          color: Colors.grey,
          image: DecorationImage(
            image: AssetImage(_imagePath),
            fit: BoxFit.cover,
          ),
        ),
      );
    }
  }
  ```

#### 4. Getting device size :

  ##### 4.1 Need to import :
  

``` dart
    import 'package:your_name_app_folder/theme/device_size.dart';
  ```

  ##### 4.2 Check if the device is a tablet :
  

``` dart
    import 'package:flutter/material.dart';
    import 'package:your_name_app_folder/theme/device_size.dart';

    class HomePage extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
    final bool isTablet = DeviceSize(context).isTablet(); // Example of checking size of device if is equal to a tablet

    return Container(
      padding: isTablet
              ? const EdgeInsets.only(top: 130, left: 180, right: 180)
              : const EdgeInsets.only(top: 30, left: 80, right: 80),
      child: FittedBox(
        alignment: Alignment.center,
        fit: BoxFit.scaleDown,
        child: Text(
          'your_name_app_title',
          style: TextStyle(
            color: CustomTheme.colors.blue[100],
            fontSize: CustomTheme.style.bodyTextSizePhone
            ), // TextStyle
          ), // Text
        ), // FittedBox
      ), // Container
    }
  }
  ```

