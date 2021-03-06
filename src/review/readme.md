[&#8249; Review Doc Home](./)

<h1>Review 集成指南</h1>
<<[../../shared/-VERSION-/version.md]

## 集成
在您确保正确安装了 SDKBOX installer 的情况下，运行下面的命令来集成 SDKBOX Review 插件。
```bash
$ sdkbox import review
```

<<[../../shared/notice.md]

<!--## Configuration
<<[../../shared/sdkbox_cloud.md]
<<[../../shared/remote_application_config.md]-->


### JSON 配置
SDKBOX 安装器会为您自动生成一个配置文件 `res/sdkbox_config.json`,在您使用前,请修改里面的值为您自己的应用所需的值.

下面给一个 Review 的配置.
```json
"Review":{
    "ios": {
        "Review":{
            "AppID":"587767923",            //appid, ios 上有效
            "DayLimit": 0,                  //在评价弹出框显示前的天数限制
            "LaunchLimit": 3,               //在评价弹出框显示前的启动次数限制
            "UserEventLimit": 0,            //在评价弹出框显示前的用户事件限制, 用户事件是集成应用来增加事件记数的,调用 userDidSignificantEvent 增加用户事件记数
            "DayForReminding": 1,           //用户选择 稍后提示 后再次弹出的天数限制
            "LaunchForReminding": 2,        //用户选择 稍后提示 后再次弹出的启动次数限制
            "tryPromptWhenInit": true       //在初始化后，是否自动弹出评价提示框
        }
    },
    "android": {
        "Review":{
            "DayLimit": 0,
            "LaunchLimit": 3,
            "UserEventLimit": 0,
            "DayForReminding": 1,
            "LaunchForReminding": 2,
            "tryPromptWhenInit": true
        }
    }
}
```

<<[sdkbox-config-encrypt.md]

## 使用
<<[usage.md]

<<[api-reference.md]

<<[manual_integration.md]

<<[manual_ios.md]

<<[manual_android.md]

<<[extra-step.md]

<<[proguard.md]

