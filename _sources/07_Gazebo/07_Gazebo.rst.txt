Limites de l’URDF et modélisation pour la simulation
====================================================

Impossibilité des boucles fermées en URDF
-----------------------------------------

Il n’est pas possible de réaliser une boucle cinématique fermée dans une description
URDF standard.  
Pour cette raison, les deux bras du pantographe ont été décrits indépendamment, puis
reliés ultérieurement lors de la phase de simulation.

Un programme a été développé afin de visualiser le fichier URDF dans **RViz**.
Cependant, nous ne sommes pas parvenus à relier correctement les bras 2 et 3 entre eux
dans ce cadre.

Spécificités pour la simulation (Gazebo / RViz)
-----------------------------------------------

Le format URDF étant limité aux structures arborescentes (chaînes en série), il ne
supporte pas nativement les boucles cinématiques fermées.  
Pour contourner cette limitation, nous avons exploité les balises spécifiques au format
**SDF** (``<gazebo>``) afin d’injecter une contrainte physique de fermeture de boucle.

Les étapes suivantes ont été mises en œuvre :

- **Création d’un lien virtuel (*Dummy Link*)**  
  Un segment intermédiaire, nommé ``link2_tip``, a été ajouté afin de matérialiser
  précisément le point de connexion géométrique entre les deux chaînes cinématiques.

- **Injection de la contrainte**  
  Une liaison virtuelle (de type *revolute* ou *universal*) a été définie dans le fichier
  Xacro afin de forcer le moteur physique à maintenir les deux extrémités solidaires.

Limites et instabilités observées
---------------------------------

Malheureusement, cette modélisation a provoqué une instabilité numérique critique
(divergence du solveur), se traduisant par des valeurs d’efforts indéfinies (*NaN*) dans
les retours d’état du robot.

Cette erreur persiste malgré plusieurs tentatives de correction, notamment :

- la désactivation des auto-collisions (``self_collide``) ;
- l’intégration de gains PID pour le contrôle des articulations.

L’hypothèse principale est l’existence d’un conflit entre les contraintes rigides imposées
par la boucle fermée et les matrices d’inertie des différentes pièces, rendant la
résolution physique du système impossible dans l’état actuel.
