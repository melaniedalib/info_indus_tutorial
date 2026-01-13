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

Voici le fichier xacro : 

.. code-block:: bash
   
   <?xml version="1.0"?> 

   <robot xmlns:xacro="http://www.ros.org/wiki/xacro" name="robot_5_bars"> 

   

   <xacro:property name="mesh_path" value="package://mon_robot_description/meshes/" /> 

      

   <xacro:macro name="default_inertial" params="mass"> 

      <inertial> 

         <origin xyz="0 0 0" rpy="0 0 0"/> 

         <mass value="${mass}" /> 

         <inertia ixx="0.001" ixy="0.0" ixz="0.0" 

                  iyy="0.001" iyz="0.0" 

                  izz="0.001" /> 

      </inertial> 

   </xacro:macro> 

   

   <material name="grey"> 

      <color rgba="0.5 0.5 0.5 1"/> 

   </material> 

   <material name="blue"> 

      <color rgba="0 0 0.8 1"/> 

   </material> 

   <material name="white"> 

      <color rgba="1 1 1 1"/> 

   </material> 

   

   <link name="world"/> 

   

   <joint name="fix_to_world" type="fixed"> 

      <parent link="world"/> 

      <child link="base_link"/> 

   </joint> 

   

   <link name="base_link"> 

      <visual> 

         <origin xyz="0 0 0" rpy="1.57 0 0"/> 

         <geometry> 

         <mesh filename="${mesh_path}base.stl" scale="0.001 0.001 0.001"/> 

         </geometry> 

         <material name="grey"/> 

      </visual> 

      <xacro:default_inertial mass="5.0"/>  

   </link> 

   

   <joint name="left_motor" type="revolute"> 

      <parent link="base_link"/> 

      <child link="link1"/> 

      <origin xyz="-0.08 -0.07 0.032" rpy="0 0 1.57" /> 

      <axis xyz="0 0 1"/> 

      <limit lower="-6.28" upper="6.28" effort="1000.0" velocity="5.0"/> 

      <dynamics damping="0.1" friction="0.1"/> 

   </joint> 

   

   <link name="link1"> 

      <visual> 

         <geometry> 

         <mesh filename="${mesh_path}link1.stl" scale="0.001 0.001 0.001"/> 

         </geometry> 

         <material name="blue"/> 

      </visual> 

      <xacro:default_inertial mass="0.5"/> 

   </link> 

   

   <joint name="left_joint" type="revolute"> 

      <parent link="link1"/> 

      <child link="link2"/> 

      <origin xyz="0.08 0 0.054" rpy="0 0 0"/>  

      <axis xyz="0 0 1"/> 

      <limit lower="-6.28" upper="6.28" effort="1000.0" velocity="5.0"/> 

      <dynamics damping="0.01" friction="0.01"/> 

   </joint> 

   

   <link name="link2"> 

      <visual> 

         <origin xyz="0 0 0" rpy="1.57 0 3.92699081699"/> 

         <geometry> 

            <mesh filename="${mesh_path}link2.stl" scale="0.001 0.001 0.001"/> 

         </geometry> 

         <material name="white"/> 

      </visual> 

      <xacro:default_inertial mass="0.5"/> 

   </link> 

      

   <link name="link2_tip"> 

      <inertial> 

         <mass value="0.001" /> 

         <inertia ixx="0.0001" ixy="0" ixz="0" iyy="0.0001" iyz="0" izz="0.0001" /> 

      </inertial> 

   </link> 

   

   <joint name="link2_to_tip" type="fixed"> 

      <parent link="link2"/> 

      <child link="link2_tip"/> 

      <origin xyz="0.147 0 0" rpy="0 0 0"/> 

   </joint> 

      

   <joint name="right_motor" type="revolute"> 

      <parent link="base_link"/> 

      <child link="link4"/> 

      <origin xyz="0.058 -0.07 0.032" rpy="0 0 1.57"/>  

      <axis xyz="0 0 1"/> 

      <limit lower="-6.28" upper="6.28" effort="1000.0" velocity="5.0"/> 

      <dynamics damping="0.1" friction="0.1"/> 

   </joint> 

   

   <link name="link4"> 

      <visual> 

         <geometry> 

         <mesh filename="${mesh_path}link4.stl" scale="0.001 0.001 0.001"/>  

         </geometry> 

         <material name="blue"/> 

      </visual> 

      <xacro:default_inertial mass="0.5"/> 

   </link> 

   

   <joint name="right_joint" type="revolute"> 

      <parent link="link4"/> 

      <child link="link3"/> 

      <origin xyz="0.079 0 0.053" rpy="0 0 0"/>  

      <axis xyz="0 0 1"/> 

      <limit lower="-6.28" upper="6.28" effort="1000.0" velocity="5.0"/> 

      <dynamics damping="0.01" friction="0.01"/> 

   </joint> 

   

   <link name="link3"> 

      <visual> 

         <origin xyz="0 0 0" rpy="-1.57 0 -3.92699081699"/> 

         <geometry> 

         <mesh filename="${mesh_path}link3.stl" scale="0.001 0.001 0.001"/> 

         </geometry> 

         <material name="white"/> 

      </visual> 

      <xacro:default_inertial mass="0.5"/> 

   </link> 

   

   <ros2_control name="FiveBarBotSystem" type="system"> 

      <hardware> 

         <plugin>gazebo_ros2_control/GazeboSystem</plugin> 

      </hardware> 

      

      <joint name="left_motor"> 

         <command_interface name="position"/> 

         <state_interface name="position"/> 

         <state_interface name="velocity"/> 

      </joint> 

      <joint name="right_motor"> 

         <command_interface name="position"/> 

         <state_interface name="position"/> 

         <state_interface name="velocity"/> 

      </joint> 

   

      <joint name="left_joint"> 

         <state_interface name="position"/> 

         <state_interface name="velocity"/> 

      </joint> 

      <joint name="right_joint"> 

         <state_interface name="position"/> 

         <state_interface name="velocity"/> 

      </joint> 

   </ros2_control> 

   

   <gazebo> 

      <plugin filename="libgazebo_ros2_control.so" name="gazebo_ros2_control"> 

         <parameters>$(find mon_robot_description)/config/my_controllers.yaml</parameters> 

      </plugin> 

   </gazebo> 

   

   <gazebo> 

      <joint name="loop_closure_joint" type="revolute"> 

         <parent>link2_tip</parent> 

         <child>link3</child> 

         <pose>0.11 0 0 0 0 0</pose>  

         <axis> 

         <xyz>0 0 1</xyz> 

         </axis> 

      </joint> 

   </gazebo> 

      

   </robot> 