Création du site web
===================

.. note::

   Cette partie s’inspire de la documentation fournie par **M. Yguel**
   dans le cadre du cours d’informatique industrielle. voir ici pour la documentation exacte.
   

Introduction
------------

Nous avons créé ce site web afin de documenter le projet de pantographe
et de présenter les différentes étapes de conception, de simulation
et de contrôle sous ROS 2.

Le site est basé sur **Sphinx** et hébergé via **GitHub Pages**.

---

Création du projet
------------------

Nous avons ouvert un terminal sous Ubuntu à l’aide du raccourci :

- ``Ctrl + Alt + T``

Nous avons ensuite créé le répertoire du projet dans notre dossier personnel :

.. code-block:: bash

   mkdir -p ~/info_indus/info_indus_tutorial

Nous avons nommé ce projet ``info_indus_tutorial``.

Puis, nous nous sommes placés dans le répertoire du projet :

.. code-block:: bash

   cd ~/info_indus/info_indus_tutorial

---

Configuration de VS Code
------------------------

Nous avons utilisé **Visual Studio Code** comme éditeur de code.

Création des fichiers de configuration
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Nous avons créé un dossier ``.vscode`` à la racine du projet, ainsi qu’un fichier
``settings.json`` vide :

.. code-block:: bash

   mkdir .vscode
   touch .vscode/settings.json

Nous avons également créé un fichier ``keybindings.json`` dans le dossier de
configuration utilisateur de VS Code :

.. code-block:: bash

   cd ~/.config/Code/User
   touch keybindings.json

---

Ouverture du projet dans VS Code
--------------------------------

Nous avons ouvert le projet dans VS Code avec la commande :

.. code-block:: bash

   code .

Nous avons ensuite complété le fichier ``settings.json`` afin d’améliorer
le formatage automatique et le confort d’édition.

.. literalinclude:: resources/code/config.vscode/settings.json
   :language: json
   :caption: Configuration VS Code (settings.json)

---

Configuration des raccourcis clavier
------------------------------------

Nous avons modifié les raccourcis clavier afin d’éviter certaines erreurs
de manipulation et de corriger un bug lié à l’extension Sphinx.

.. literalinclude:: resources/code/config.vscode/keybindings.json
   :language: json
   :caption: Configuration des raccourcis clavier

Après modification, nous avons rechargé VS Code via :

- ``Ctrl + Shift + P``
- ``Developer: Reload Window``

---

Installation des extensions VS Code
-----------------------------------

Nous avons installé plusieurs extensions afin de faciliter le développement,
la documentation et l’utilisation de ROS 2.

Édition de code
^^^^^^^^^^^^^^^
- **Gremlins Tracker**  
  Permet de visualiser les caractères invisibles.

Git
^^^
- **Git Graph**  
  Permet de visualiser l’historique Git.

Python
^^^^^^
- **Python**
- **Python Debugger**

Documentation
^^^^^^^^^^^^^
- **Esbonio**  
  Permet l’édition et l’aperçu des fichiers Sphinx.

ROS 2
^^^^^
- **ROS 2**
- **ROS 2 Ament Task Provider**
- **Uncrustify**

Assistant IA
^^^^^^^^^^^^
- **GitHub Copilot**

Ces extensions nous ont permis d’améliorer la productivité
et la qualité du code et de la documentation.
