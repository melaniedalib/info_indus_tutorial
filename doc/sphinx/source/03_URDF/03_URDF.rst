Gestion de la Géométrie et Importation des Meshes
=================================================

.. contents::
   :local:
   :depth: 2

1. Importation de la géométrie du robot
---------------------------------------

La première étape de la description URDF a consisté à importer la géométrie du robot.  
Bien que la modélisation 3D initiale du pantographe soit disponible aux formats **STP** et **DAE**, des contraintes techniques ont imposé une conversion.

**Problématique :**  
Les fichiers DAE présentaient des erreurs d'orientation d'axes lors de l'importation.

**Solution :**  
Utilisation du logiciel *Creo Parametric* pour générer des fichiers **STL** à partir des fichiers sources STP.  
Cette méthode a permis de définir manuellement et précisément l'origine et l'orientation des axes de chaque pièce avant l'exportation, garantissant une compatibilité parfaite avec le format URDF.


2. Structure du Package ROS 2
-----------------------------

Pour organiser le projet, un package nommé **mon_robot_description** a été créé avec l'arborescence standardisée suivante :  

- **/meshes** : Contient l'ensemble des fichiers STL exportés.  
- **/urdf** : Contient le fichier de description principal au format Xacro.  
- **/launch** : Regroupe les scripts Python permettant de lancer la visualisation sur RViz2.  


3. Développement du Modèle Xacro
--------------------------------

Le choix du format **Xacro (XML Macros)** a été privilégié par rapport à l'URDF classique pour ses avantages en termes de flexibilité :  

- **Paramétrage :** Définition de constantes (dimensions, masses, offsets) en début de fichier.  
- **Modularité :** Réutilisation des constantes comme paramètres pour plusieurs liens (*links*), notamment pour les propriétés d'inertie des bras, évitant ainsi les répétitions et les erreurs de saisie.  


4. Configuration des Liens et Articulations
-------------------------------------------

L'intégration dans le fichier Xacro a nécessité une attention particulière sur :  

- La position exacte des repères de chaque lien.  
- L'orientation des axes de rotation des articulations (*joints*).  
- La cohérence globale de la chaîne cinématique.  

.. note::
   Remarque : il n’est pas possible de réaliser une boucle fermée dans une description URDF.  
   Nous avons donc décrit les deux bras indépendamment afin de les relier ensuite lors de la simulation.

