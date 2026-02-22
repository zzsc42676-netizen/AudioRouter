---
AIGC:
    ContentProducer: Minimax Agent AI
    ContentPropagator: Minimax Agent AI
    Label: AIGC
    ProduceID: "00000000000000000000000000000000"
    PropagateID: "00000000000000000000000000000000"
    ReservedCode1: 3046022100851817764d14d57be42404b295e543ec385570006cab7cac356480875dddd108022100dc9eac11a3dc61f8f25d843a5fd2928e7e8fbfd0f1d0a35ebb6c73a7f6be9e14
    ReservedCode2: 304502210089eb8b5b4cc42437152b64b41c2d7ee07ba6dcfff9436c1a88f03b873694e900022012950aab2db430e076d0edbcf351e9670a5959a1fe28a3fe14b9e6003b0fb293
---

# GitHub 自动编译指南

本指南将帮助你使用 GitHub Actions 自动编译 Android APK，无需在本地安装 Android Studio。

## 步骤详解

### 步骤1: 创建 GitHub 仓库

1. 访问 https://github.com 并登录你的账号
2. 点击右上角的 **"+"** 按钮，选择 **"New repository"**
3. 填写仓库信息：
   - Repository name: `AudioRouter`（或其他名称）
   - Description: 荣耀手机音频路由工具
   - 选择 **Public**（免费）
   - 勾选 **"Add a README file"**（可选）
4. 点击 **"Create repository"**

### 步骤2: 上传代码

有两种方式上传代码：

#### 方式A: 使用 GitHub 网页上传（简单）

1. 在仓库页面，点击 **"Upload files"** 按钮
2. 将本地解压后的 `AudioRouter` 文件夹内的所有内容拖进去
3. 注意：需要上传隐藏文件（.github 等），点击"View all commits"旁边可以看到选项
4. 填写 commit 信息，点击 **"Commit changes"**

#### 方式B: 使用 Git 上传（推荐）

如果你安装了 Git：

```bash
# 1. 克隆空仓库到本地
git clone https://github.com/你的用户名/AudioRouter.git

# 2. 进入目录
cd AudioRouter

# 3. 将所有项目文件复制到这个目录

# 4. 添加所有文件
git add .

# 5. 提交
git commit -m "Initial commit"

# 6. 推送到 GitHub
git push origin main
```

### 步骤3: 等待自动构建

1. 上传代码后，点击仓库的 **"Actions"** 标签
2. 你会看到构建任务正在运行（橘黄色圆圈）
3. 等待约 3-5 分钟让 GitHub 下载 Android SDK 并编译
4. 如果成功，会显示绿色勾勾 ✓

### 步骤4: 下载 APK

1. 构建完成后，点击该次构建
2. 在页面底部找到 **"Artifacts"** 部分
3. 点击 **"app-debug.apk"** 即可下载编译好的 APK

---

## 常见问题

### Q: 构建失败了怎么办？

1. 点击失败的构建任务
2. 查看 **"build debug APK with Gradle"** 步骤的错误日志
3. 常见问题：
   - 代码错误：请检查是否上传了所有必要文件
   - 网络问题：GitHub 可能需要重试

### Q: 如何更新代码后重新构建？

1. 修改本地代码
2. 推送到 GitHub：
```bash
git add .
git commit -m "Update: 你的修改说明"
git push origin main
```
3. GitHub 会自动重新构建

### Q: 可以分享 APK 给朋友吗？

可以！下载的 APK 可以直接分享给他人安装使用。

### Q: 需要付费吗？

完全免费！GitHub Actions 每月提供 2000 分钟的免费构建时间，足够使用。

---

## 文件结构说明

上传到 GitHub 的文件应该包含：

```
AudioRouter/
├── .github/
│   └── workflows/
│       └── android-build.yml    # 自动构建配置
├── app/
│   └── src/main/               # 应用源代码
├── build.gradle                # 项目配置
├── settings.gradle
├── gradle.properties
├── local.properties
├── gradlew                    # Gradle 包装器
├── gradlew.bat
└── README.md
```

---

## 注意事项

1. 首次构建可能需要较长时间（需要下载 Android SDK）
2. 如果长时间显示"Queued"，可能是仓库设置了需要审核
3. 每次推送到 main 分支都会自动触发构建
