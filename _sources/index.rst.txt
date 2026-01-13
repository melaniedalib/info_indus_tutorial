.. Dm_info_indus__tutorial documentation master file, created by
   sphinx-quickstart on Wed Sep 17 09:02:51 2025.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Informatique industrielle
=========================

Ce projet a été réalisé par Bonnet Gaëtan, Dalibard Mélanie et Luton Philémon dans le cadre du cours d'informatique industrielle de l’année 2025/2026 en MIQ5.

L'objectif de cette page internet est d'expliquer le fonctionnement de la plateforme robotique « pantographe » avec ROS2 sur une Raspberry Pi (PI5) et de documenter le projet.

Voici une vidéo du pilotage :

.. figure:: ./_static/videos/video_finale2.gif
   :width: 80%
   :align: center

Le projet consiste à :

#. :doc:`Décrire la plateforme mécanique <01_description_des_elements_maquette/description_maquette>`
#. :doc:`Décrire le matériel électronique, la carte Dynamixel avec des liens vers les documentations techniques (datasheets) <01_description_des_elements_maquette/materiel_electronique>`
#. :doc:`Créer la représentation mécanique du pantographe dans un fichier URDF <03_URDF/03_URDF>`
#. :doc:`Visualiser le résultat avec RViz <04_RViz/04_RViz>`
#. :doc:`Décrire la dynamique et donner les équations permettant de piloter la position de l'organe terminal du pantographe <05_resultat_theorique/05_programmation>`
#. :doc:`Pilotage du panthographe <06_ROS2/06_ROS2>`
#. :doc:`Tester la simulation avec Gazebo et RViz <07_Gazebo/07_Gazebo>`

Le rendu attendu est un site web correspondant à un fork du site internet de M. Yguel. Ce site décrira comment nous sommes parvenus à piloter le pantographe réel.

.. toctree::
   :maxdepth: 2
   :caption: Contents:
   
   00_creation_site_web/00_site_web
   01_description_des_elements_maquette/description_maquette
   01_description_des_elements_maquette/materiel_electronique
   03_URDF/03_URDF
   04_RViz/04_RViz
   05_resultat_theorique/05_programmation
   06_ROS2/06_ROS2
   07_Gazebo/07_Gazebo
