# 漫画翻译器 Android MVP 0.1

这是可继续编译的 Android Studio 项目源代码，不是已经签名的 APK。当前环境没有 Android SDK/Gradle，无法在这里可靠构建和测试 APK。

## 已实现
- Android WebView 打开 HTTPS 漫画网站
- 日文、韩文、中文 OCR 选项（ML Kit）
- 截取 WebView 当前可见区域并识别文字
- 调用 MyMemory 公共翻译 API 将识别行翻译为简体中文
- 在原页面上用白底黑字覆盖层显示翻译
- 清除翻译、返回网页、网页地址栏

## 当前限制（请先阅读）
- 这是验证流程的 MVP：不是逐字完美嵌字。覆盖区域按 OCR 文本框近似定位，可能遮挡原画；复杂气泡、竖排日文、拟声词、跨行文本会有误差。
- 只处理当前屏幕，不会自动连续翻译整章；页面滚动后需再次点击识别。
- 翻译通过 MyMemory 公共 API 在线完成，免费服务有速率/隐私/可用性限制；不要输入敏感内容。
- 某些漫画网站会阻止 WebView、登录或反自动化；不绕过付费墙、登录限制或 DRM。只对有权访问的网页使用。
- 网页本身若使用 DRM、canvas、跨域受限或受保护视频式渲染，WebView 截图可能无法捕获其漫画图像。
- ML Kit 的日文/韩文/中文模型首次使用时可能需要联网下载。
- 当前版本不包含图像修复（去除原文后重建背景），所以不是专业汉化质量。

## 编译成 APK
1. 在电脑安装 Android Studio（建议稳定版）与 Android SDK Platform 35。
2. 解压项目 ZIP，在 Android Studio 中选择 `Open`，打开 `MangaTranslateAndroid` 文件夹。
3. 等待 Gradle Sync 下载依赖（需要网络）。
4. 连接安卓手机，打开开发者选项与 USB 调试；或使用模拟器。
5. 点 Run 安装调试版，或选择 **Build > Build APK(s)**。
6. 通常输出在 `app/build/outputs/apk/debug/app-debug.apk`。
7. 将 APK 传到手机，允许该来源安装应用后安装。调试 APK 不适合公开发布。

## 依赖
- Android Gradle Plugin 8.7.3
- Kotlin 2.0.21
- AndroidX Core KTX 1.15.0、AppCompat 1.7.0
- Google ML Kit Text Recognition Japanese/Korean/Chinese 16.0.1
- MyMemory Translation API（在线）

## 下一步建议
1. 加入页面内图片定位和逐气泡区域检测。
2. 加入可拖动/编辑的译文框、字号与底色调节。
3. 增加翻译缓存、限流和可替换翻译引擎。
4. 做图像修复与漫画纵向阅读优化。

## 手机云端编译（GitHub Actions）
项目现附带 `.github/workflows/android.yml`，推送到 `main` 后会自动构建；也可在仓库 Actions 页面手动运行 `Build MangaTranslate APK`。成功后打开该次运行页面底部的 Artifacts，下载 `MangaTranslate-debug-apk`，解压即可得到 `app-debug.apk`。GitHub Actions 标准 runner 对公开仓库免费；公开仓库中的源代码对所有人可见，上传前请确认不含隐私或密钥。GitHub 账号与网页操作是必需的。# MangaTranslate
