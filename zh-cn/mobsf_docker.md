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

您现在可以在网络浏览器中通过“http://127.0.0.1:8000”访问 MobSF 网络界面。

### 运行具有静态和动态分析支持的 MobSF

您还可以使用 MobSF v3.6.9 及以上版本的 docker 映像运行具有静态和动态分析支持的 MobSF。

!> 在运行 MobSF 之前，您必须运行任何 **[支持](dynamic_analyzer.md)** Genymotion Android VM/Android Studio 模拟器。在继续之前请阅读[此](dynamic_analyzer.md)。

```
docker run -it --rm -p 8000:8000 -p 1337:1337 -e MOBSF_ANALYZER_IDENTIFIER=<adb device identifier> opensecurity/mobile-security-framework-mobsf:latest
```

?> MobSF 仅支持 **rooted** Android 版本 4.1 至 11.0 直至 API 30 的动态分析。不支持 Android 版本 12 及更高版本。


iOS动态分析

```
docker run -it --rm -p 8000:8000 -p 1337:1337 -e MOBSF_CORELLIUM_API_KEY=<corellium api key> opensecurity/mobile-security-framework-mobsf:latest
```

更多常见的 docker 选项可在 [MobSF Docker Options](docker.md) 下找到


## 如何使用 MobSF

来自 Defcon Demo Labs 2020 的这段视频解释了 MobSF 的一些基本功能。

<iframe width="760" height="515" src="https://www.youtube.com/embed/1NIQs82n3nw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
### 其他资源

* [过去的 MobSF 演示文稿和幻灯片](https://mobsf.github.io/Mobile-Security-Framework-MobSF/presentations.html)
* [电子学习课程：使用 MobSF -MAS 进行自动化移动应用程序安全评估](https://opsecx.com/index.php/product/automated-mobile-application-security-assessment-with-mobsf/)