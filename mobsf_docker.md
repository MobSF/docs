# Running MobSF

?> You must have [docker](https://docs.docker.com/get-docker/) installed to run MobSF.


## Download

You should always download the `latest` tagged MobSF docker image to get the most upto date version, features, security, and bug fixes. We also offer versioned [releases](https://hub.docker.com/r/opensecurity/mobile-security-framework-mobsf/tags) which are behind the latest version.

```
docker pull opensecurity/mobile-security-framework-mobsf:latest
```

## Run

### Run MobSF with Static Analysis Support

```
docker run -it --rm -p 8000:8000 opensecurity/mobile-security-framework-mobsf:latest
```

### Run MobSF with Static & Dynamic Analysis Support

You can also run MobSF with both Static and Dynamic Analysis support using the docker image from MobSF v3.6.9 onwards.

!> You must run any of the **[supported](dynamic_analyzer.md)** Genymotion Android VM/ Android Studio Emulator before running MobSF. Read [this](dynamic_analyzer.md) before proceeding.

```
docker run -it --rm -p 8000:8000 -p 1337:1337 -e MOBSF_ANALYZER_IDENTIFIER=<adb device identifier> opensecurity/mobile-security-framework-mobsf:latest
```

?> MobSF only supports Dynamic Analysis with **rooted** Android version 4.1 to 11.0 upto API 30. Android version 12 and above are not supported.

iOS Dynamic Analysis

```
docker run -it --rm -p 8000:8000 -p 1337:1337 -e MOBSF_CORELLIUM_API_KEY=<corellium api key> opensecurity/mobile-security-framework-mobsf:latest
```

More common docker options are available under [MobSF Docker Options](docker.md)