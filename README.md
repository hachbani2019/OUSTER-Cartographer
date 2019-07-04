# Cartographer_ROS & OS1-Ouster

Ce document a pour but d'assister à l'installation de Cartographer_ros et importer les fichiers de configuration nécessaires au bon fonctionnement de cet outil de SLAM avec le Lidar utilisé (Os1-Ouster).

## Installation et construction de Cartographer ROS. 

les outils [wstools](http://wiki.ros.org/wstool) et [rosdep](http://wiki.ros.org/rosdep) sont recommandés pour la construction de Cartographer ROS. On y ajoute [Ninja](https://ninja-build.org/) pour une construction rapide.

```
sudo apt-get update
sudo apt-get install -y python-wstool python-rosdep ninja-build
```

Création d'un nouveau workspace pour Cartographer. 
```
mkdir catkin_ws
cd catkin_ws
wstool init src
wstool merge -t src https://raw.githubusercontent.com/googlecartographer/cartographer_ros/master/cartographer_ros.rosinstall
wstool update -t src
```

Installation des dépendances nécessaires pour Cartographer. <br />
*`sudo rosdep init` renvoyera une erreur si ce n'est pas la première fois que vous exécutez cette commande*

```
src/cartographer/scripts/install_proto3.sh
sudo rosdep init
rosdep update
rosdep install --from-paths src --ignore-src --rosdistro=${ROS_DISTRO} -y
```
Construire et installer

```
catkin_make_isolated --install --use-ninja
```

## Importer les fichiers de configuration.

