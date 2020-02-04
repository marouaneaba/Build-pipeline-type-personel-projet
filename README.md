# Java-Build

### Build CI    
Une build CI (continuous intégration) à pour objectif de publier la version de l'application sur le nexus si un nouveau tag existe sur la branch qui est utilisé par la build, et pour créér un artifact, qui n'est ni plus ni moins qu'une archive zip contenant les fichiers nécéssaire au lancement de l'application en mode production. 

1.La tache "mvn clean package" effacer tous les éléments générés lors des exécutions précédentes, compile le code source du projet avec exécution des tests, et enfin génère l'artéfact.<br/>
2.La tache "Copy files to" copie l'exécutable (jar, war, ear) ainsi que les fichiers de configuration dans le répertoire d'artéfact.<br/>
3.La tache "Publish Artifact" récupère le dossier d'artifact (contenant l'exécutable de l'application et les fichiers de configuration) et le publie dans Azure Pipeline.

# Génération de la documentation pickles

1.La tache "Pickles Documentation Generator" génére la documentation à partir des tests Gherkin de l'application.
2.La tache "Publish Artifact" récupère les fichiers pickels généré précédemment et les publies dans Azure Pipeline


### Build PR 
La build de PR (pull request), doit être lancée automatiquement dès qu'une pull request est créée sur les branches develop et master. Elle permet de lancer tous les tests du projet, de vérifier que la couverture de test n'est pas passé en dessous du seuil défini (généralement à 80% minimum sur le coverage statements)

1.La tache "mvn clean package" effacer tous les éléments générés lors des exécutions précédentes, compile le code source du projet avec exécution des tests, et enfin génère l'artéfact.<br/>
2.La tache "Task group: SonarQube6_7 for JAVA" est un ensemble de taches permettant de générer et publier le rapport sonar.<br/>




Configurer le lancement d'une build PR pour les pull request sur develop (à faire aussi sur la branche master) :



### Build SEC
La build SEC (pour securité), permet de générer chaque jour les rapport Checkmarx (analyse de sécurité static du code) et LifeCycle (analyse de sécurité sur les dépendances du projet.

1.La tache "Security static source code analysis" génére le rapport Checkmarx et le publie.<br/>
2.La tache "mvn clean package" effacer tous les éléments générés lors des exécutions précédentes, compile le code source du projet avec exécution des tests, et enfin génère l'artéfact.<br/>
3.La tache "Nexus LifeCycle analysis" génère le rapport LifeCycle et le publie.<br/>


PS: Il est nécessaire de télécharger les dépendances du projet avec mvn package avant de lance l'analyse LifeCycle
