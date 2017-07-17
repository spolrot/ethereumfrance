---
ID: 187
post_title: 'Comment miner de l&rsquo;ether (ETH) sous Windows (introduction pour débutant)'
author: Simon Polrot
post_excerpt: ""
layout: post
permalink: >
  https://www.ethereum-france.com/comment-miner-de-lether-eth-windows/
published: true
post_date: 2016-03-05 22:40:13
---
<strong>Ce guide est ancien mais constitue un premier mode d'emploi simple et non-technique pour les personnes souhaitant se lancer dans le minage avec des connaissances informatique très limitées.</strong>

<strong><a href="https://www.ethereum-france.com/tutoriel-complet-pour-miner-sur-la-blockchain-ethereum-mai-2017/">Un tutoriel complet a été préparé par Okkoh</a> qui couvre tous les aspects du minage en détail (optimisation des drivers, version de Windows conseillée, configuration du logiciel de minage, choix du pool, etc.). Si vous souhaitez vous lancer de façon sérieuse dans cette entreprise, rendez-vous plutôt sur ce guide complet pour optimiser votre rendement ! Le tutoriel d'Okkoh a été mis à jour en mai 2017.</strong>

Ceci étant précisé :

Pour miner de l'ether (ETH) en participant à la blockchain ethereum, vous avez besoin :
<ul>
 	<li>D'une adresse sur laquelle envoyer vos ethers (de type 0xD95DC4cf508fDDC10...) que vous pouvez <a href="http://www.ethereum-france.com/creer-et-gerer-son-portefeuille-dether-en-2-minutes-avec-myetherwallet-com/">créer ici</a>.</li>
 	<li>D'un ordinateur doté d'une carte graphique assez puissante (et dotée de minimum 2 Go de RAM) ;</li>
 	<li>De temps.</li>
</ul>
La façon plus "simple" de miner, c'est en participant à travers un "<em>pool</em>" qui permet de mutualiser la puissance de calcul de plusieurs personnes pour miner plus efficacement. Cela permet aussi d'éviter une longue période de synchronisation de la blockchain.

<strong>Etape 1 : télécharger le pack logiciel</strong>

Pour miner en pool, il vous faut un pilote OpenGL pour votre carte graphique (normalement déjà installé sur votre PC) et le programme ethminer.

Pour télécharger le programme ethminer, <a href="https://github.com/Genoil/cpp-ethereum/blob/master/releases/ethminer-0.9.41-genoil-1.1.7.zip">cliquez ici</a>.

Il s'agit d'une archive au format .zip. Il est plus simple de l'extraire  directement à la racine de votre disque dur (par exemple <em>C:\eth\</em>). Si cette dernière phrase est incompréhensible, <a href="http://windows.microsoft.com/fr-fr/windows/compress-uncompress-files-zip-files#1TC=windows-7">suivez ce guide</a> ou posez vos questions en commentaires.

<strong>Etape 2 : exécutez ethminer</strong>

Il faut maintenant exécuter "<em>ethminer</em>" , le logiciel de minage. Pour cela, il vous faut créer un raccourci qui exécutera le logiciel avec les bonnes options.

Rendez-vous dans le dossier dans lequel vous avez extrait les archives et repérez le fichier <em>ethminer.exe, </em>qui peut aussi s'appeler simplement <em>ethminer</em>:

<img class="size-medium wp-image-192 alignnone" src="http://www.ethereum-france.com/wp-content/uploads/2016/02/ethminer-icone-300x13.png" alt="ethminer - icone" width="300" height="13" />

Faites <em>Clic droit &gt; Créer un raccourci.</em>

Un nouveau fichier appelé "<em>ethminer- Raccourci</em>" devrait être apparu dans le dossier. Faites desssus <em>Clic-droit &gt; Propriétés. </em>Vous devriez ouvrir la fenêtre ci-dessous (en français) :

<img class="size-medium wp-image-195 aligncenter" src="http://www.ethereum-france.com/wp-content/uploads/2016/02/ethminer-raccourci-1-217x300.png" alt="ethminer - raccourci" width="217" height="300" />

Il faut modifier l'équivalent de "<em>Target"</em> (cela devrait être "<em>Cible</em>" en français), pour y rajouter :
<blockquote><code>-U -S eth-eu1.nanopool.org:9999 -FS eth-eu2.nanopool.org:9999 -O WALLET_ETHER.UN_NOM</code></blockquote>
En remplaçant :
<ul>
 	<li><code>WALLET_ETHER</code> par votre adresse au format 0xD95DC4cf508fDDC....</li>
 	<li><code>UN_NOM</code> par une chaine de caractère arbitraire qui désignera le PC qui est en train de miner.</li>
</ul>
Il faut ajouter cette chaîne de caractère après l'espace. Le texte complet à entrer dans "<em>Target</em>" est donc :
<blockquote><code>C:\eth\ethminer.exe -U -S eth-eu1.nanopool.org:9999 -FS eth-eu2.nanopool.org:9999 -O WALLET_ETHER.UN_NOM
</code></blockquote>
Validez avec <em>OK</em>.

Il ne reste plus qu'à double-cliquer sur "ethminer - Raccourci" pour lancer le mining. La fenêtre suivante devrait s'afficher :

<img class="size-medium wp-image-196 alignnone" src="http://www.ethereum-france.com/wp-content/uploads/2016/02/ethminer-generating-DAG-300x152.png" alt="ethminer - generating DAG" width="300" height="152" />

La phase "<em>Generating DAG</em>" peut durer un petit peu de temps, soyez patients. Après cette phase, le programme va commencer à miner.

<strong>Étape 3 : Vérifier que le <em>mining</em> fonctionne
</strong>

Pour vérifier que tout fonctionne, direction le site du pool, en <a href="http://eth.nanopool.org/">cliquant ici</a>.

Il vous suffit d'entrer votre adresse dans la case de recherche en haut à droite, puis de cliquer sur "<em>Search</em>" pour voir la progression et l'ether généré. Si vous venez de commencer à miner, la création de votre page peut prendre quelques heures.

Si vous avez un commentaire ou une question, n'hésitez pas à réagir ci-dessous ou <a href="https://cryptofr.com">sur</a><a href="https://cryptofr.com"> l</a><a href="https://cryptofr.com">e</a><a href="https://cryptofr.com"> forum</a>.