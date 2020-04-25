# Running Tests
We use tox for running tests. Install tox outside virtualenv.
```bash
pip install tox
```

**For linting**
```bash
tox -e lint
```

**For running lint + test**
```bash
tox -e lint,test
```
