# Running MobSF

?> You'll need to have [Docker](https://docs.docker.com/get-docker/) installed to run MobSF, and it’s recommended to use version 20.10.0 or higher for the best experience.

To ensure you have the latest features, security updates, and bug fixes, it's best to download the most recent `latest` tagged MobSF Docker image. We also provide versioned [releases](https://hub.docker.com/r/opensecurity/mobile-security-framework-mobsf/tags), though they may not include the latest updates.

## Static Analysis

### Run MobSF with Static Analysis Support

Download the latest docker image and run the MobSF container.

```
docker pull opensecurity/mobile-security-framework-mobsf:latest
docker run -it --rm \
    -p 8000:8000 \
    opensecurity/mobile-security-framework-mobsf:latest
```

You can now access the MobSF web interface by opening `http://127.0.0.1:8000` in your browser. Use the default login credentials: `mobsf/mobsf`.

## Dynamic Analysis
### Run MobSF with Static & Dynamic Analysis Support

You must run any of the **[supported](dynamic_analyzer_docker.md)** (Genymotion Android VM/ Android Studio Emulator/ Corellium VM) and obtain the `MOBSF_ANALYZER_IDENTIFIER` before running MobSF.

```
docker run -it --rm \
    -p 8000:8000 \
    -p 1337:1337 \
    -e MOBSF_ANALYZER_IDENTIFIER=<adb device identifier> \
    opensecurity/mobile-security-framework-mobsf:latest
```

See how you can obtain the correct value for `<adb device identifier>` [here](dynamic_analyzer_docker.md).

!> On Ubuntu and other Linux-based systems, make sure your Docker version is >= `20.10.0`. When running the MobSF Docker container, add the extra option `--add-host=host.docker.internal:host-gateway`. Without this setting, the MobSF Docker container will be unable to communicate with the Android VM/emulator running on `localhost` of the host machine. You may also need to forward traffic to the emulator by following the instructions below.

```
# Install socat
sudo apt install socat

# Run start_avd script
scripts/start_avd.sh <avd-name>
# The script will output the MOBSF_ANALYZER_IDENTIFIER
```
```
# Example usage:
$ scripts/start_avd.sh Pixel_5_API_30
...
...
socat listener started on port 5556 forwarding to 5555 in the host.
Docker users please set the environment variable MOBSF_ANALYZER_IDENTIFIER=host.docker.internal:5556 for adb connectivity.

docker run -it --rm \
    -p 8000:8000 \
    -p 1337:1337 \
    --add-host=host.docker.internal:host-gateway \
    -e MOBSF_ANALYZER_IDENTIFIER=host.docker.internal:5556 \
    opensecurity/mobile-security-framework-mobsf:latest
```


?> MobSF only supports Dynamic Analysis with **rooted** Android version `4.1` to `11.0` upto `API 30`. Android version `12` and above are not supported.


### Run MobSF with iOS Dynamic Analysis Support

Obtain a Corellium [API key](https://app.corellium.com/login) before running MobSF.

```
docker run -it --rm \
    -p 8000:8000 \
    -p 1337:1337 \
    -e MOBSF_CORELLIUM_API_KEY=<corellium api key> \
    opensecurity/mobile-security-framework-mobsf:latest
```

## MobSF Tutorials

This video from Defcon Demo Labs 2020 explains some of the basic features of MobSF.

<iframe width="760" height="515" src="https://www.youtube.com/embed/1NIQs82n3nw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

If you're just getting started with MobSF, the [Automated Mobile Application Security Assessment with MobSF](https://opsecx.com/index.php/product/automated-mobile-application-security-assessment-with-mobsf/) course is a great way to dive in. It’s designed to walk you through MobSF’s key features and show you how to get the most out of the tool, making it perfect for beginners.

### Other Resources

* [Past MobSF Presentations & Slides](https://mobsf.github.io/Mobile-Security-Framework-MobSF/presentations.html)
* [Community Generated Playlist](https://youtube.com/playlist?list=PLX3EwmWe0cS9SRHpuuiRA-CsxevX3hh6o&si=5o3Mt6a6q9lmvuDn)