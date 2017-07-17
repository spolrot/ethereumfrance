---
ID: 657
post_title: 'Interview de Vitalik Buterin, créateur d&rsquo;Ethereum et Président de la Fondation (partie 2 sur 2)'
author: Simon Polrot
post_excerpt: ""
layout: post
permalink: >
  https://www.ethereum-france.com/interview-de-vitalik-buterin-createur-dethereum-et-president-de-la-fondation-partie-2-sur-2/
published: true
post_date: 2016-05-19 17:12:45
---
[caption id="attachment_581" align="alignright" width="300"]<img class="wp-image-581 size-medium" src="https://www.ethereum-france.com/wp-content/uploads/2016/05/Vitalik-Buterin-300x169.jpg" alt="Vitalik Buterin" width="300" height="169" /> Vitalik Buterin, créateur d'Ethereum[/caption]
<p id="magicdomid2" class="ace-line gutter-author-p-593706 emptyGutter" data-author-initials="SP" data-author-name="Simon P" data-author-link="/ep/profile/FHxhJ7Ui9KD"><strong>Deuxième partie de l'interview de Vitalik Buterin réalisée par <span class="author-p-593706 i">Quentin de Beauchesne, les membres de la communauté CryptoFR et moi-même. <a href="https://www.ethereum-france.com/interview-de-vitalik-buterin-createur-dethereum-et-president-de-la-fondation-partie-1-sur-2/"><span style="text-decoration: underline;">La première partie est disponible ici</span></a>. Cette seconde partie aborde des questions plus techniques telles que le Proof of Stake, le sharding ou Casper.</span></strong></p>
<p class="ace-line longKeep gutter-noauthor"><em><span class="author-p-593706 i">Les questions posées par les membres sont attribuées à leurs auteurs entre parenthèses, les questions non attribuées étant posées par Quentin ou moi-même. Les réponses ont été légèrement reformulées pour en faciliter la lecture.</span></em></p>
<p class="ace-line longKeep gutter-noauthor"><strong><em>La prochaine version d'Ethereum est Metropolis, quelles nouveautés sont-elles prévues? D'ici à combien de temps pourrions-nous la voir arriver ? À l'automne avec la DEVCON2 ou même avant ?  (djinou)</em></strong></p>
<p class="ace-line longKeep gutter-noauthor">Nous travaillons actuellement sur plusieurs choses :</p>

<ul>
 	<li>La première c'est un "client léger" (<em>light client</em>), pour qu'on puisse utiliser Ethereum avec un smartphone, un appareil de Slock.it, etc. Nous travaillons dessus depuis 4 mois et nous avons une version "alpha" opérationnelle, il reste cependant beaucoup de travail pour finaliser le protocole.</li>
</ul>
<ul>
 	<li>La deuxième, c'est Mist, le "<em>navigateur du Web décentralisé</em>". Nous agrandissons l'équipe qui travaille sur ce projet, et pensons que c'est un projet important pour améliorer la facilité d'utilisation d'Ethereum pour les gens "normaux".</li>
</ul>
<ul>
 	<li>La troisième c'est un "<em>hard fork</em>" du protocole, qui comprend des changements pour augmenter l'efficacité, faciliter le développement d'applications sur Ethereum qui utilisent des méthodes de cryptographie complexe (signatures cycliques, etc), faire les premiers étages de "l'abstraction" (<a href="https://blog.ethereum.org/2015/12/24/understanding-serenity-part-i-abstraction/"><span style="text-decoration: underline;">plus d'infos ici</span></a>), et quelques autres modifications mineures.</li>
</ul>
Nous ne pouvons pas prédire quand on va finir tous ces chantiers, et il est donc impossible d'annoncer avec certitude lesquelles feront partie de Metropolis, ni quand Metropolis sortira. Peut-être que le <em>hard fork</em> sortira en même temps que <a href="https://www.ethereum-france.com/le-devcon2-se-tiendra-a-shanghai-du-19-au-21-septembre-2016-avant-le-blockchain-summit/"><span style="text-decoration: underline;">la DEVCON2</span></a>, mais nous ne pouvons pas le promettre.

<strong><em>A propos de Mist, il y a de gros problèmes de synchronisation actuellement, est-ce un point phare dans son développement ?</em></strong>

La synchronisation est un problème très important ; dans la version la plus récente nous avons ajouté un protocole de synchronisation rapide avec lequel on peut synchroniser toute la chaîne en moins d'une heure. Avec un ordinateur rapide et une bonne connexion, certains ont réussi à synchroniser toute la blockchain en six minutes ! Casper va aussi beaucoup améliorer cette situation ; j'espère que nous arriverons à rendre la synchronisation presque instantanée.

<strong><em>Quelques questions sur Casper. Tout d'abord, Casper est-t-il bien le nom de l'algorithme PoS d'Ethereum ou cela englobe plus de choses ?</em></strong>

Oui, Casper c'est le nom de l'algorithme POS sur lequel nous travaillons.

Nous avons aussi une activité de développement en cours sur la <em>scalability </em>(capacité à monter en charge), mais c'est à plus long terme. Nous parlons souvent de ces deux sujets en même temps mais il est très important de ne pas oublier que Casper et <em>scalability</em> sont deux sujets différents.

<strong><em>Simple curiosité, mais d'où vient le nom "Casper" ? (sachant que GHOST est l'acronyme pour Greedy Heaviest Observed Subtree)</em></strong>

Certaines idées du protocole Casper sont basés sur les principes de GHOST, d'où Casper (<a href="https://en.wikipedia.org/wiki/Casper_the_Friendly_Ghost">https://en.wikipedia.org/wiki/Casper_the_Friendly_Ghost</a>)

<strong><em>Comment définirais-tu Casper par rapport aux solutions existantes (bitshare, nxt, peercoin, blackcoin...) ? Est-ce une solution totalement différente ou s'inspire-elle principalement d'une solution existante ?</em></strong>

Casper c'est une combinaison de plusieurs idées, y compris Slasher (<a href="https://blog.ethereum.org/2014/01/15/slasher-a-punitive-proof-of-stake-algorithm/"><span style="text-decoration: underline;">ma première idée du protocole PoS</span></a>), la théorie du consensus tolérant aux défauts byzantins, un peu de NXT.

Nous utilisons la théorie du consensus tolérant aux défauts byzantins, la théorie de jeux et les autres idées des mathématiques et de la cryptographie pour réaliser un protocole qui fournit les garanties du sécurité, vitesse, finalité, etc. le mieux possible.

<strong><em>Slasher c'est une solution contre le problème du "nothing at stake" ? (la première critique que l'on fait au Proof of Stake en général)</em></strong>

Casper est beaucoup plus avancé, sa conception de "<em>consensus par le pari</em>" est une version plus générale des idées de slasher.

<strong><em>Casper a-t-il également pour objectif de réduire le temps de bloc ? Si oui, quel est l'objectif de temps de bloc avec l'arrivée de Casper ? (daboloskov)</em></strong>

Oui, c'est un de ses objectifs. Nous essayons d'atteindre une seconde, mais ce n'est pas garanti. Au mieux nous espérons 1 seconde ou 0.5 secondes, au pire 4-8 secondes pour la première version.

<strong><em>L'objectif principal dans cette réduction du temps, c'est accélérer l’exécution des contrats ?</em></strong>

Oui, faciliter l'utilisation des dApps est très important et les utilisateurs ne veulent pas attendre 14 secondes pour confirmer chaque opération. 14 secondes, c'est déjà bien mieux que 10 minutes (<em>ndlr : le temps entre deux blocs sur la blockchain Bitcoin</em>), mais ce n'est pas parfait.

<strong><em>Revenons aux paramètres. Avez-vous déterminé une fourchette de valeurs pour le pourcentage d'inflation de Casper ? (généralement de 2% pour beaucoup de projets PoS) (jilan)</em></strong>

Avec Casper, cela sera peut-être un peu plus élevé, parce qu'il faut verrouiller son ether et qu'on ne peut pas le toucher pendant 4 mois. Cela fonctionne comme un "compte épargne".

<strong><em>Les 4 mois sont-ils déterminés par l’algorithme ? Ou est-ce la personne qui stake qui va décider du temps ?</em></strong>

C'est déterminé par l'algorithme.

<strong><em>Est-ce qu'Ethereum pourrait abandonner l'idée de passer en PoS si, dans un an par exemple, une solution technique n'était pas trouvée ? (Et travailler sur le PoW dans ce cas-là ?)</em></strong>

Ce sera 100% PoS. Les mineurs savent que le réseau sera PoS. Actuellement ils estiment qu'ils auront assez du temps pour rembourser leur investissement, mais quelques mois avant le déploiement du PoS je pense qu'il n'y aura plus de nouveaux mineurs.

<strong><em>Si je dois traiter des pics de transactions (20k tx/h sans attente de blocs), est-ce qu'Ethereum a pour ambition d'absorber une charge de cet ordre à terme ou est-ce qu'il faut s'orienter vers autre chose ? (anw)</em></strong>

Oui, à long terme, c'est notre objectif. C'est le "sharding".

<strong><em>Quelle est l'idée derrière ce 'sharding' ?</em></strong>

L'idée derrière le sharding est qu'à la place d'avoir chaque noeuds du réseau qui vérifie toutes les transactions, on réunit ces transactions en groupes et on attribue ces groupes aléatoirement à des sous-groupe de noeuds, qui sont chargé de les vérifier. Ensuite, seul un hash du bloc et le "state" est ajouté dans une « header chain » qui est vérifiée et téléchargée par tous les noeuds.

En théorie, si le mécanisme de sélection aléatoire des noeuds  est bien sécurisé, une personne qui veut attaquer la blockchain devrait alors contrôler plus de 40 % du réseau pour compromettre un seul <em>shard</em> (sous-groupe). Et ce fonctionnement permet au réseau de traiter de nombreux groupes de transactions en parallèle, ce qui améliore sensiblement la rapidité de traitement des transactions.

A long terme, il sera possible de concevoir un système dans lequel il n'y aura aucune limite au nombre de transaction que le réseau pourra traiter. Le réseau deviendra de plus en plus puissant pour chaque nouveau node participant...