# 运行 MobSF

?> 您必须安装 [docker](https://docs.docker.com/get-docker/) 才能运行 MobSF。


＃＃ 下载

您应该始终下载标记为“最新”的 MobSF docker 映像，以获得最新版本、功能、安全性和错误修复。我们还提供最新版本背后的版本控制[releases](https://hub.docker.com/r/opensecurity/mobile-security-framework-mobsf/tags)。

```
docker pull opensecurity/mobile-security-framework-mobsf:latest
```

＃＃ 跑步

### 运行带有静态分析支持的 MobSF

```
docker run -it --rm -p 8000:8000 opensecurity/mobile-security-framework-mobsf:latest
```

### 运行具有静态和动态分析支持的 MobSF

您还可以使用 MobSF v3.6.9 及以上版本的 docker 映像运行具有静态和动态分析支持的 MobSF。

!> 在运行 MobSF 之前，您必须运行任何 **[支持](dynamic_analyzer.md)** Genymotion Android VM/Android Studio 模拟器。在继续之前请阅读[此](dynamic_analyzer.md)。

```
docker run -it --rm -p 8000:8000 -p 1337:1337 -e MOBSF_ANALYZER_IDENTIFIER=<adb device identifier> opensecurity/mobile-security-framework-mobsf:latest
```

?> MobSF 仅支持 **rooted** Android 版本 4.1 至 11.0 直至 API 30 的动态分析。不支持 Android 版本 12 及更高版本。

更多常见的 docker 选项可在 [MobSF Docker Options](docker.md) 下找到