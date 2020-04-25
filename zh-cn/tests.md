# 运行测试
我们使用tox进行测试。 在 virtualenv 外部安装tox。
```bash
pip install tox
```

**用于风格检查**
```bash
tox -e lint
```
!> 风格检查在Windows上不起作用


**用于运行风格检查和测试**
```bash
tox -e lint,test
```