# Guia Ubuntu 20.04 LTS.

# ####
### Nota
- Esta guia empieza después de haber instalado ubutnu 20.04.
- Después de cada comando, ejecutar el comando: <code style='font-family: "courier new"'>sudo apt update</code>.
# ###

## Actualizar Ubuntu despues de instalar.
- sudo apt update 
- sudo apt upgrade 
- sudo apt update

## ocultar iconos del dock de dispositivos montados
- gsettings set org.gnome.shell.extensions.dash-to-dock show-mounts false

## Buscar archivos dentro de paquetes.
- sudo apt install apt-file
- sudo apt update
- sudo apt-file update

## codecs de audio y video
- sudo apt install ubuntu-restricted-extras
- sudo apt install libavcodec-extra
- sudo apt install gstreamer1.0-libav gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-pulseaudio totem-plugins libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev

## GStreamer
- sudo apt install libgstreamer1.0-0 gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav gstreamer1.0-doc gstreamer1.0-tools gstreamer1.0-x gstreamer1.0-alsa gstreamer1.0-gl gstreamer1.0-gtk3 gstreamer1.0-qt5 gstreamer1.0-pulseaudio

## Configuración 
- pkg-config --cflags --libs gstreamer-1.0

## Retoques
- sudo apt install gnome-tweak-tool

## Gnome shell
- sudo apt install chrome-gnome-shell
### Agregar desde el navegador Firefox.
- https://extensions.gnome.org/

## Firewall.
### Solo instalar en caso de necesidad.
- sudo ufw enable
### Interfaz del firewall
- sudo apt install gufw

## Limpiar dependencias no utilizadas o descontinuadas, solo en caso de necesidad.
- sudo apt-get autoclean
- sudo apt-get clean
- sudo apt-get autoremove

## QT5
- sudo apt install qt5-default qtcreator qtwebengine5-dev

## OpenJDK.
- sudo apt install default-jdk
- sudo apt install openjdk-8-jdk

## pip3
- sudo apt install python3-pip
- pip3 install --upgrade pip

# ####
### Nota
Desde este punto se debe instalar las dependencias para la <code>GPU</code>, en mi caso, solo tengo <code>NVIDIA</code>, por lo que no puedo proporcionar pasos para otras <code>GPU</code>.
# ###

## Nvidia.
- sudo add-apt-repository ppa:graphics-drivers/ppa
## Muestra los driver posibles a instalar, seleccionar el recomendado.
- ubuntu-drivers devices
###### En este punto recomiendo ir a la aplicación <code>Software y actualizaciones</code>, luego a la pestaña <code>Más controladores</code> y seleccionar el driver privativo de la <code>GPU</code>, no seleccionar la ultima versión disponible, tampoco server ni probado ó abierto, por lo general dan problemas.

- <span style='color: #76ff3a'>***NVIDIA driver metapackage desde nvidia-driver-535(privativo)***</span>
- <span style='color: #ff0000'>***NVIDIA driver metapackage desde nvidia-driver-535(privativo, probado)***</span>
- <span style='color: #ff0000'>***NVIDIA driver metapackage desde nvidia-driver-535-server(privativo)***</span>

## En este punto se necesita reiniciar.

# ####
### Nota
Antes de iniciar el siguiente paso, necesitan descargar los siguientes archivos y dejarlos en la carpeta personal con los nombres de la lista.
- [Vulkan](https://vulkan.lunarg.com/sdk/home)
- [cmake](https://cmake.org/download/)
- [SDL](https://github.com/libsdl-org/SDL/releases/tag/release-2.30.3)
- [AntTweakBar](https://anttweakbar.sourceforge.io/doc/tools_anttweakbar_download.html)

### Las versiones que uso son.
- <code>Vulkan 1.1.130.0</code>
- <code>cmake 3.15.6</code>
- <code>SDL2 2.0.10</code>
- <code>AntTweakBar 116</code>
# ###

## SDK Vulkan.
En este punto, primero deben rebisar las dependiencias, si son las mismas ó deben modificar algunos campos del comando.
- [Docs](https://vulkan.lunarg.com/doc/sdk/latest/linux/getting_started.html)
- sudo apt-get install libglm-dev cmake libxcb-dri3-0 libxcb-present0 libpciaccess0 libpng-dev libxcb-keysyms1-dev libxcb-dri3-dev libx11-dev g++ gcc g++-multilib libmirclient-dev libwayland-dev libxrandr-dev libxcb-ewmh-dev git libpython3.6 bison

## CMake
- ./bootstrap
- make
- sudo make install
- sudo apt install cmake-qt-gui

## vulkan environment
- export VULKAN_SDK=~/vulkan/1.1.130.0/x86_64
- export PATH=$VULKAN_SDK/bin:$PATH
- export LD_LIBRARY_PATH=$VULKAN_SDK/lib${LD_LIBRARY_PATH:+:$LD_LIBRARY_PATH}
- export VK_LAYER_PATH=$VULKAN_SDK/etc/vulkan/explicit_layer.d

## Vulkan Header Files
- sudo cp -r $VULKAN_SDK/include/vulkan/ /usr/local/include/

## Vulkan Loader Files
- sudo cp -P $VULKAN_SDK/lib/libvulkan.so* /usr/local/lib/
	
## Vulkan Layer Files
- sudo cp $VULKAN_SDK/lib/libVkLayer_*.so /usr/local/lib/
- sudo mkdir -p /usr/local/share/vulkan/explicit_layer.d
- sudo cp $VULKAN_SDK/etc/vulkan/explicit_layer.d/VkLayer_*.json /usr/local/share/vulkan/explicit_layer.d

## Dependencias de AntTweakBar.

### GLUT
- sudo apt-get install mesa-utils
- sudo apt-get install freeglut3 freeglut3-dev


### dependencias de SDL2
- sudo apt-get install libsdl2-2.0 libsdl2-dev
- sudo apt install libjpeg-dev libwebp-dev libtiff5-dev libsdl2-image-dev libsdl2-image-2.0-0
- sudo apt install libmikmod-dev libfishsound1-dev libsmpeg-dev liboggz2-dev libflac-dev libfluidsynth-dev libsdl2-mixer-dev libsdl2-mixer-2.0-0
- sudo apt install libfreetype6-dev libsdl2-ttf-dev libsdl2-ttf-2.0-0
- sudo apt-get install libsamplerate-dev

## Configuración de las dependencias del SDL2
- sdl2-config --cflags --libs -lSDL2 -lSDL2_mixer -lSDL2_image -lSDL2_ttf

## SDL2
- cd SDL
- mkdir build
- cd build
- ../configure
- make
- sudo make install

## GLFW
- sudo apt-get install libglfw3 libglfw3-dev

## SFML
- sudo apt-get install libsfml-dev

## AntTweakBar
- cd AntTweakBar/src
- make

#
#
# Con esto nos aseguramos de tener todo lo basico para el día a día.