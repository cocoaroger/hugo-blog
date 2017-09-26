---
title: "使用 fastlane"
date: 2017-09-26T14:11:54+08:00
draft: false
---

以下是我集成 *fastlane* 的过程

#### 安装 *fastlane*
`sudo gem install fastlane`

#### 初始化 *fastlane*
`cd` 到项目目录
执行 `fastlane init`

#### 两个主要文件配置
##### *fastlane/Appfile* 配置 App 基本信息

``` ruby-lang
app_identifier "com.cocoaroger.appstore" # The bundle identifier of your app

apple_dev_portal_id ""  # Apple Developer Account
itunes_connect_id ""  # iTunes Connect Account

team_id "" # Developer Portal Team ID
itc_team_id "" # iTunes Connect Team ID

for_lane :adhoc do
  app_identifier "com.cocoaroger.test"
end

for_lane :appstore do
  app_identifier "com.cocoaroger.appstore"
end
```

##### *fastlane/Fastfile* 定制我们的自动化脚本
我这里的 `appstore` 只是打包了，没有直接传到 `itunes connect`

``` ruby-lang
fastlane_version "2.55.0"
default_platform :ios

desc "upload pgyer"
lane :adhoc do
  gym(export_method: "ad-hoc")
  pgyer(api_key: "", user_key: "")
end

desc "upload appstore"
lane :appstore do
  gym(export_method: "app-store")
end

after_all do |lane|
  puts "Successfully deployed new App Update."
end

error do |lane, exception|
  puts exception.message
end
```

#### 运行方法
上传 `pgyer` 测试环境：`fastlane adhoc`
打包 `appstore`：`fastlane appstore`
