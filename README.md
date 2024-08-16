USAC Linux
1. Instalación de Dependencias
Para preparar el entorno de compilación del kernel, es necesario instalar los paquetes esenciales. Se deben instalar herramientas de desarrollo y bibliotecas necesarias para el proceso de compilación.

2. Descargar el Código Fuente del Kernel
El siguiente paso es obtener el código fuente del kernel. Visite el sitio oficial de kernel.org y descargue la versión longterm del kernel (6.6.45 en el momento actual). Obtenga el enlace para la opción tarball y descargue el archivo correspondiente. Luego, proceda a descomprimir el archivo descargado.

3. Configuración del Kernel
Con el código fuente descargado y descomprimido, el siguiente paso es configurar el kernel:

Navegue al directorio del código fuente del kernel.

Copie la configuración actual del kernel al archivo .config. Esto asegura que la nueva configuración esté basada en la configuración del kernel que actualmente se está utilizando.

Utilice la herramienta localmodconfig para ajustar la configuración del kernel, eliminando módulos y drivers innecesarios. Esto reducirá el tiempo de compilación y adaptará el kernel a su sistema específico. Tenga en cuenta que esta configuración hará que el kernel compilado funcione únicamente en su máquina.

Modifique el archivo .config para eliminar cualquier referencia a llaves privadas que pudieran haberse copiado.

4. Compilación del Kernel
Con la configuración del kernel en su lugar, puede proceder a la compilación. Utilice todos los núcleos disponibles para acelerar el proceso de compilación. FakeRoot es una herramienta que permite ejecutar comandos con privilegios de superusuario sin necesidad de permisos de root, lo cual es necesario para la compilación del kernel. La opción de compilación en paralelo optimiza el uso de todos los núcleos del procesador.

Una vez completada la compilación, verifique que la imagen del kernel se haya generado correctamente. La herramienta de verificación debería indicar éxito con un código de retorno de 0.

5. Instalación del Kernel
Para instalar el kernel, primero instale los módulos del kernel. Posteriormente, proceda a instalar el kernel en sí.

6. Configuración del GRUB
Para que el sistema arranque con el nuevo kernel, es necesario actualizar la configuración de GRUB:

Instale GRUB Customizer, una herramienta gráfica para configurar GRUB.

Abra GRUB Customizer y seleccione el nuevo kernel como predeterminado. Configure otras opciones de GRUB según sea necesario y guarde los cambios.

Reinicie el sistema y seleccione el nuevo kernel en el menú de GRUB para iniciar el sistema con la nueva versión del kernel. Verifique que el kernel se haya instalado correctamente ejecutando el comando apropiado.

7. Configuración Inicial
Para personalizar el kernel, puede agregar un mensaje de bienvenida en el archivo init/main.c utilizando la función printk. Además, puede modificar el nombre del sistema mostrado por el comando uname editando la definición de UTS_SYSNAME en el archivo include/linux/uts.h.

Compile nuevamente el kernel y reinicie el sistema para aplicar estos cambios.

8. Implementación de Llamadas al Sistema
Las llamadas al sistema permiten que los programas de usuario soliciten servicios del kernel. Se añadirán tres llamadas al sistema personalizadas: get_current_time, get_uptime, y get_last_5_kernel_logs. Estas llamadas permitirán obtener la hora actual, el tiempo de actividad del sistema, y los últimos 5 mensajes del kernel, respectivamente.

Modifique el archivo kernel/sys.c para implementar las nuevas llamadas al sistema.

Actualice el archivo include/linux/syscalls.h para declarar las nuevas llamadas al sistema.

Edite el archivo arch/x86/entry/syscalls/syscall_64.tbl para definir las nuevas llamadas al sistema.

Compile el kernel nuevamente y reinicie el sistema para reflejar estos cambios.

9. Prueba de las Nuevas Llamadas al Sistema
Cree una aplicación de usuario para probar las nuevas llamadas al sistema. Compile el código de prueba y ejecute el programa para verificar que las llamadas al sistema devuelvan los resultados esperados, como la hora actual, el tiempo de actividad y los últimos 5 mensajes del kernel.

Con esto, se ha completado la configuración del kernel para USAC Linux.