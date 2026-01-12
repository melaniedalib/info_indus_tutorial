Création du site web
====================

Création du projet
^^^^^^^^^^^^^^^^^^
.. note::
   Cette partie s’inspire de la documentation fournie par **M. Yguel**
   dans le cadre du cours d’informatique industrielle. `à cette adresse <https://yguel.github.io/informatique_industrielle_avec_ROS2/c01_create_and_publish_doc/p01s02_create_and_publish_doc.html>`_.

Introduction
------------
Nous avons créé ce site web afin de documenter le projet de pantographe et de présenter les étapes de conception, de simulation et de contrôle sous ROS 2. Le site repose sur **Sphinx** et est hébergé via **GitHub Pages**.

Création du dossier
-------------------
Nous avons ouvert un terminal sous Ubuntu avec le raccourci ``Ctrl + Alt + T`` puis créé le répertoire du projet :

.. code-block:: bash

   mkdir -p ~/info_indus/info_indus_tutorial

Nous avons nommé le projet ``info_indus_tutorial`` puis nous nous sommes placés dans ce répertoire :

.. code-block:: bash

   cd ~/info_indus/info_indus_tutorial

Configuration de VS Code
------------------------
Nous avons utilisé **Visual Studio Code** comme éditeur principal.

Création des fichiers de configuration
--------------------------------------
Nous avons créé le dossier ``.vscode`` et le fichier ``settings.json`` :

.. code-block:: bash

   mkdir .vscode
   touch .vscode/settings.json

Nous avons également créé le fichier ``keybindings.json`` dans le dossier utilisateur de VS Code :

.. code-block:: bash

   cd ~/.config/Code/User
   touch keybindings.json

Ouverture du projet
-------------------
Nous avons ouvert le projet dans VS Code :

.. code-block:: bash

   code .

Nous avons complété le fichier ``settings.json`` afin d’améliorer le formatage et le confort d’édition.

.. code-block:: bash

   {
    "editor.formatOnSave": true,
    "editor.detectIndentation": true,
    "editor.formatOnPaste": true,
    "editor.wordWrap": "on",
    "C_Cpp.clang_format_sortIncludes": false,
    "python.formatting.autopep8Args": [
        "--ignore",
        "E402"
    ],
    "terminal.integrated.scrollback": 100000,
    "workbench.editor.enablePreview": false,
    "[restructuredtext]": {
        "editor.tabSize": 3
    },
   }

Configuration des raccourcis clavier
------------------------------------
Nous avons modifié les raccourcis clavier afin d’éviter des erreurs de manipulation et de corriger un problème lié à l’extension Sphinx.

.. code-block:: bash

   [
    {
        "key": "ctrl+q",
        "command": "-workbench.action.quit"
    },
    {
        "key": "enter",
        "command": "-restructuredtext.editor.listEditing"
      }
   ]  

Nous avons ensuite rechargé VS Code via ``Ctrl + Shift + P`` puis ``Developer: Reload Window``.

Installation des extensions
^^^^^^^^^^^^^^^^^^^^^^^^^^^
Nous avons installé les extensions nécessaires au développement, à la documentation et à ROS 2 : Gremlins Tracker, Git Graph, Python, Python Debugger, Esbonio, ROS 2, ROS 2 Ament Task Provider, Uncrustify et GitHub Copilot. Ces extensions ont amélioré la productivité et la qualité de la documentation.

Introduction au versionnement avec Git
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Nous avons utilisé **Git** afin de suivre l’évolution du projet et conserver un historique clair des modifications.

Initialisation du dépôt
-----------------------
Nous nous sommes placés à la racine du projet et avons initialisé le dépôt Git :

.. code-block:: bash

   cd ~/info_indus/info_indus_tutorial
   git init

Cette commande a créé le répertoire caché ``.git`` contenant l’historique du projet.

Vérification de l’état du dépôt
-------------------------------
Nous avons vérifié l’état du dépôt avec :

.. code-block:: bash

   git status

Le dossier ``.vscode`` apparaissait comme non suivi.

Ajout des fichiers
------------------
Nous avons ajouté le dossier ``.vscode`` au suivi Git :

.. code-block:: bash

   git add .vscode
   git status

Création du premier commit
--------------------------
Nous avons créé un premier commit :

.. code-block:: bash

   git commit -m "First commit"

Git a demandé une configuration utilisateur :

.. code-block:: bash

   git config user.email "prenom.nom@insa-strasbourg.fr"
   git config user.name "Prénom NOM"

.. note::
   Nous n’avons pas renseigné nos informations personnelles dans le rapport et n’avons pas utilisé l’option ``--global``.

Nous avons ensuite relancé la commande de commit :

.. code-block:: bash

   git commit -m "First commit"

Consultation de l’historique
----------------------------
Nous avons consulté l’historique des commits avec :

.. code-block:: bash

   git log

Création d’une première documentation Sphinx
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Installation de Sphinx
----------------------
Nous avons installé Sphinx :

.. code-block:: bash

   sudo apt-get update
   sudo apt-get install -f python3-sphinx

Nous avons créé le répertoire de documentation :

.. code-block:: bash

   mkdir -p doc/sphinx

Nous avons créé le fichier ``requirements.txt`` :

.. code-block:: bash

   touch ~/info_indus/info_indus_tutorial/doc/sphinx/requirements.txt

Nous avons ajouté les dépendances puis installé l’environnement virtuel :

.. code-block:: bash

   cd ~/info_indus/info_indus_tutorial/doc/sphinx
   python3 -m venv .venv
   source .venv/bin/activate
   pip install -r requirements.txt

Configuration de Sphinx
-----------------------
Nous avons initialisé la documentation avec :

.. code-block:: bash

   cd ~/info_indus/info_indus_tutorial/doc
   sphinx-quickstart sphinx

Nous avons conservé une séparation claire entre les sources et le build afin de ne versionner que les fichiers utiles.

Création de la documentation
----------------------------
Nous avons généré la documentation HTML :

.. code-block:: bash

   cd ~/info_indus/info_indus_tutorial/doc/sphinx
   make html

La documentation est accessible via le fichier ``index.html`` :

.. code-block:: bash

   firefox ~/info_indus/info_indus_tutorial/doc/sphinx/build/html/index.html

Sauvegarde avec Git
-------------------
Nous avons ajouté la documentation au dépôt Git et effectué un commit :

.. code-block:: bash

   git add source
   git add Makefile make.bat requirements.txt
   git commit -m "First commit of the documentation"

Publication sur GitHub
^^^^^^^^^^^^^^^^^^^^^^
Nous avons créé un dépôt GitHub public et configuré une clé SSH afin de pouvoir pousser le projet. Nous avons ensuite ajouté le dépôt distant, renommé la branche principale en ``rolling`` et poussé le code sur GitHub.

Nous avons mis en place une **GitHub Action** permettant de générer et publier automatiquement la documentation à chaque modification. La documentation est ainsi mise à jour en temps réel via GitHub Pages.
