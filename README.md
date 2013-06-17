`doyoudatabnf` helps you download [data.bnf.fr](http://data.bnf.fr/)
RDF dumps and load it on a personnal [4store](http://4store.org/)
triple store and SPARQL server. This set of RDF files is a sample of
French national library catalog in RDF. It's [high quality Open
Data](http://data.bnf.fr/semanticweb) [fr].

Prerequesite
============

You need 10 Go on your harddrive, a *nix computer (*BSD, GNU/Linux,
possibly Mac OS X...) with wget and 4store installed. We use also use
git in this tutorial. On Ubuntu you can install it with:

    sudo apt-get install wget 4store git

It seemed 4store defaults it's files location to `/var/lib/4store`,
but Ubuntu doesn't create the directory. Here's a way of creating it,
letting all users access it (same way you can access the `/tmp` dir):

    sudo mkdir /var/lib/4store
    sudo chmod 1777 /var/lib/4store

Import data.bnf.fr RDF files on your desktop
============================================

    git clone git://github.com/nlegrand/doyoudatabnf.git
    cd doyoudatabnf
    ./doyoudatabnf

Launch the 4store triple store backend:

    4s-backend databnf

You may have to wait for something like half an hour for the process
to complete. Once finished, you can test it:

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

Yummy! You can launch a SPARQL server:

    4s-httpd -s -1 -p 8000 databnf

and go to the [HTML sandbox](http://localhost:8000/test/).

About 4store
============

You'll love 4store if you like straightforward application in the *nix
spirit. It seemed to me like the easiest triple store to install and
use.

Start and stop
--------------

When you're done playing with 4store, you can stop the backend this
way:

    pkill -f '^4s-backend databnf$'

To launch it again (or after a computer reboot):

    4s-backend databnf

More on 4store
--------------

You'll find all you need on the [officiel web
site](http://4store.org/).
