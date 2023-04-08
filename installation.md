
# Installation


!> If you are new to MobSF, try [easy install](mobsf_docker.md) instead.


## Legacy Steps


**Tested on Windows 10, Ubuntu (18.04, 19.04) , macOS Catalina**

!> Please make sure that all the [requirements](requirements.md) mentioned are installed first.


## Linux/Mac
```bash
git clone https://github.com/MobSF/Mobile-Security-Framework-MobSF.git
cd Mobile-Security-Framework-MobSF
./setup.sh
```
***

## Windows
```batch
git clone https://github.com/MobSF/Mobile-Security-Framework-MobSF.git
cd Mobile-Security-Framework-MobSF
setup.bat
```

?> Windows users, before running `setup.bat` close any opened folders of MobSF or text editors with MobSF opened. Either of these can interrupt the setup by causing permission errors.


# Running MobSF

## Linux/Mac
```bash
./run.sh 127.0.0.1:8000
```

***

## Windows

```batch
run.bat 127.0.0.1:8000
``` 

!> MobSF will listen to `0.0.0.0:8000` if you use the run script without arguments.

In your web browser, navigate to `http://localhost:8000/` to access MobSF web interface.
