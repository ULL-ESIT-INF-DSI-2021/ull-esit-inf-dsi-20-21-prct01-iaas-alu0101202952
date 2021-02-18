


# Informe Práctica 1: Configuración de máquina virtual en el IaaS


![Image](https://www.ull.es/servicios/stic/wp-content/uploads/sites/2/2016/05/VDI-1.png)



╔═══════════════════════════════════════════════════════════════════╗

> - Autora: Andrea Calero Caro
> - Alu: [alu0101202952@ull.edu.es](alu0101202952@ull.edu.es)
> - Práctica: 1 Configuración de máquina virtual en el IaaS
> - Asignatura: Desarrollo de Sistemas Informáticos
> - Universidad de La Laguna

╚═══════════════════════════════════════════════════════════════════╝



▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂


## Índice
  - Objetivos
  - Pasos previos
  - Configuración máquina IaaS
  - Instalación de git y node.js
  - Desarrollo del informe con GitHub Pages
  - Conclusiones
  - Bibliografía
  
  

▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂


## OBJETIVOS
Los objetivos en esta práctica serán la configuración de la máquina virtual IaaS de la ULL, además de la instalación y configuración de todas las herramientas necesarias para comenzar a trabajar en la asignatura, como es git y node.js. Todo ello junto con la presentación de este informe y el desarrollo del mismo en GitHub Pages.



▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂


## PASOS PREVIOS

Antes de comenzar se nos requiere una serie de pasos previos para introducirnos en la asignatura.

1. Cumplimentar la encuesta de elección de grupo de trabajo, en mi caso estaría en el **"Grupo J"** de trabajo.

2. Cumplimentar la encuesta sobre expectativas y conocimientos previos, la cual ya he realizado.

3. Darse de alta en el aula Google Classroom de la asignatura. Para ello seleccionamos nuestro correo institucional y seleccionamos que somos **alumnos**.

4. Como ya poseía una cuenta GitHub asociada a mi correo institucional (alu0101202952@ull.edu.es), solicité los beneficios de GitHub Education y acepté la asignación del GitHub Classroom asociada a esta práctica. En caso contrario, debería de haberme creado dicha cuenta en la comunidad y realizar los pasos anteriores.

5. Como para el desarrollo de esta práctica y su respectivo informe necesito conocimientos en **GitHub Pages**, **Markdown** y **Jekyll**. Mediante diversas búsquedas en páginas web, las cuales muestro en el apartado bibliografía de este informe, conseguí realizar el susudicho con el estilo que se me requiere.


▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂▂


## CONFIGURACIÓN MÁQUINA IAAS

Lo primero para poder acceder al servicio de máquinas virtuales del IaaS es configurar la VPN, en mi caso ya la tengo configurada gracias a la aplicación de **GlobalProtect**, a la cual accedo a la VPN de la ULL introduciendo en el usuario `aluxxxxxxxxxx` y en la contraseña `contraseña_institucional`. Y así nos conectaríamos.

Una vez dentro del servicio https://iaas.ull.es/ovirt-engine/, tras meterme con mi alu y contraseña, enciendo mi máquina virtual asignada en la asignatura de Desarrollo de Sistemas Informáticos (DSI) con un identificador, en mi caso es **DSI-31**. Cuando la enciendo, desde mi subsistema Linux Ubuntu 18.04 LTS me conecto a ella mediante el commando:

> `ssh usuario@10.6.XXX.XXX` 
Esto con la IP de mi máquina virtual

Lo primero que se me pide es cambiar la contraseña actual (usuario) por una mía que pueda recordar. Tras ellos comenzaría a configurar el fichero **hostname** con el nombre de mi host en la máquina, esto será necesario para poder acceder a la máquina desde local mediante el host asignado:

iaas-dsi31

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
< `sudo vi /etc/hosts`

Y añadir la ip y el host de nuestra máquina, en mi caso pondría:
...
> `10.6.XXX.XXX     iaas-dsi31`

Una vez que tenemos el host necesitaré configurar la llave pública-privada, con el comando:
> `cat .ssh/id_rsa.pub`

Nos mostrará la llave:
https://github.com/ULL-ESIT-INF-DSI-2021/ull-esit-inf-dsi-20-21-prct01-iaas-alu0101202952/blob/doc/llave_pub.jpg

