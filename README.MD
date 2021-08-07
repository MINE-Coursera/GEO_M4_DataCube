# Despliegue del Open Data Cube 1.8.2

El [Open Data Cube](https://www.opendatacube.org/) proporciona un entorno que facilita el análisis de datos de observación de la tierra mediante el lenguaje de programación Python. Los pasos que se listan a continuación despliegan el ambiente del Open Data Cube para inicar el proceso de análisis de imágenes satelitales.

**Nota importante**
El cubo de datos que vamos a usar está instalado en una máquina virtual con sistema operacional Linux que vamos a acceder desde Windows.

## Requerimientos

1. Computador con mímino 8 GB de Memoria RAM.
2. Sistema Operativo Windows 10.
3. Descarge las imágenes Sentinel 2 disponibles en el siguiente [enlace](https://drive.google.com/drive/folders/1eNWlKCcia3FsnhFA7k61m3pnkFp3OiF6?usp=sharing) antes de continuar el proceso.

## Pasos de configuración

El despliegue automatizado del Open Data Cube sin necesidad de entrar en detalles técnicos utiliza las herramientas Virtualbox y Vagrant. 

1. Descargue e instale la herramienta [Virtualbox 6.1.22](https://download.virtualbox.org/virtualbox/6.1.22/VirtualBox-6.1.22-144080-Win.exe).
2. Descargue e instale la herramienta [Vagrant 2.2.17](https://releases.hashicorp.com/vagrant/2.2.17/vagrant_2.2.17_x86_64.msi)
3. Reinicie su computador.

## Pasos de instalación del Open Data Cube 

Una vez instaladas las herramientas Virtualbox y Vagrant continue con los siguientes pasos.

0. Cree un directorio para alojar el Open Data Cube en una unidad con suficiente espacio y ponerle un nombre corto, diciente y sin caracteres especiales (Se sugiere algo del estilo D:\DataCube)
1. Descarge el siguiente archivo [datacube-tutorial-main.zip](https://github.com/MINE-Coursera/GEO_M4_DataCube/archive/refs/heads/main.zip) en el directorio creado para este efecto.
2. Descomprima el archivo `datacube-tutorial-main.zip`. Al descomprimir el archivo se creará la carpeta `datacube-tutorial-main`. Ingrese a este directorio.
3. Estando ubicando en el directorio `datacube-tutorial-main`, presione la tecla **shift + click derecho**, en el menú contextual seleccione "Abrir la ventana de PowerShell aquí".
4. En la consola de PowerShell que se despliega, digitar el siguiente comando.

```bash 
vagrant up
```

Este comando realiza el despliegue del Open Data Cube. La primera vez que se ejecuta el comando puede tomar Hasta 20 a 30 minutos, dependiendo de la velocidad de descarga de la red de su computador. 

En el proceso de ejecución del comando se puede observar información del estado de despliege de la herramientas Open Data Cube (Nota: Algunos mensajes pueden cambiar, sobre todo los que se refieren a los números de versión de las herramientas utilizadas).

```bash
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Checking if box 'hashicorp/bionic64' version '1.0.282' is up to date...
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
    default: 8080 (guest) => 8080 (host) (adapter 1)
    default: 8081 (guest) => 8081 (host) (adapter 1)
    default: 22 (guest) => 2222 (host) (adapter 1)
...

==> default: Running provisioner: shell...
    default: Running: inline script
    default: vagrant_postgis_1 is up-to-date
    default: Starting vagrant_explorer_1 ...
    default: vagrant_jupyter_1 is up-to-date
    default: Starting vagrant_explorer_1 ... done
    default: Initialising database...
    default: Updated.
    default: Checking indexes/views.
    default: Done.
    default: /home/datacube/.local/lib/python3.8/site-packages/flask_caching/__init__.py:201: UserWarning: Flask-Caching: CACHE_TYPE is set to null, caching is effectively disabled.
    default:   warnings.warn(
    default: Initialising schema
    default: Updating 1 products for LocalConfig<loaded_from=defaults, environment='default', config={'db_hostname': 'postgis', 'db_port': '5432', 'db_database': 'datacube', 'db_username': 'datacube', 'db_password': '***', 'index_driver': 'default', 'db_connection_timeout': '60'}>
    default: Generating product summaries...
    default: s2_sen2cor_ard_granule_EO3 done: (2 datasets)
    default: done. 1/1 generated, 0 failures
    default: Refreshing statistics...
    default: done
```

Al finalizar el proceso de despliegue, debe verificar en su consola de PowerShell que la última parte de la información desplegada sea similar a la que se muestra a continuación. Si no fue así entonces solicite asistencia.

```bash 
    default: Initialising schema
    default: Updating 1 products for LocalConfig<loaded_from=defaults, environment='default', config={'db_hostname': 'postgis', 'db_port': '5432', 'db_database': 'datacube', 'db_username': 'datacube', 'db_password': '***', 'index_driver': 'default', 'db_connection_timeout': '60'}>
    default: Generating product summaries...
    default: s2_sen2cor_ard_granule_EO3 done: (2 datasets)
    default: done. 1/1 generated, 0 failures
    default: Refreshing statistics...
    default: done
```

**Los pasos 3 y 4 deben ejecutarse cada vez que se quiera trabajar con el cubo de datos.**

Una vez instalada la máquina virtual, este proceso es mucho más rápido.

## Solución a posibles problemas

**Si al final del despliegue obtiene un error similar al que se muestra a continuación.**

```bash 
negative string size (or size too big) (argumenterror) 
````

Ingrese a `C:\Users\<su nombre de usuario>\`, busque el directorio `.vagrant.d` y renombrelo a `.vagrant.d.old`

Referencias:
1. https://github.com/hashicorp/vagrant/issues/10657
2. https://www.gitmemory.com/issue/hashicorp/vagrant/9146/541988622

## Acceso al Open Data Cube

En este momento, la máquina virtual que contiene el cubo está instalada y prendida.

Para acceder a cubo, vamos a utilizar una herramienta WEB llamada JupyterLab, con la cual, mediante notebooks (cuadernos de trabajo) podemos dar las instrucciones de manejo de las imágenes de satélite que requiramos.

Para esto, abra el navegador de su preferencias (Google Chrome o Mozila Firefox) e ingrese al siguiente enlace **[http://localhost:8080/lab](http://localhost:8080/lab).**

En el navegador aparece la interfaz gráfica de JupyterLab. JupyterLab es el ambiente que nos permite entender y desarrollar algoritmos que consultan el cubo de datos y nos permiten ejecutar análisis sobre las imágenes obtenidas a partir de esa consulta. 

## Apagar la máquina virtual que contiene el Open Data Cube

Una vez se termine de trabajar con el cubo de datos, es necesario apagar la máquina virtual, pues está consumiendo recursos (memoria principal, procesador y red) de la máquina real y esto puede afectar el funcionamiento de la misma. Para esto:

1. En la ventana Power Shell, dar el comando `vagrant halt`.

## Borrar/destruir la máquina virtual que contiene el Open Data Cube

Finalmente cuando ya no se quiera más trabajar con el cubo, se puede borrar la máquina virtual usando el comando `vagrant destroy` en la ventana de Power shell.

Si en algún momento se requiere de nuevo, sólo hay que repetir el proceso mostrado, creando de nuevo la máquina virtual con el comando `vagrant up`.


## Agradecimientos

- [German Bravo]()
- [David Niño](https://github.com/dfnino10) 

## Licencia

Todos los derechos reservados 2021. Desarrollado por Universidad de los Andes. 
