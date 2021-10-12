# テストの実行
テストの実行にはtoxを使用します。virtualenv外でtoxをインストールしてください。
```bash
pip install tox
```

**lintの実行**
```bash
tox -e lint
```

**lintとテストの実行**
```bash
tox -e lint,test
```
