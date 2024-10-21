# Laboratori0

# Compilar un Kernel

## Introduccion

El kernel es el núcleo del sistema operativo. En el caso de Linux, el kernel es de código abierto, lo que significa que cualquiera puede descargarlo, modificarlo y distribuirlo

La compilación del kernel de Linux es un proceso en el que se toma el código fuente del kernel, se configura según las necesidades específicas del sistema y se transforma en un archivo binario ejecutable que el sistema operativo puede utilizar para gestionar el hardware y los procesos. El kernel es la parte central del sistema operativo y actúa como un intermediario entre el hardware del equipo y las aplicaciones de software.

### ¿Por qué compilar un kernel?

La mayoría de las distribuciones de Linux vienen con un kernel precompilado que ya está configurado para funcionar en la mayoría de los sistemas.Sin embargo, hay varias razones para compilar un kernel personalizado:

- Optimización del rendimiento: Puedes eliminar características no necesarias, reduciendo el tamaño del kernel y mejorando el rendimiento.
- Compatibilidad de hardware: Algunos controladores específicos de hardware pueden no estar incluidos en el kernel predeterminado y deben ser activados manualmente.
- Actualización a una versión más reciente: Puedes compilar una versión más nueva del kernel para aprovechar las últimas mejoras y correcciones de seguridad.
- Personalización avanzada: Puedes habilitar funciones experimentales o específicas que no están disponibles en los kernels precompilados.

Una de las mejores razones para compilar un kernel es para aprender cómo funciona el Kernel de Linux, ampliar conocimientos sobre el hardware de nuestra máquina y saber como funciona el sistema operativo.

### Pasos a seguir

1. Instalar las dependencias necesarias: Abre una terminal en tu Debian y ejecuta los siguientes comandos para instalar las herramientas esenciales:

#### sudo apt update

#### sudo apt install build-essential libncurses-dev bison flex libssl-dev libelf-dev

Instala las herramientas necesarias para compilar un kernel:

- build-essential: Incluye el compilador gcc y otras herramientas esenciales para compilación.
- libncurses-dev: Biblioteca utilizada para crear interfaces de configuración del kernel en modo texto.
- bison y flex: Herramientas para analizar y generar código en la configuración y compilación del kernel.
- libssl-dev: Necesario para incluir soporte de cifrado en el kernel.
- libelf-dev: Proporciona soporte para archivos de formato ELF, comúnmente usados en el kernel.

![u](https://github.com/RaulRiCi/Sistemas_UnixLinux_Kernel/blob/main/Capturas/update.png?raw=true)

## 2. Descargar el código fuente del kernel:

Dirígete al sitio oficial de kernel.org para obtener la última versión estable del kernel o ejecuta este comando:

![w](https://github.com/RaulRiCi/Sistemas_UnixLinux_Kernel/blob/main/Capturas/wget.png?raw=true)

- wget: Descarga el archivo fuente del kernel desde el sitio oficial.

- Sustituye "6.x" por la versión que desees descargar.

## 3. Extraer el archivo descargado

![t](https://github.com/RaulRiCi/Sistemas_UnixLinux_Kernel/blob/main/Capturas/tar.png?raw=true)

![cd](https://github.com/RaulRiCi/Sistemas_UnixLinux_Kernel/blob/main/Capturas/cd.png?raw=true)

- tar -xvf linux-6.11.3-tar.xz: Extrae el archivo comprimido del kernel.
- cd linux-6.11.3: Cambia el directorio actual al directorio donde se extrajo el código fuente.

## 4. Configurar el Kernel

Para la compilación del Kernel se utiliza un fichero .config que usará el comando make para construirlo.

Vamos a usar el fichero de configuración del kernel actual en uso para simplificar el proceso, para ello lo copiaremos en nuestro directorio actual del código fuente y lo cambiaremos de nombre, lo hacemos directamente con el siguiente comando:

![uname](https://github.com/RaulRiCi/Sistemas_UnixLinux_Kernel/blob/main/Capturas/uname.png?raw=true)

- cp /boot/config-$(uname -r) .config : Copia la configuración del kernel actual
- (config-$(uname -r)) al archivo .config en el directorio de compilación para utilizarla como base.

### Iniciar la configuración del nuevo kernel:

Ésta es la opción más usada para la compilación del Kernel, se utiliza si no dispones de un entorno gráfico instalado en tu equipo (por ejemplo si compilas el kernel desde un servidor). Para iniciarlo ejecuta:

![makemenu](https://github.com/RaulRiCi/Sistemas_UnixLinux_Kernel/blob/main/Capturas/menu.png?raw=true)

![menu2](https://github.com/RaulRiCi/Sistemas_UnixLinux_Kernel/blob/main/Capturas/menu2.png?raw=true)

La manera de usarlo es mediante las flechas del teclado, el tabulador para cambiar entre opciones y la barra espaciadora para marcar/desmarcar opciones o cambiar algo a tipo 'modulo'.

En la captura anterior, hemos marcado 'Virtualización', deberemos entrar en las subopciones de esta opción. Para ello una vez marcado hay que escoger 'Select' para acceder y dentro de esta opción escoger lo que deseemos:

![menu3](https://github.com/RaulRiCi/Sistemas_UnixLinux_Kernel/blob/main/Capturas/menu3.png?raw=true)

Si queremos disponer de algo de ayuda sobre lo que estamos seleccionando, deberemos ir hasta 'Help' para que nos muestre un menú con la información de la opción actual:

![menu4](https://github.com/RaulRiCi/Sistemas_UnixLinux_Kernel/blob/main/Capturas/menu4.png?raw=true)

## 5. Compilar el Kernel

La parte más difícil para nosotros, que es la revisión detallada de lo que queremos que tenga y haga nuestro kernel ya está realizada, ahora vamos a darle trabajo a nuestro equipo para que compile el kernel.
Para compilar el Kernel, simplemente tienes que ejecutar:

- make -j$(nproc): Compila el kernel utilizando todos los núcleos de CPU disponibles. $(nproc) obtiene automáticamente el número de núcleos en el sistema para acelerar el proceso.

![nproc](https://github.com/RaulRiCi/Sistemas_UnixLinux_Kernel/blob/main/Capturas/nproc.png?raw=true)

## 6. Instalar los módulos

Una vez compilado el kernel sin errores, tienes que compilar los módulos que seleccionaste en la configuración para usar como módulos extra por el kernel.
Se compilarán e instalarán automáticamente en la ruta necesaria de tu equipo para que sean accesibles por tu nuevo kernel, para ello ejecuta el comando:

![modules](https://github.com/RaulRiCi/Sistemas_UnixLinux_Kernel/blob/main/Capturas/modules.png?raw=true)

- sudo make modules_install: Instala los módulos del kernel en /lib/modules/6.x, donde "6.x" es la versión del kernel que se está compilando.

## 7. Instalar el Kernel

Si todo ha salido correctamente y no hemos obtenido ningún error en la compilación, ya tenemos preparado nuestro Kernel para poder usarlo.

Para instalarlo simplemente ejecuta:

![install](https://github.com/RaulRiCi/Sistemas_UnixLinux_Kernel/blob/main/Capturas/install.png?raw=true)

- sudo make install: Copia los archivos del kernel (como vmlinuz, System.map, etc.) al directorio /boot y actualiza automáticamente el cargador de arranque GRUB.

## 8. Actualizar el cargador de arranque y reiniciar

Ahora debemos preparar nuestro 'boot-loader' para que pueda iniciar con él.
Para ello ejecuta lo siguiente:

![ugrup](https://github.com/RaulRiCi/Sistemas_UnixLinux_Kernel/blob/main/Capturas/updategrup.png?raw=true)

![reboot](https://github.com/RaulRiCi/Sistemas_UnixLinux_Kernel/blob/main/Capturas/reboot.png?raw=true)

- sudo update-grub: Actualiza la configuración de GRUB para incluir el nuevo kernel.
- sudo reboot: Reinicia el sistema para arrancar con el nuevo kernel.

## 9. Verificar la instalación

![r](https://github.com/RaulRiCi/Sistemas_UnixLinux_Kernel/blob/main/Capturas/r.png?raw=true)

uname -r: Muestra la versión del kernel que está en ejecución, la cual debería ser la que acabas de compilar.
