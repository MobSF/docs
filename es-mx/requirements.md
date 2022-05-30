# Requisitos

## Análisis Estático

* **MacOS**
  * Instalar [Git](https://www.atlassian.com/git/tutorials/install-git).
  * Instalar [Python **3.8 o 3.9**](https://www.python.org/).
  * Después de instalar Python 3.8+: Se debe de ir a `/Applications/Python 3.8/` y ejecutar `Update Shell Profile.command`, después ejecutar `Install Certificates.command`.
  * Instalar el [JDK 8+](https://www3.ntu.edu.sg/home/ehchua/programming/howto/JDK_Howto.html).
  * Instalar las command line tools con el comando `xcode-select --install`.
  * Descargar e instalar [wkhtmltopdf](https://wkhtmltopdf.org/downloads.html) como se indica en las [instrucciónes](https://github.com/JazzCore/python-pdfkit/wiki/Installing-wkhtmltopdf).
  * Para realizar un análisis estático de una aplicación de Windows se necesita una computadora con Windows o una máquina virtual en Mac o Linux. [Más información](https://github.com/MobSF/Mobile-Security-Framework-MobSF/blob/master/mobsf/install/windows/readme.md).

* **Distribuciones de Linux basadas en Ubuntu/Debian**:
  * Instalar Git `sudo apt-get install git`.
  * Instalar Python **3.8 o 3.9** `sudo apt-get install python3.8`.
  * Instalar el JDK 8+ `sudo apt-get install openjdk-8-jdk`.
  * Instalar las siguientes dependencias:
    ```bash
    sudo apt install python3-dev python3-venv python3-pip build-essential libffi-dev libssl-dev libxml2-dev libxslt1-dev libjpeg8-dev zlib1g-dev wkhtmltopdf
    ```
  * Para realizar un análisis estático de una aplicación de Windows se necesita una computadora con Windows o una máquina virtual en Mac o Linux. [Más información](https://github.com/MobSF/Mobile-Security-Framework-MobSF/blob/master/mobsf/install/windows/readme.md).

* **Windows**
  * Instalar [Git](https://git-scm.com/download/win).
  * Instalar [Python **3.8 o 3.9**](https://www.python.org/).
  * Instalar [JDK 8+](https://www3.ntu.edu.sg/home/ehchua/programming/howto/JDK_Howto.html).
  * Instalar [Microsoft Visual C++ Build Tools](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=BuildTools&rel=16).
  * Instalar [OpenSSL (non-light)](https://slproweb.com/products/Win32OpenSSL.html).
  * Descargar e instalar [wkhtmltopdf](https://wkhtmltopdf.org/downloads.html) como se indica en las [instrucciónes](https://github.com/JazzCore/python-pdfkit/wiki/Installing-wkhtmltopdf).
  * Añadir el directorio que contiene el binario de `wkhtmltopdf` a la variable de ambiente `PATH`.

?> **IMPORTANTE:** Establecer la variable de entorno `JAVA_HOME`. Análisis IPA para iOS solo funciona en **MacOS, Linux y dentro de contenedores de Docker**.

***

## Análisis Dinámico

* **El análisis dinámico no funcionará si se usa MobSF dentro de un contenedor de Docker o dentro de una máquina virtual.**
* Instalar [Genymotion](https://www.genymotion.com/fun-zone/) o [Genymotion Cloud VM](https://www.genymotion.com/cloud/) o [Android Studio Emulator](https://developer.android.com/studio).
