
# 安装

如果您是 MobSF 的新手，请尝试 [easy install](/zh-cn/mobsf_docker.md)。


## 遗留步骤


**在 Windows 10, Ubuntu (18.04, 19.04) , macOS Catalina 测试**

!> 请确认首先安装了所有 [要求](requirements.md) 里的内容


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

?> Windows用户在运行`setup.bat`之前，请关闭所有MobSF打开过的文件夹和用MobSF打开过的文本编辑器。 这些都会因为引起权限错误造成安装中断。


# 运行MobSF

## Linux/Mac

```bash
./run.sh 127.0.0.1:8000
```

***

## Windows

```batch
run.bat 127.0.0.1:8000
```

!> 如果你在执行脚本时没有附带任何参数，那么 MobSF 将监听 `0.0.0.0:8000`。

在你的Web浏览器中，跳转到 `http://localhost:8000/` 以访问 MobSF Web界面。


