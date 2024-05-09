# Añadir similar a antivirus.

Estos programas nos sirven para detectar posibles ataques y/o virus, también nos permiten analizar los archivos antes de realizar alguna accion con ellos.

# ####
### Nota
Esto solo es para añadir capas de seguridad a nuestro sistema.
# ###

## CamAV y ClamTK
### Instalación.
- sudo apt install clamav clamav-daemon clamtk
#### El clamtk es una interfaz para escanear archivos, carpetas, entre otros antes de realizar alguna acción con ellos.

## Rootkit
### Instalación.
- sudo apt install rkhunter
### Actualización.
- sudo apt install rkhunter
### Escanea en busqueda de algún virus.
- sudo rkhunter --check
### ver reporte
- sudo nano /var/log/rkhunter.log

#
## Existen más herramientas que se pueden agregar como una capa más de seguridad.