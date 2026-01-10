.. Dm_info_indus__tutorial documentation master file, created by
   sphinx-quickstart on Wed Sep 17 09:02:51 2025.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Informatique industrielle 
=====================================

Ce projet a été réalisé par Bonnet Gaëtan, Dalibard Mélanie, et Luton Philémon dans le cadre du cours d'informatique industrielle de 2025/2026 en MIQ5.

L'objectif de cette page internet, est d'expliquer le fonctionnement de la plateforme robotique "pentographe" avec ROS2 sur une Rasperry Pi (PI5) et de documenter le projet.

Voici une image de la maquette :

.. image:: images/real_system_photo.png
   :alt: Photo du système réel
   :width: 400px
   :align: center

Le projet consiste à : 

#. Décrire la plateforme mécanique
#. Décrire le matériel électronique, carte dynamixel avec les liens sur les documentations techniques (datasheets)
#. Créer la rerprésentation mécanique du pantographe dans un fichier URDF
#. Visualiser le résultat avec RVIZ
#. Décrire la dynamique et donner les équations pour piloter la position de l'organe terminal du pentographe: comment 
#. Créer un package ROS2 pour contrôler le pantographe
#. Créer des tests et documenter les tests
#. Créer un code pour dessiner avec le pentographe
#. Tester en réel avec le pantographe
#. Créer un code de simulation pour le pentographe
#. Tester en simulation avec Gazebo et RViz

Le rendu attendu est un site web correspondant à un fork du site internet de M. Yguel. Ce site décrira comment nous sommes parvenu à piloter le pentographe réel.

.. toctree::
   :maxdepth: 2
   :caption: Contents:

