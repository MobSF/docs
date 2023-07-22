# Running MobSF

?> You must have [docker](https://docs.docker.com/get-docker/) installed to run MobSF.


## Download the latest MobSF docker image

```
docker pull opensecurity/mobile-security-framework-mobsf:latest
```

## Run MobSF (Only Static Analysis)

```
docker run -it --rm -p 8000:8000 opensecurity/mobile-security-framework-mobsf:latest
```

## Run MobSF with Static and Dynamic Analysis Support 

!> You must run any of the **[supported](dynamic_analyzer.md)** Genymotion Android VM/Android Studio Emulator before running MobSF. Read [this](dynamic_analyzer.md) before proceeding.

```
docker run -it --rm -p 8000:8000 -p 1337:1337 -e MOBSF_ANALYZER_IDENTIFIER=<adb device identifier> opensecurity/mobile-security-framework-mobsf:latest
```


?> MobSF only supports Dynamic Analysis with Android version 4.1 to 11.0 upto API 30. Android version 12 and above are not supported.

More common docker options are available under [MobSF Docker Options](docker.md)