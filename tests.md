# Running Tests
We use tox for running tests. Install tox outside virtualenv.
```bash
pip install tox
```

**For linting**
```bash
tox -e lint
```
!> linting does not work on Windows


**For running lint + test**
```bash
tox -e lint,test
```