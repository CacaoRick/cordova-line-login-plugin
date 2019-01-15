# cordova-line-login-plugin
LineSDKを使用してLINEログインを簡単に実装するためのcordovaプラグイン。　　

機能はログイン、ログアウト、アクセストークンの取得・検証・リフレッシュを行う。使用しているLineSDKのバージョンは以下のとおり。  

iOS：5.0.2

Android：4.0.8  

組み込みまでの流れは以下の通り  
「LINE BUSINESS CENTER」からLINEログインに対応したビジネスアカウントを作成。Application TypeはNATIVE_APPを選択。

### ios
1. 「LINE DEVELOPERS」より「iOS Bundle ID」「iOS Scheme」を設定。
1. 当プラグインをインストール。
1. xcodeの「Capabilities」より「Keychain Sharing」をONに設定。
1. プログラムの実装

```
例)
iOS Bundle ID : com.example.sample
iOS Scheme : line3rdp.com.example.sample
```

### android
1. 「LINE DEVELOPERS」より「Android Package Name」「Android Package Signature」「Android Scheme」を設定。
1. 当プラグインをインストール。
1. プログラムの実装

```
例)  
Android Package Name : com.example.sample
Android Package Signature : 11:22:33:44:55:66:77:88:99:aa:bb:cc:dd:ee:ff:gg:hh:ii:jj:kk
Android Scheme : com.example.sample://
```

## Installation
- iOS

```
cordova plugin add https://github.com/nrikiji/cordova-line-login-plugin.git

cd platform/ios
echo github \"line/line-sdk-ios-swift\" \~\> 5.0 >> Cartfile
carthage update --platform iOS
```

「Linked Frameworks and Libraries」より 「Carthage/Build/iOS/LineSDK.framework」を追加  

「Build Phases」より 「Run Script」を登録

Command
```
/usr/local/bin/carthage copy-frameworks

```

Input Files
```
$(SRCROOT)/Carthage/Build/iOS/LineSDK.framework
```

Output Files
```
$(BUILT_PRODUCTS_DIR)/$(FRAMEWORKS_FOLDER_PATH)/LineSDK.framework
```

- Android

## Supported Platforms
- iOS
- Android

## LINE SDK
このプラグインはLINEが提供するSDKを使用しています。これらの詳細はドキュメントを確認下さい。[iOS](https://developers.line.me/ja/docs/ios-sdk/) or 
[Android](https://developers.line.me/ja/docs/android-sdk/)

## Example

ionicでの使用例
```js
angular.module('starter', ['ionic'])
  .run(function($ionicPlatform) {
    ・・・

    // initialize
    lineLogin.initialize({channel_id: "your_chanel_id"});
  })
  .controller("LineCtrl", function($scope) {
    $scope.onLineLogin = function() {
      // login...
      lineLogin.login({},
        function(result) {
          console.log(result); // {userID:12345, displayName:'user name', pictureURL:'thumbnail url'}
        }, function(error) {
          console.log(error);
        });
    }

    $scope.onLineLoginWeb = function() {
      // login with web...(iOS only)
      lineLogin.loginWeb({},
        function(result) {
          console.log(result); // {userID:12345, displayName:'user name', pictureURL:'thumbnail url'}
        }, function(error) {
          console.log(error);
        });
    }

    $scope.onLineLogout = function() {
      // logout...
      lineLogin.logout(
        function(result) {
          console.log(result);
        }, function(error) {
          console.log(error);
        });
    }

    $scope.onLineGetAccessToken = function() {
      // get access token
      lineLogin.getAccessToken(
        function(result) {
          // success
          console.log(result); // {accessToken:'xxxxxxxx', expireTime: 123456789}
        }, function() {
          // failed
        });
    }

    $scope.onLineVerifyAccessToken = function() {
      // verify current access token
      lineLogin.verifyAccessToken(
        function() {
          // success
        }, function() {
          // failed
        });
    }

    $scope.onLineRefreshAccessToken = function() {
      // refresh access token
      lineLogin.verifyAccessToken(
        function(accessToken) {
          // success
        }, function() {
          // failed
        });
    }

  });
```

