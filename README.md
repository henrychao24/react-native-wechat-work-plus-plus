# react-native-wechat-work-plus-plus

千愁散尽一剑轻

## 感谢

[react-native-wechat-work](https://github.com/xinpureZhu/react-native-wechat-work)

[react-native-wechat-work-plus](https://www.npmjs.com/package/react-native-wechat-work-plus?activeTab=readme)

## Getting started

```
$ yarn add react-native-wechat-work-plus-plus
$ npx pod-install
```

### Installation

#### iOS

1. 在XCode中，选择你的工程设置项，选中“TARGETS”一栏，在“Info”标签栏的“URL Types”添加“URL Schemes”，其内容为你所注册的应用程序将获得应用程序ID和scheme。

[企微文档](https://developer.work.weixin.qq.com/document/path/91193#%E6%90%AD%E5%BB%BA%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83)

2. 由于iOS系统的限制，在iOS9及以上系统检测企业微信是否安装，需要将企业微信的scheme"wxwork"(云端版本)及"wxworklocal"(本地部署版本)添加到工程的Info.plist中的LSApplicationQueriesSchemes白名单里，否则此方法总是会返回NO。

```
<key>LSApplicationQueriesSchemes</key>
<array>
  <string>wxworklocal</string>
  <string>wxwork</string>
</array>
```

3. 在 AppDelegate.m 文件中添加 handleOpenURL 支持，否则点击登录后不会回调code

```
#import <React/RCTLinkingManager.h>

- (BOOL)application:(UIApplication *)application
            openURL:(NSURL *)url
            options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options
{
  return [RCTLinkingManager application:application openURL:url options:options];
}
```

#### Android
1. android/settings.gradle
```
include ':react-native-wechat-work-plus-plus'
project(':react-native-wechat-work-plus-plus').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-wechat-work-plus-plus/lib/android')
```
2. android/app/build.gradle
```
implementation project(':react-native-wechat-work-plus-plus')
```
3. MainApplication
```
import com.xinpure.wechatwork.RNWeChatWorkPackage;
getPackages函数里，添加
packages.add(new RNWeChatWorkPackage());
```


## Usage
```javascript
import * as RNWeChatWork from 'react-native-wechat-work-plus-plus';

// 注册
async () => {
  try {
    console.log('begin.....................');
    let res = await WeChatWork.registerApp('11', '22', '33');
    console.log('success.....................', res);
  } catch (error) {
    console.log('error.....................', error);
  }
}

// 登录
async () => {
  try {
    console.log('begin.....................');
    let res = await WeChatWork.SSOAuth('test');
    console.log('success.....................', res);
  } catch (error) {
    console.log('error.....................', error);
  }
}
```

