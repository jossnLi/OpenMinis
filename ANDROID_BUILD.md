# Android APK 构建说明

## 已完成的工作

### 1. 图标替换（ChatGPT 风格）
已将 26 个 Android 文件中的图标替换为简洁线性风格：
- Settings → Tune
- Extension → Dashboard  
- Psychology → Memory
- Forum → Chat
- ChatBubbleOutline → Chat
- Inventory2 → Archive

### 2. GitHub Actions 工作流配置
已创建 .github/workflows/build-android.yml 用于云端自动构建。

## 使用 GitHub Actions 构建 APK

### 步骤：

1. **提交代码到 GitHub**
   ```bash
   git add .
   git commit -m "Update Android icons and add build workflow"
   git push origin main
   ```

2. **触发构建**
   - 自动触发：推送到 main 或 master 分支
   - 手动触发：访问 GitHub 仓库 → Actions → Build Android APK → Run workflow

3. **下载 APK**
   - 构建完成后，在 Actions 运行记录中找到 openminis-release-apk
   - 下载 artifacts 中的 APK 文件

### 构建流程

工作流会自动执行：
1. 配置 JDK 17、Android SDK、NDK、CMake
2. 安装 Go 和 gomobile
3. 构建原生依赖：PRoot、Alpine sandbox、Rclone AAR  
4. 编译 Android APK（Release 版本）
5. 上传构建产物

**首次构建时间**：约 30-60 分钟  
**后续构建**：约 15-30 分钟（有缓存）

## 注意事项

1. **首次构建**：需要完整构建所有原生依赖，耗时较长
2. **签名配置**：当前使用 debug 签名
3. **保留时间**：APK 产物保留 30 天