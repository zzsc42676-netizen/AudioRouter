---
AIGC:
    ContentProducer: Minimax Agent AI
    ContentPropagator: Minimax Agent AI
    Label: AIGC
    ProduceID: "00000000000000000000000000000000"
    PropagateID: "00000000000000000000000000000000"
    ReservedCode1: 3044022014cdca8d0027cf02f0323dcf1621c24b85f1e05f3dd108dd17a362ab3c449593022020bcc74cc07329d7bf099ce7065abe189743a70dd705d4f43ae82b168ae2aadd
    ReservedCode2: 30460221009580cf0e73be848236e5fc37d2275c216129f8575a466642005f1b0c6857b601022100de4ca076f995daea2a2c8d962208e3532246fdf6aca0ee09adbd9fa8cf4d9960
---

# AudioRouter for MagicOS

一个用于荣耀/华为手机的音频路由管理工具，可以在连接耳机时强制特定应用使用外放播放。

## 功能特点

- **智能音频路由**: 当耳机连接时，自动将指定应用的音频切换到扬声器
- **应用选择**: 用户可自定义选择需要强制外放的应用
- **后台监控**: 前台服务持续监控应用状态
- **荣耀MagicOS适配**: 针对荣耀手机的后台管理进行了优化
- **完全本地运行**: 不收集任何个人信息，保护隐私

## 技术原理

1. **无障碍服务 (AccessibilityService)**: 用于监听前台应用变化
2. **音频管理器 (AudioManager)**: 使用 `MODE_IN_COMMUNICATION` 模式强制开启扬声器
3. **前台服务 (Foreground Service)**: 保证后台持续运行

## 项目结构

```
AudioRouter/
├── app/
│   ├── src/main/
│   │   ├── java/com/audiorouter/magicos/
│   │   │   ├── data/
│   │   │   │   ├── AppInfo.kt          # 应用数据类
│   │   │   │   └── AppPreferences.kt  # 数据存储
│   │   │   ├── service/
│   │   │   │   ├── AudioRouterAccessibilityService.kt  # 无障碍服务
│   │   │   │   ├── AudioRouterService.kt              # 前台服务
│   │   │   │   └── BootReceiver.kt                   # 启动接收器
│   │   │   ├── ui/
│   │   │   │   ├── MainActivity.kt     # 主界面
│   │   │   │   └── AppListAdapter.kt  # 应用列表适配器
│   │   │   └── utils/
│   │   │       ├── AudioRouteManager.kt  # 音频路由管理
│   │   │       └── AppUtils.kt          # 应用工具类
│   │   ├── res/
│   │   │   ├── layout/     # 布局文件
│   │   │   ├── values/    # 字符串、颜色、主题
│   │   │   ├── drawable/  # 图标资源
│   │   │   ├── menu/      # 菜单
│   │   │   └── xml/       # 配置文件
│   │   └── AndroidManifest.xml
│   └── build.gradle
├── build.gradle
├── settings.gradle
└── gradle.properties
```

## 使用说明

### 1. 安装应用

将编译好的 APK 安装到荣耀手机上。

### 2. 授予权限

首次启动时需要授予以下权限：

- **无障碍权限**: 用于检测当前前台应用
- **通知权限**: 用于后台服务运行（Android 13+）
- **电池优化白名单**: 防止服务被系统杀死

### 3. 配置使用

1. 开启主界面上的服务开关
2. 在应用列表中搜索并选择需要强制外放的应用（如抖音、微信语音等）
3. 连接耳机
4. 打开选中的应用，音频将自动从扬声器播放

## 构建指南

### 环境要求

- Android Studio Arctic Fox 或更高版本
- JDK 11 或更高版本
- Android SDK (API 34)

### 构建步骤

1. 克隆项目到本地
2. 在 Android Studio 中打开项目
3. 等待 Gradle 同步完成
4. Build → Build APK

### 命令行构建

```bash
# 进入项目目录
cd AudioRouter

# 同步Gradle
./gradlew assembleDebug

# APK输出位置
# app/build/outputs/apk/debug/app-debug.apk
```

## 已知限制

1. **全局切换**: 目前实现的是全局音频切换（非真正的音频分流）
2. **音频延迟**: 切换可能有1-2秒延迟
3. **后台存活**: 部分设备需要手动将应用加入白名单

## 兼容性

- 最低Android版本: API 26 (Android 8.0)
- 目标Android版本: API 34 (Android 14)
- 特别适配: 荣耀MagicOS、华为EMUI、小米MIUI、OPPO ColorOS等

## 许可证

本项目仅供学习交流使用，请勿用于商业目的。
