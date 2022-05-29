# Corriendo las Pruebas

MobSF usa Tox para ejecutar las pruebas. Tox se deberá de instalar fuera del virtualenv.

```bash
pip install tox
```

**Para usar el lintern**

```bash
tox -e lint
```

**Para usar el lintern y correr las pruebas**

```bash
tox -e lint,test
```
