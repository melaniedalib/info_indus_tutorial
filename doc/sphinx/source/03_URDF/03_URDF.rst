Modèle URDF du pantographe
==========================

.. contents::
   :local:
   :depth: 2

Introduction
------------

Cette partie décrit la réalisation de la description URDF du pantographe.  
L’objectif est de modéliser correctement la structure mécanique du robot afin de
permettre sa visualisation et sa simulation dans ROS2.

Plan
----

#. Importer les fichiers
#. Créer un fichier Xacro
#. Remplir et orienter correctement le fichier Xacro

Importer les fichiers
---------------------

Afin de réaliser la description URDF du robot, il est nécessaire d’importer sa géométrie
sous forme de *mesh* dans le fichier URDF.

La modélisation 3D du pantographe est disponible sous les formats **STP** et **DAE**.
Cependant, le format URDF n’accepte que les fichiers **DAE**.  
Un problème a été rencontré : les axes des fichiers DAE étaient mal orientés.

Pour résoudre ce problème, des fichiers **STL** ont été générés à partir des fichiers
STP à l’aide du logiciel *Creo Parametric*.  
Cette étape a permis de choisir correctement l’orientation des axes avant l’export
vers un format compatible avec l’URDF.

Créer un fichier URDF (Xacro)
-----------------------------

Pour décrire le robot, un fichier **Xacro** est utilisé à la place d’un fichier URDF
classique.

L’utilisation de Xacro permet de :
- définir des constantes en début de fichier ;
- réutiliser ces constantes comme paramètres ;
- simplifier la description du robot.

Par exemple, les propriétés d’inertie des bras peuvent être définies une seule fois
et réutilisées pour plusieurs liens.

Remplir et orienter correctement le fichier Xacro
--------------------------------------------------

Chaque lien et chaque articulation du pantographe est défini en respectant :
- la position des repères ;
- l’orientation correcte des axes ;
- la cohérence entre les éléments mécaniques.

Simulation
----------

Pour la simulation, un **dummy link** est utilisé afin de connecter *link3* à l’extrémité
de *link2* et non à l’origine de son repère.

Cette approche permet de :
- respecter la géométrie réelle du robot ;
- garantir une simulation correcte dans RViz et Gazebo.
