


# Informe Práctica 1: Configuración de máquina virtual en el IaaS


![Image](https://www.ull.es/servicios/stic/wp-content/uploads/sites/2/2016/05/VDI-1.png)



╔═══════════════════════════════════════════════════════════════════╗

> - Autora: Andrea Calero Caro
> - Alu: [alu0101202952@ull.edu.es](alu0101202952@ull.edu.es)
> - Práctica: 1 Configuración de máquina virtual en el IaaS
> - Asignatura: Desarrollo de Sistemas Informáticos
> - Universidad de La Laguna

╚═══════════════════════════════════════════════════════════════════╝



▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂


## Índice
  - Objetivos
  - Pasos previos
  - Configuración máquina IaaS
  - Instalación de git y node.js
  - Desarrollo del informe con GitHub Pages
  - Conclusiones
  - Bibliografía y/o Webgrafía
  
  


▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂


## OBJETIVOS
Los objetivos en esta práctica serán la configuración de la máquina virtual IaaS de la ULL, además de la instalación y configuración de todas las herramientas necesarias para comenzar a trabajar en la asignatura, como es git y node.js. Todo ello junto con la presentación de este informe y el desarrollo del mismo en GitHub Pages.



▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂


## PASOS PREVIOS

Antes de comenzar se nos requiere una serie de pasos previos para introducirnos en la asignatura.

1. Cumplimentar la encuesta de elección de grupo de trabajo, en mi caso estaría en el **"Grupo J"** de trabajo.

2. Cumplimentar la encuesta sobre expectativas y conocimientos previos, la cual ya he realizado.

3. Darse de alta en el aula Google Classroom de la asignatura. Para ello seleccionamos nuestro correo institucional y seleccionamos que somos **alumnos**.

4. Como ya poseía una cuenta GitHub asociada a mi correo institucional (alu0101202952@ull.edu.es), solicité los beneficios de GitHub Education y acepté la asignación del GitHub Classroom asociada a esta práctica. En caso contrario, debería de haberme creado dicha cuenta en la comunidad y realizar los pasos anteriores.

5. Como para el desarrollo de esta práctica y su respectivo informe necesito conocimientos en **GitHub Pages**, **Markdown** y **Jekyll**. Mediante diversas búsquedas en páginas web, las cuales muestro en el apartado bibliografía de este informe, conseguí realizar el susudicho con el estilo que se me requiere.



▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂


## CONFIGURACIÓN MÁQUINA IAAS

Lo primero para poder acceder al servicio de máquinas virtuales del IaaS es configurar la VPN, en mi caso ya la tengo configurada gracias a la aplicación de **GlobalProtect**, a la cual accedo a la VPN de la ULL introduciendo en el usuario `aluxxxxxxxxxx` y en la contraseña `contraseña_institucional`. Y así nos conectaríamos.
『』[VPN_acceso](https://drive.google.com/file/d/19OsVf77mYxXfyt7Qb0S1zYPXx1RQ3KTv/view)

Una vez dentro del servicio https://iaas.ull.es/ovirt-engine/, tras meterme con mi alu y contraseña, enciendo mi máquina virtual asignada en la asignatura de Desarrollo de Sistemas Informáticos (DSI) con un identificador, en mi caso es **DSI-31**.
『』[Máquina virtual DSI-31](https://drive.google.com/file/d/1aSENTWgb3IIfF8K_ADWfvdmqduShmMH4/view)

Cuando la enciendo, desde mi subsistema Linux Ubuntu 18.04 LTS me conecto a ella mediante el commando:

> `andreacc@DESKTOP-EMSOIU9:~$ ssh usuario@10.6.XXX.XXX` 
Esto con la IP de mi máquina virtual

Lo primero que se me pide es cambiar la contraseña actual (usuario) por una mía que pueda recordar. Tras ellos comenzaría a configurar el fichero **hostname** con el nombre de mi host en la máquina, esto será necesario para poder acceder a la máquina desde local mediante el host asignado:

**iaas-dsi31**

Mediante el comando: 
> `sudo vi /etc/hostname`

Pero además necesitamos modificar otro fichero para conseguir lo previsto, con:
> `sudo vi /etc/hosts`

Donde había antes: 
127.0.0.1	localhost
**127.0.1.1	ubuntu**

Pondría ahora:
127.0.0.1	localhost
**127.0.1.1	iaas-dsi31**

Ya con ello habríamos cambiado el nombre del host, para guardar los cambios necesitaríamos actualizar y reiniciar la máquina, para ello haría en orden:
> `sudo apt update`
> `sudo apt upgrade`
> `sudo reboot`  // Con esto reiniciaríamos

**MIENTRAS ESTA SE REINICIA VAMOS A CONFIGURAR EL ACCESO DE LOCAL A LA MÁQUINA VIRTUAL**

Como queríamos que nuestro local tuviera el host de la máquina virtual, para poder conectarnos a ella de forma más rápida, tendríamos que editar el fichero **hosts** mediante:
< `andreacc@DESKTOP-EMSOIU9:~$ sudo vi /etc/hosts`

Y añadir la ip y el host de nuestra máquina, en mi caso pondría:
...
> `10.6.XXX.XXX     iaas-dsi31`

Una vez que tenemos el host necesitaré configurar la llave pública-privada, con el comando:
> `andreacc@DESKTOP-EMSOIU9:~$ cat .ssh/id_rsa.pub`

Nos mostrará la llave:

『』[Llave pública-privada](https://drive.google.com/file/d/1tY3NSqwOnjAxTaY-txrG4an76O-ev7MD/view)

Como ya se generó el par de llaves no debo hacer nada más. A continuación, una vez generadas las claves, ejecuto el comando:
> `andreacc@DESKTOP-EMSOIU9:~$ ssh-copy-id usuario@iaas-dsi31`
Lo cual permitirá copiar mi clave pública desde la máquina local a la máquina virtual. Y trato de hacer inicio de sesion en la máquina virtual ejecutando el siguiente comando:
> `andreacc@DESKTOP-EMSOIU9:~$ ssh usuario@iaas-dsi31`

Con ello compruebo que ahora no necesito la ip de mi máquina y tampoco introducir contraseña, sino el host que tengo configurado para esta. Como tampoco quiero usar el nombre **usuario** para ello hago:
> `vi ~/.ssh/config `

Lo edito y pongo: 
『』[ssh/config](https://drive.google.com/file/d/1ATeEnR2ufiHdiJKhw0RFgrEwywdWwTCU/view)
     
Ahora se puede iniciar una conexión SSH simplemente indicando el nombre de la máquina virtual tal que:
> `andreacc@DESKTOP-EMSOIU9:~$ ssh iaas-dsi31 `


Finalmente, genero las claves pública-privada en mi máquina virtual también, siguiendo los pasos que seguí anteriormente:
> `ssh-keygen 
Generating public/private rsa key pair.
Enter file in which to save the key (/home/usuario/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again:
... `

> `usuario@iaas-dsi31:~$ cat .ssh/id_rsa.pub `

Generando así, la llave y finalizando la configuración de la máquina virtual.


▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂


## INSTALACIÓN DE GIT Y NODE.JS

Primero necesitamos instalar git mediante: 

> `sudo apt install git`

Y, una vez instalado todos los paquetes configuramos el git para vincularlo con nuestra cuenta de GitHub, tal que:
> `git config --global user.name "Andrea Calero Caro"`
> `git config --global user.email alu0101202952@ull.edu.es`
> `git config --list `  // Con este comando veremos cómo se listaría lo antes configurado

Quedando:
> `user.name=Andrea Calero Caro
   user.email=alu0101202952@ull.edu.es
   core.repositoryformatversion=0
   core.filemode=true
   core.bare=false
   core.logallrefupdates=true`
   
**AHORA SE CONFIGURARÍA EL PROMPT**

Para modificar el prompt se siguen dos pasos sencillos, esto para bash:
1. Descargar del script [git_prompt_script](https://github.com/git/git/blob/master/contrib/completion/git-prompt.sh)

Los pasos serían:
> `mv git-prompt.sh .git-prompt.sh`

2. Modificar el fichero  **~/.bashrc**, mediante:
> `vi ~/.bashrc`

Pegando al final del propio fichero las líneas:
『』[vi ~/.bashrc](https://drive.google.com/file/d/1g7BxsLxBsmQA_NeC6j0rAxt2HZtyLw6l/view)

Y así cambiaría el prompt quedando:
『』[Prompt](https://drive.google.com/file/d/1hcIhewQhMGEXu3yhr_feQveXSBOyqrvu/view)

Ahora reiniciaríamos para refrescar el prompt tal que:
> `exec bash -l`

##### Al finalizar: 

Como tendremos que trabajar remotamente con repositorios del **GitHub**, necesitamos enlazar la cuenta de git con nuetsra máquina, siguiendo los siguientes pasos:
1. Copiamos la llave pública de la máquina:
『』[Llave-máquina](https://drive.google.com/file/d/1FCHyVj-SUK576aw9YtwifFhVs26ZC_S8/view)

2. Vamos a la configuración de la cuenta en _Setting -> SSH and GPG keys_
『』[Setting](https://drive.google.com/file/d/1C2Oa1mzrrPfoUjxxVgrgrAraVysSAVFf/view)
『』[SSH and GPG keys](https://drive.google.com/file/d/1j6L5yQTB4dmAA23WYNu83gCPf1D5Q4dO/view)

3. Creamor una nueva llave en el **botón verde** _New SSH key_
『』[New SSH key](https://drive.google.com/file/d/1nD38rPk_ctYkgW10tn8fvhwsm-w4UZYb/view)

4. Rellenaríamos los campos título con _usuario@iaas-dsi31_ y el campo Key o llave con la llave ya copiada en el **paso 1**
『』[Add Key](https://drive.google.com/file/d/1AGFscblE97-UZAgUD9Ye-jNa0hirTVuZ/view)

5. Ahora clonaremos el repositorio que hemos aceptado de tarea, tal que:
> `git clone git@github.com:ULL-ESIT-INF-DSI-2021/ull-esit-inf-dsi-20-21-prct01-iaas-alu0101202952.git` 

6. Comprobamos con el comando `ls` y entramos en el repositorio clonado:
『』[cd repositorio](https://drive.google.com/file/d/1vxcm51UgAyT2LhbvMSOHrJAKCQHmHGlT/view)

##### Procedemos con la instalación de node.js y su control de versiones nvm

Node.js es un entorno que permite la ejecución de código desarrollado en JavaScript y variantes, como por ejemplo, TypeScript, con el cual trabajaremos en la asignatura, para ello ejecutamos los comandos:
『』[Instalar nvm](https://drive.google.com/file/d/1AhZan6jlpzNvfz9BnfNq3j2waaA6y0_t/view)

Y con el comando `nvm install node` instalamos el entorno de código desarrollado en JavaScript.

Como sabemos con el comando `... --version` veremos la versión con la que trabajaremos tanto en **node** como en **nvm**. En el caso del paquete que se nos instaló es la versión:
『』[Versiones instaladas por defecto](https://drive.google.com/file/d/1QiIXDlzp4Je0DHhiIAPzqmsUU8hr2M9A/view)

Para poder manejarnos entre versiones tenemos que saber unos comandos muy útiles como:

##### COMANDOS ÚTILES

- Saber qué versiones hay con el comando `list`:
『』[Versiones que hay](https://drive.google.com/file/d/1_YQLNy66u_ZCjkSh9m18cYN4IqL1KQ_Z/view)

- Instalar una versión concreta con el comando `install`:
『』[Versión concreta](https://drive.google.com/file/d/1EhT-yDzr3rbGenykALdDLXYgmUwgR9wC/view)

- Cambiar entre versiones con el comando `use`:
『』[Cambiar entre versiones](https://drive.google.com/file/d/1dOCjJGDGPqnrBKUJVgrOjWB8_zVMBjdX/view)


▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂


## DESARROLLO DEL INFORME CON GITHUB PAGES


Tras finalizar la práctica se nos requiere un informe en con el formato de estilos de Markdown en **GitHub Pages**, para ello me familiaricé e informé tras búsquedas en la página oficial, otros sitios web y visualizaciones de vídeos. Podemos ver la guía de estilos de Markdown en [Markdown guide](https://guides.github.com/features/mastering-markdown/).

Tras saber, por diversas fuentes, cómo elaborar un informe en GitHub Pages llegué a:
Primero para clasificar mejor la parte del informe de la práctica cree una rama nueva llamada **gh_pages** en mi repositorio y un archivo _.md_ denominado **index.md**, también me surgió una duda, que plantearé en el apartado **"CONCLUSIONES"**:
『』[Rama informe gh_pages](https://drive.google.com/file/d/163x2QqzIxu7RmCQzYU5a3cijoz7HLrrS/view)

Con ello tendría el fichero donde elaboraría el informe, pero quiero vincularlo con la herramienta de presentación de GitHub Pages, para ello seguí los siguientes pasos:
1. Ir al apartado _Settings_ esto en el repositorio, y luego en _Options_ llegar hasta casi el final de dicha página, al subapartado _GitHub Pages_.
『』[Settings](https://drive.google.com/file/d/1F1tNIh8Wlz8B28wRuKkbALoN5NbM9NWo/view)
『』[Options](https://drive.google.com/file/d/1Dj_RaJHyn8KT4tpeUUVKQ8fl-obRoeTK/view)

2. **Paso previo** Se debe ejecutar este paso antes, porque si no saltaría un _warning_ debido a la privacidad del repositorio, para ello llegamos al final de la página de _Options_ donde pone _Danger Zone_ y cambiamos la privacidad de **Privada** a **Pública**:
『』[Cambiar visibilidad](https://drive.google.com/file/d/19mlsWJBR7iufx1CspcS89cf30N9qU1Bh/view)

3. Ahora ya con la visibilidad en pública podemos ir al subapartado _GitHub Pages_ antes nombrado y decidir la rama por **gh_pages** donde se encuentra el index.md que contendrá el informe con el que trabajaremos:
『』[GitHub Pages rama](https://drive.google.com/file/d/1Dj_RaJHyn8KT4tpeUUVKQ8fl-obRoeTK/view)

4. Luego en el apartado _Change Theme_ podremos cambiar el tema de fondo con el que se presentará el informe, al aplicar todo, en la parte de arriba se crea un nuevo enlace al informe, dicho enlace se subirá a la tarea dedicada a esta práctica.
『』[Cambiar tema y enlace del informe](https://drive.google.com/file/d/1pZ0Ugz-CtyTPXga6kdyy_MTIGh3hvHaT/view)

Y así finalizamos esta práctica e informe redactado en el archivo **index.md** dentro de la rama **gh_pages**.




▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂

## CONCLUSIONES

Conclusión sobre la práctica e informe, aquí plantearé la dinámica de la práctica y posibles dudas que me hayan surgido y solucionado. La práctica en sí pude hacerla sin dificultades. Sin embargo, a la hora de hacer el informe como nunca antes había usado la herramienta GitHub Pages, tuve que informarme y en varias fuentes me indicaban algo distinto del formato del fichero donde hacer el informe. Esto es debido a que algunos usuarios realizaban los informes o páginas web en formato HTML y muy pocos en formatos .md, pero me di cuenta con la guía de estilos de **Markdown** que muchas herramientas como etiquetas, etc. de HTML eran sustituídas por ejemplo, los tamaños de las cabeceras 

**h1 = #** 
**h2 = ##** etc.

Y aunque muchos trabajasen en HTML y al principio lo intentase con este informe, al final me di cuenta que en .md resulta más legible y conciso, además de ser el formato que aparece en algunas páginas oficiales. Pero de resto, a medida que investigaba conseguía saberme desenvolver algo mejor con la herramienta.


▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂


## BIBLIOGRAFÍA Y/O WEBGRAFÍA
- https://pages.github.com/
- https://github.com/cristinafsanz/github-pages
- https://docs.github.com/en/github/working-with-github-pages
- https://developer.mozilla.org/es/docs/Learn/Using_Github_pages
- https://www.youtube.com/watch?v=QaxgF4v4hms
- https://devcode.la/tutoriales/publicar-tu-web-usando-github-pages/
- https://docs.github.com/es/github/writing-on-github/basic-writing-and-formatting-syntax
- https://parzibyte.me/blog/2019/01/17/agregar-imagenes-github-readme-otras-paginas/
- https://guides.github.com/features/mastering-markdown/
- https://docs.github.com/es/github/working-with-github-pages/setting-up-a-github-pages-site-with-jekyll
