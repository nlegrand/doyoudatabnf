`doyoudatabnf` vous aide à télécharger les dumps RDF de [Data
BnF](http://data.bnf.fr/) pour les importer dans votre triple store et
serveur SPARQL personnel. Nous utilisons ici le logiciel
[4store](http://4store.org/). Data BnF est un échantillon du catalogue
de la Bibliothèque nationale de France, en RDF. Ce sont des données de
[très belle qualité](http://data.bnf.fr/semanticweb).

Prérequis
=========

Vous avez besoin de 10 Go sur votre disque dur, un système *nix
(GNU/Linux, peut-être Mac OS X) avec wget et 4store d'installé. Nous
utilisons aussi git dans ce tutoriel. Sur Ubuntu, vous pouvez les
installer avec :

    sudo apt-get install wget 4store git

Il semblerait que par défaut, l'emplacement des fichiers de 4store se
trouve sous `/var/lib/4store`, mais Ubuntu ne crée pas le
répertoire. Voici une manière de le faire, permettant à tous les
utilisateurs d'y accéder (de la même manière que tout le monde accède
à `/tmp`).

    sudo mkdir /var/lib/4store
    sudo chmod 1777 /var/lib/4store

Installez Data BnF sur votre machine personnel
==============================================

    $ git clone git://github.com/nlegrand/doyoudatabnf.git
    $ cd doyoudatabnf
    $ ./doyoudatabnf

Vous pouvez avoir à attendre plus d'une demi-heure pour que l'import
se fasse. Une fois terminé, vous pouvez le tester :

    $ 4s-query -s -1 -f text -P databnf <sparql/totaltypes.sparql 
    ?type	?total
    <http://rdvocab.info/uri/schema/FRBRentitiesRDA/Manifestation>	1497296
    <http://data.bnf.fr/ontology/Anl>	224290
    <http://rdvocab.info/uri/schema/FRBRentitiesRDA/Expression>	1497296
    <http://xmlns.com/foaf/0.1/Organization>	6517
    <http://xmlns.com/foaf/0.1/Person>	13527
    <http://www.w3.org/2004/02/skos/core#Concept>	251033
    <http://rdvocab.info/uri/schema/FRBRentitiesRDA/Work>	63116
    #EOR

Miam ! Vous pouvez lancer le serveur SPARQL :

    4s-httpd -s -1 -p 8000 databnf

Et jouer dans le [bac à sable](http://localhost:8000/test/) HTML.

À propos de 4store
==================

Vous adorerez 4store si vous aimez les applications simples dans
l'esprit *nix. Il m'a semblé être le triple store le plus simple à
installer et utiliser.

Démarrage et arrêt
------------------

Une fois que vous avez fini de jouer avec 4store, vous pouvez arrêter
le backend de cette manière :

    pkill -f '^4s-backend databnf$'

Pour le relancer (ou après un redémarrage de votre ordinateur) :

    4s-backend databnf

En savoir plus sur 4store
-------------------------

Vous trouverez tout ce dont vous avez besoin sur le [site web
officiel](http://4store.org/) du projet.
