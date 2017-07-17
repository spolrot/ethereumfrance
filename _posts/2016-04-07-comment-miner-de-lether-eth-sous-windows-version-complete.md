---
ID: 430
post_title: 'Comment miner de l’ether (ETH) sous Windows (version complète) [MàJ 18.07.2016]'
author: Okkoh
post_excerpt: ""
layout: post
permalink: >
  https://www.ethereum-france.com/comment-miner-de-lether-eth-sous-windows-version-complete/
published: true
post_date: 2016-04-07 14:24:04
---
<em>[Edit 18.07.2016: Sous CUDAMiner, la commande farm-recheck n'est plus très utile. L'article est mis à jour en conséquence]</em>
<h1><span class="c13">Introduction</span></h1>
<p class="c10 c22"><span class="c0">Pour miner de l’ether (ETH) en participant à la blockchain Ethereum, vous avez besoin :</span></p>

<ul class="c5 lst-kix_px6kp097bhti-0 start">
 	<li class="c10 c22 c29"><span class="c0">D’un wallet sur lequel envoyer vos ether (0xD95DC4cf508fDDC108709556d0CD70e3F6369C90 par exemple) que vous pouvez </span><span class="c0 c3"><a class="c19" href="https://www.google.com/url?q=http://www.ethereum-france.com/creer-et-gerer-son-portefeuille-dether-en-2-minutes-avec-myetherwallet-com/&amp;sa=D&amp;ust=1460027167751000&amp;usg=AFQjCNGkP4Svg-lOydOBuauSSBjC2FK11g">créer ici</a></span><span class="c0">.</span></li>
 	<li class="c10 c22 c29"><span class="c0">D’un ordinateur doté d’une carte graphique assez puissante (et dotée de minimum </span><strong><span class="c0 c8">2 Go de RAM,<a href="https://www.ethereum-france.com/miner-sur-ethereum-aujourdhui/"> sachant que d'ici fin 2016 il en faudra plus</a></span></strong><span class="c0">). Vous pouvez voir quelques stats ici : </span><span class="c0 c3 c20"><a class="c19" href="http://62.212.74.86/~mining/list/nvidia/index.php?algo=eth" target="_blank">http://62.212.74.86/~mining/list/nvidia/index.php?algo=eth</a></span><span class="c0"> ou avoir une idée de rentabilité de votre matériel ici : </span><span class="c0 c3 c20"><a class="c19" href="https://www.cryptocompare.com/mining/#/equipment" target="_blank">https://www.cryptocompare.com/mining/#/equipment</a></span><span class="c0"> .</span></li>
 	<li class="c10 c22 c29"><span class="c0">De temps et de patience (on y reviendra pour la patience).</span></li>
</ul>
<p class="c10 c22"><span class="c0">Je vais partir sur la façon la plus « simple » de miner, c’est à dire en participant à travers un « </span><span class="c0 c18">pool</span><span class="c0"> » qui permet de mutualiser la puissance de calcul de plusieurs personnes pour miner plus efficacement. Cela permet aussi d’éviter une longue période de synchronisation de la Blockchain.</span></p>
<p class="c10 c22"><span class="c0">Pour vous faire une idée de l'état actuel de la Blockchain, c’est ici : </span><span class="c0 c3 c20"><a class="c19" href="https://etherchain.org/" target="_blank">https://etherchain.org/</a></span><span class="c0"> </span></p>
<p class="c10 c22"><span class="c0">On y apprend pas mal de choses, comme la difficulté actuelle du minage, le Hashrate et</span><span class="c0">,</span><span class="c0"> dans Statistics</span><span class="c0">,</span><span class="c0"> la </span><span class="c0">stat de distribution du hashrate (</span><span class="c0 c3 c20"><a class="c19" href="https://etherchain.org/statistics/miners" target="_blank">https://etherchain.org/statistics/miners</a></span><span class="c0">)</span><span class="c0">.</span></p>
<p class="c10 c22"><span class="c0">Pour ensuite vous faire une idée de la rentabilité de votre affaire</span><span class="c0"> c’est</span><span class="c0"> ici : </span><span class="c0 c3 c20"><a class="c19" href="https://cryptowizzard.github.io/eth-mining-calculator/" target="_blank">https://cryptowizzard.github.io/eth-mining-calculator/</a></span><span class="c0"> </span></p>
<p class="c10 c22"><span class="c0">Enfin, quelques mots de vocabulaire :</span></p>

<ul>
 	<li class="c10 c22"><span class="c0">Fork = Logiciel modifié</span></li>
 	<li class="c10 c22"><span class="c0">Pool = équipe de minage</span></li>
 	<li class="c10 c22"><span class="c0">Wallet = un portefeuille qui stocke vos ethers</span></li>
 	<li class="c10 c22"><span class="c0">Worker/Rig = machine qui mine (le plus souvent, votre PC)</span></li>
</ul>
<p style="text-align: center"><strong><span class="c0 c15 c8">Petit avertissement également pour les investisseurs, le minage type Proof of Work n’est pas prévu pour durer jusqu’à la fin des temps. La Blockchain est censée passer en Proof of Stake d’ici quelques temps, et il n’y aura plus de minage tel que je le présente ici.</span></strong></p>
&nbsp;
<h1 class="c10 c22">Les logiciels</h1>
<p class="c10"><span class="c1">Nous allons faire une liste de quelques logiciels qui vont vous permettre d’entrer de plain-pied dans votre nouvelle activité d’ouvrier des temps modernes, mais avant cela quelques avertissements :</span></p>

<ul class="c5 lst-kix_iuqdbpnn1quu-0 start">
 	<li class="c10 c11"><span class="c1">Pour les possesseurs de cartes <strong>AMD</strong>, <strong>n’utilisez pas les pilotes Catalyst 16.3</strong>, ils feront chuter votre Hashrate. Préfèrez les 15.11.</span></li>
 	<li class="c10 c11"><span class="c1">Pour les possesseurs de cartes <strong>Nvidia</strong>, vous aurez peut-être besoin de télécharger les <strong>pilotes CUDA 7.5</strong> (pour utiliser l'argument -U avec CUDAminer, qui utilise CUDA 7.5). Attention, en cas de downgrade de pilotes Nvidia<strong> sous Windows 10 ca ne sert à rien</strong> (pour les raisons expliquées plus bas, merci à Francis de me l'avoir fait remarquer).</span></li>
 	<li class="c10 c11"><span class="c1">Je vous recommande d’utiliser le fork de Genoil, CUDAminer, quel que soit votre matériel. En utilisant ce logiciel, vous aurez accès à un maximum de possibilités (avec/sans CUDA, avec/sans Stratum, pleine puissance, pas pleine puissance,...).</span></li>
 	<li class="c10 c11"><strong>Désactivez le SLI/Crossfire</strong> pour pouvoir bénéficier de la puissance de chaque carte graphique.</li>
 	<li class="c10 c11"><span class="c1">Quel que soit le logiciel que vous utilisez, soyez </span><strong><span class="c1 c8">patients</span></strong><span class="c1">, utilisez l’aide du programme avant de venir demander de l’aide. Elle est souvent incluse dans le dossier d’installation du programme.</span></li>
 	<li class="c10 c11"><span class="c1">Il existe des <strong>FAQ</strong> sur les sites de chaque pool. Utilisez de préférence ce qu’ils vous recommandent. Évidemment, c’est en anglais, mais si vous vous lancez dans le minage, il est préférable d’avoir quelques connaissances en anglais, en commandes MS-DOS et en dépatouillages et petits bidouillages de programmes. </span></li>
 	<li class="c10 c11"><span class="c1"><strong>N’utilisez pas Windows 10</strong>, surtout si vous avez une carte Nvidia. Pour avoir essayé, c’est la plaie, le hashrate est super mauvais avec des pilotes récents. Je vous épargne les détails. Pour faire face à cette frustration, il vous faudra télécharger les pilotes pour W7, les 347.52, puis les décompresser quelque part et forcer leur installation dans le gestionnaire de périphérique. Puis éviter que W10 remette à jour tout seul le pilote. Sachant que les 347.52 n'ont que les CUDA 6.5, il n'est pas possible de miner avec l'argument -U (car CUDAminer fonctionne avec les CUDA 7.5). Pas facile, mais si ca n'était que ça... A titre personnel, j’ai dû tout formater quand W10 s’est mis à clignoter joyeusement après un redémarrage, sans aucune possibilité de faire quelque chose. Après je ne dis pas que c’est systématique comme bug, mais ça m’a refroidi. Et je n’ai pas testé le dernier Call of Duty avec ces pilotes, je ne peux pas dire si les gros jeux fonctionnent encore. Bon après, c’est pas le but, hein ! Si vous minez, c’est pas pour l’arrêter toutes les 5 min, sinon les ethers vont pas être légion ;).</span></li>
 	<li class="c10 c11"><span class="c1">Windows 10 et les cartes AMD, je n’ai pas testé, je n’ai pas d’avis.</span></li>
 	<li class="c10 c11"><span class="c1">Je propose ici de démarrer votre logiciel en passant par un  fichier .bat, avec un tout petit peu de code </span><strong><span class="c1 c18"><em>cmd /K “start /B …”</em></span></strong><span class="c1">. Ça n’est pas obligatoire, on peut tout à fait mettre les attributs dans le raccourci, mais avec ma méthode </span><span class="c1">vous pourrez lire les indications du logiciel si jamais vous avez tapé une erreur (par </span><span class="c1">défaut</span><span class="c1"> la fenêtre se ferme et sauf si vous êtes un super sayan, vous n’aurez pas le temps de lire le message). De plus, vous pouvez rajouter d’autres choses à effectuer avant le lancement du programme (quelques lignes d’optimisation, lancer un minuteur,... ou autre chose qui vous passe par la tête). </span><strong><span class="c1 c8">Attention, ce fichier .bat doit être dans le dossier du logiciel, et si </span><span class="c1 c8">cela ne vous convient </span><span class="c1 c8">pas il vous faut taper dans le fichier .bat toute l’arborescence pour atteindre votre ethminer.exe ou qtminer.exe.</span></strong></li>
 	<li class="c10 c11"><span class="c1">Lors du premier lancement du logiciel, un fichier DAG est créé, </span><span class="c1">ça</span><span class="c1"> prend un peu de temps.</span><span class="c1"> Patience.</span></li>
</ul>
&nbsp;
<h2>Stratum Proxy</h2>
<p class="c10"><span class="c0">Avec lui, vous ne minez rien du tout, il vient en complément de vos logiciels de minage. En gros ça fonctionne comme ça :</span></p>

<div class="c10"><span class="c30">    Pool A &lt;---+                                    </span><span class="c30">        +-------------+ Rig1 / PC1</span></div>
<div class="c10"><span class="c30">  (Active)        |                                              |                                                </span></div>
<div class="c10"><span class="c30">                        |                                              +-------------+ Rig2 / PC2</span></div>
<div class="c10"><span class="c30">                        |                                              |                                                </span></div>
<div class="c10"><span class="c30">   Pool B &lt;---+-----StratumProxy  &lt;-----+-------------+ Rig3 / PC3</span></div>
<div class="c10"><span class="c30">(FailOver)                                                     |                                                </span></div>
<div class="c10"><span class="c30">                                                                       +-------------+ Rig4 / PC4</span></div>
<div class="c10"><span class="c30">                                                                        |                                                </span></div>
<div class="c10"><span class="c30">                                                                       +-------------+ Leaserigs</span></div>
<p class="c10"><span class="c0">Il permet de coordonner/optimiser/synchroniser le travail pour vos workers et de jongler entre les serveurs des pools en cas de panne chez eux.</span></p>
<p class="c10"><span class="c0">Je ne mets pas de lien ici pour le télécharger, car selon le logiciel que vous allez utiliser, ses fonctions sont déjà implémentées. Comme ça il n’y a pas de confusion possible.</span></p>
&nbsp;
<h2 class="c10">AlethOne</h2>
<p class="c10"><span class="c0">C’est le logiciel qui fait partie </span><span class="c0">d’un </span><span class="c0">ensemble officiel de logiciels. Il n’est pas très compliqué à configurer, il suffit de l’installer, puis de lancer AlethOne, de rentrer un mot de passe fort, de bien se le noter quelque part (si vous le perdez c’est tout de suite beaucoup plus compliqué à faire fonctionner :D ), puis vous débarquerez sur une petite interface graphique soignée. </span></p>
<p class="c10"><span class="c0">Le logiciel est assez simple : on clique sur start, ça mine. On clique sur stop, ça s’arrête. Il est stable, et il n’y a quasiment rien à optimiser/configurer. Du coup si vous minez sur un portable, n’utilisez pas ce logiciel, sauf erreur de ma part vous ne pourrez pas lui indiquer de miner sur le GPU dédié Nvidia ou AMD.</span></p>
<p class="c10"><span class="c0">Notez que vous pouvez spécifier le nom de votre worker si vous en avez plusieurs (j’y reviendrai en parlant des adresses de pool).</span></p>
<p class="c10"><span class="c0">Notez aussi que vous pouvez avoir un accès direct à ethminer.exe, il vous suffit de jeter un oeil dans le dossier d’installation.</span></p>

<h3 class="c10"><span class="c13">Pour miner avec AlethOne :</span></h3>
<p class="c10"><span class="c0">1. Téléchargez et installez AlethOne :</span></p>
<p class="c21 c28"><span class="c0 c3 c20"><a class="c19" href="https://github.com/ethereum/webthree-umbrella/releases" target="_blank">https://github.com/ethereum/webthree-umbrella/releases</a></span></p>
<p class="c10"><span class="c0">2. Lancez AlethOne, choisissez Pool Mining et mettez </span><code><em><span class="c1 c2 c18">URL_POOL</span></em><strong><span class="c6 c1">:</span></strong><em><span class="c1 c2 c18">PORT_POOL</span></em></code> <span class="c0">dans la case prévu à cet effet</span><span class="c0">. Si vous avez plusieurs workers, mettez </span><code><em><span class="c1 c2 c18">URL_POOL</span></em><strong><span class="c6 c1">:</span></strong><em><span class="c1 c2 c18">PORT_POOL</span></em><strong><span class="c0 c15 c8">/</span></strong><em><span class="c0 c2">NOM_DU_WORKER</span></em></code><span class="c0"> (mettez le nom que vous voulez à la place de </span><code><em><span class="c0 c2">NOM_DU_WORKER</span></em></code><span class="c0">). Les url et ports de la pool désirée sont détaillées dans les paragraphes plus loin.</span></p>
<p class="c10"><span class="c0">Avec un peu de dextérité et de jugeote, on peut même utiliser Stratum-Proxy (il faut le télécharger ici : </span><span class="c0 c3 c20"><a class="c19" href="https://github.com/feeleep75/eth-stratum-mining-proxy/releases" target="_blank">https://github.com/feeleep75/eth-stratum-mining-proxy/releases</a></span><span class="c0">), mais je ne suis pas sûr qu’il y ait une grande utilité, du coup je ne m’attarderai pas là dessus.</span></p>
&nbsp;
<h2 class="c10">Ethereum CUDA Miner (Genoil)</h2>
<p class="c10"><span class="c0">C’est un fork réalisé par Genoil. </span><strong><span class="c0 c8">Ce logiciel est vivement recommandé aux possesseurs de cartes Nvidia</span></strong><span class="c0">. En effet, cet ethminer modifié leur permet d’avoir un hashrate un peu plus digne de leur investissement en utilisant les instructions CUDA, tant il est vrai que les cartes graphiques AMD sont bien meilleures en OpenCL que les Nvidia. Ça reste un logiciel assez simple à utiliser, en ligne de commandes uniquement. Un <strong>help.txt</strong> est même fourni pour les bidouilleurs qui cherchent à optimiser leur investissement en t</span><span class="c0">e</span><span class="c0">ntant de gagner quelques % de Hashrate.</span></p>
<p class="c10"><strong><span class="c0 c8">Il fonctionne </span><span class="c0 c8">également </span></strong><span class="c0 c8"><strong>très bien pour les possesseurs de cartes AMD</strong> </span><span class="c0">(et chez moi mieux que Qt-Miner, mais je ne peux pas dire si c’est une généralité car j’ai une config</span><span class="c0">uration</span><span class="c0"> bizarre</span><span class="c0"> :</span><span class="c0"> AMD R9 270 + Nvidia GTX 660 sous W7).</span></p>
<p class="c10"><span class="c0">Notez que Genoil, dans sa grande bonté, a implémenté Stratum-Proxy dans la dernière version de son fork. Un bon, quoi.</span></p>

<h3 class="c10">Miner avec Stratum-Proxy</h3>
1. Téléchargez et installez le CUDA Miner :
<p class="c21 c28" style="text-align: center"><span class="c0 c3 c20"><a class="c19" href="https://github.com/Genoil/cpp-ethereum/tree/master/releases" target="_blank">https://github.com/Genoil/cpp-ethereum/tree/master/releases</a></span></p>
<p class="c21 c28" style="text-align: center">OU</p>
<p style="text-align: center"><a href="https://github.com/Genoil/cpp-ethereum/tree/master/releases/cuda-6.5">https://github.com/Genoil/cpp-ethereum/tree/master/releases/cuda-6.5</a> (CUDA 6.5 pour Windows 10 et Nvidia)</p>
<span class="c1">2. Ouvrez le Bloc-Notes, et écrivez les lignes suivantes : </span>
<p class="c10 c24"><span class="c3 c1">Si vous avez une ou plusieurs cartes graphiques Nvidia</span><span class="c3 c1"> </span><span class="c3 c1">:</span></p>

<pre class="c14"><span class="c6 c1">cmd /K "start /B ethminer.exe -U -S </span><span class="c1 c2 c18">URL_POOL</span><span class="c6 c1">:</span><span class="c1 c2 c18">PORT_POOL</span><span class="c7 c1"> </span><span class="c6 c1">-O</span><span class="c7 c1"> </span><span class="c1 c2 c18">VOTRE</span><span class="c1 c2 c18">_WALLET</span><span class="c6 c1">.</span><span class="c1 c2 c18">NOM_DU_WORKER</span><span class="c6 c1">”
</span><span class="c6 c1">pause</span></pre>
<p class="c10 c24"><span class="c3 c1">Si vous avez </span><span class="c3 c1">une ou plusieurs cartes graphiques AMD</span><span class="c3 c1"> </span><span class="c3 c1">:</span></p>

<pre class="c14"><span class="c6 c1">cmd /K “start /B ethminer.exe -G -S </span><span class="c1 c2 c18">URL_POOL</span><span class="c6 c1">:</span><span class="c1 c2 c18">PORT_POOL</span><span class="c6 c1"> -O</span><span class="c7 c1"> </span><span class="c1 c2 c18">VOTRE</span><span class="c1 c2 c18">_WALLET</span><span class="c6 c1">.</span><span class="c1 c2 c18">NOM_DU_WORKER</span><span class="c6 c1">”
</span><span class="c6 c1">pause</span></pre>
<p class="c10 c24"><span class="c3 c1">Si vous avez :</span></p>

<ul>
 	<li class="c10 c24"><span class="c1">un PC portable avec un combo carte intégré Intel + GPU AMD ou Nvidia</span></li>
 	<li class="c10 c24">un combo carte AMD+Nvidia</li>
</ul>
<pre class="c14 c27"><span class="c6 c1">cmd /K “start /B ethminer.exe -G -S </span><span class="c1 c2 c18">URL_POOL</span><span class="c6 c1">:</span><span class="c1 c2 c18">PORT_POOL</span><span class="c7 c1"> </span><span class="c6 c1">-O</span><span class="c7 c1"> </span><span class="c1 c2 c18">VOTRE</span><span class="c1 c2 c18">_WALLET</span><span class="c6 c1">.</span><span class="c1 c2 c18">NOM_DU_WORKER </span><span class="c6 c1">--opencl-platform 1”
</span><span class="c6 c1">pause</span></pre>
<p class="c10 c24"><span class="c1">Notez que l’on ne peut pas miner avec une CG Nvidia+AMD en même temps. Donc selon la carte sur laquelle vous désirez miner (la plus puissante ?), changez </span><code><strong><em><span class="c6 c1">--opencl-platform</span></em></strong></code><span class="c1 c2 c18"> </span><span class="c1 c18">(</span><code><strong><span class="c1 c15 c8">0</span></strong></code><span class="c1 c18">=</span><span class="c1">1ère carte, celle qui gère l’affichage, </span><code><strong><span class="c1 c15 c8">1</span></strong></code><span class="c1">=2ème carte</span><span class="c1 c18">).</span></p>
<p class="c10 c24"><span class="c1">Evidemment, changez </span><code><em><span class="c1 c2">URL_POOL</span></em></code><span class="c1">, </span><code><em><span class="c1 c2">PORT_POOL</span></em></code><span class="c1"> et </span><code><em><span class="c1 c2">VOTRE</span><span class="c1 c2">_WALLET</span></em></code><span class="c1"> (la mienne par exemple : 0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64) et ne mettez </span><code><span class="c1 c2"><em><strong>.</strong>NOM_DU_WORKER</em></span></code><span class="c1"> que si ça vous est utile (si vous avez plusieurs workers). Les url et ports de la pool désirée sont détaillées dans les paragraphes plus loin.</span></p>
<p class="c10"><span class="c1">3. Sauvez votre fichier en <em>.bat</em> </span><strong><span class="c1 c8">dans le dossier du logiciel</span></strong><span class="c1"> c’est à dire </span><span class="c1">là où vous l’avez décompressé (</span><span class="c1">Fichier &gt; E</span><span class="c1">nregistrer sous -&gt; </span><span class="c1">Nom “</span><span class="c1">LAUNCH.bat</span><span class="c1">”</span><span class="c1">)</span></p>
<p class="c10"><span class="c1">4. Lancez le logiciel en double-cliquant sur votre fichier LAUNCH.bat.</span></p>

<h3 class="c10">Miner sans Stratum-Proxy</h3>
<p class="c10"><span class="c1">1. Téléchargez et installez le CUDA Miner :</span></p>
<p class="c10" style="text-align: center"><span class="c1"> </span><span class="c0 c3 c20"><a class="c19" href="https://github.com/Genoil/cpp-ethereum/tree/master/releases" target="_blank">https://github.com/Genoil/cpp-ethereum/tree/master/releases</a></span></p>
<p class="c10"><span class="c1">2. Ouvrez le Bloc-Notes, et écrivez les lignes suivantes : </span></p>
<p class="c10 c24"><span class="c3 c1">Si vous avez une ou plusieurs Nvidia</span><span class="c3 c1"> </span><span class="c3 c1">:</span></p>

<pre class="c14"><span class="c6 c1">cmd /K "start /B ethminer.exe -F </span><span class="c1 c2 c18">URL_POOL</span><span class="c6 c1">:</span><span class="c1 c2 c18">PORT_POOL</span><span class="c6 c1">/</span><span class="c1 c2 c18">VOTRE</span><span class="c1 c2 c18">_WALLET</span><span class="c1 c6">/</span><span class="c1 c2 c18">NOM_DU_WORKER</span><span class="c6 c1">/</span><span class="c1 c2 c18">VOTRE</span><span class="c1 c2 c18">_EMAIL</span><span class="c7 c1"> </span><span class="c6 c1">-U”
</span><span class="c6 c1">pause</span></pre>
<p class="c10 c24"><span class="c3 c1">Si vous avez une ou plusieurs AMD</span><span class="c3 c1"> </span><span class="c3 c1">:</span></p>

<pre class="c14"><span class="c6 c1">cmd /K "start /B ethminer.exe -F</span><span class="c7 c1"> </span><span class="c1 c2 c18">URL_POOL</span><span class="c6 c1">:</span><span class="c1 c2 c18">PORT_POOL</span><span class="c6 c1">/</span><span class="c1 c2 c18">VOTRE</span><span class="c1 c2 c18">_WALLET</span><span class="c6 c1">/</span><span class="c1 c2 c18">NOM_DU_WORKER</span><span class="c6 c1">/</span><span class="c1 c2 c18">VOTRE</span><span class="c1 c2 c18">_EMAIL</span><span class="c7 c1"> </span><span class="c6 c1">-G”
</span><span class="c6 c1">pause</span></pre>
<p class="c10 c24"><span class="c3 c1">Si vous avez :</span></p>

<ul class="c5 lst-kix_j2lwdifuoy79-0">
 	<li class="c10 c16"><span class="c1">un PC portable avec un combo carte intégré Intel + GPU AMD ou Nvidia</span></li>
 	<li class="c10 c16"><span class="c1">un combo carte AMD+Nvidia</span></li>
</ul>
<pre class="c10 c24"><span class="c6 c1">cmd /K "start /B ethminer.exe -F</span><span class="c7 c1"> </span><span class="c1 c2 c18">URL_POOL</span><span class="c6 c1">:</span><span class="c1 c2 c18">PORT_POOL</span><span class="c6 c1">/</span><span class="c1 c2 c18">VOTRE</span><span class="c1 c2 c18">_WALLET</span><span class="c6 c1">/</span><span class="c1 c2 c18">NOM_DU_WORKER</span><span class="c6 c1">/</span><span class="c1 c2 c18">VOTRE</span><span class="c1 c2 c18">_EMAIL</span><span class="c7 c1"> </span><span class="c6 c1">-G --opencl-platform 1”
</span><span class="c6 c1">pause</span></pre>
<p class="c10 c24"><span class="c1">Notez que l’on ne peut pas miner avec une CG Nvidia</span><span class="c1"> et une </span><span class="c1">CG</span><span class="c1"> </span><span class="c1">AMD en même temps. Donc selon la carte sur laquelle vous désirez miner (la plus puissante ?), changez </span><code><strong><em><span class="c6 c1">--opencl-platform</span></em></strong></code><span class="c1 c18"><em> </em>(</span><code><strong><span class="c1 c15 c8">0</span></strong></code><span class="c1 c18">=</span><span class="c1">1ère carte, celle qui gère l’affichage, </span><code><strong><span class="c1 c15 c8">1</span></strong></code><span class="c1">=2ème carte</span><span class="c1 c18">).</span></p>
<p class="c10 c24"><span class="c1">Evidemment, changez </span><code><em><span class="c1 c2 c18">URL_POOL</span></em></code><span class="c1">, </span><code><em><span class="c1 c2 c18">PORT_POOL</span></em></code> <span class="c1">et </span><code><em><span class="c1 c2 c18">VOTRE</span><span class="c1 c2 c18">_WALLET</span></em></code><span class="c1"> (la mienne</span><span class="c1">, pour l’</span><span class="c1">exemple : 0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64) et ne mettez <code><strong>/</strong></code></span><code><em><span class="c1 c2 c18">NOM_DU_WORKER</span></em></code><span class="c1"> et <code><strong>/</strong></code></span><code><em><span class="c1 c2">VOTRE</span><span class="c1 c2">_EMAIL</span></em></code> <span class="c1">que si ça vous est utile. Les url et ports de la pool désirée sont détaillées dans les paragraphes plus loin.</span></p>
<p class="c10"><span class="c1">3. Sauvez votre fichier en <em>.bat </em></span><strong><span class="c1 c8">dans le dossier du logiciel</span></strong><span class="c1"> c’est à dire là où vous l’avez décompressé (enregistrer sous -&gt; LAUNCH.bat)</span></p>
<p class="c10"><span class="c1">4. Lancez le logiciel en double-cliquant sur votre fichier LAUNCH.bat.</span></p>

<h3 class="c10">Les options du logiciel</h3>
<p class="c10"><span class="c1">Pour info, il y a des options possibles, à rajouter à la fin, mais tout </span><span class="c1">ça</span><span class="c1"> dépend de votre </span><span class="c1">matériel </span><span class="c1">et de la configuration que vous voulez faire :</span></p>

<h4 class="c10"><span class="c3 c1">Options qui fonctionnent </span><span style="text-decoration: underline"><span class="c3 c1 c8">avec l’attribut -U </span></span><span class="c3 c1"><span style="text-decoration: underline">(CUDA)</span> :</span></h4>
<p class="c10 c24"><span class="c1">Pour pouvoir régler au mieux sa config, utiliser au préalable l’option </span><code><strong><em><span class="c1 c15">--list-devices</span></em></strong></code><span class="c1"> qui est très utile pour connaître ses périphériques CUDA. Une des indications donnée, <code>CL_DEVICE_MAX_WORK_GROUP_SIZE</code> permet de connaître la valeur à donner à l’option </span><code><strong><em><span class="c1 c15">--cl-local-work</span></em></strong></code><span class="c1">.</span></p>

<table style="height: 220px" width="1168">
<tbody>
<tr>
<td><em><strong><code>--cuda-extragpu-mem xxx</code></strong></em></td>
<td style="text-align: left">
<div><span class="c1">permet de ne pas utiliser </span><span class="c1 c15">xxx</span><span class="c1">MB de mémoire du GPU </span></div>
<div><span class="c1">permet de faire autre chose que du minage.</span></div></td>
</tr>
<tr>
<td><em><strong><code>--cuda-block-size xxx</code></strong></em></td>
<td style="text-align: left">
<div><span class="c1">définit la taille du bloc de travail CUDA à </span><span class="c1 c15">xxx</span><span class="c1">. </span></div>
<div><span class="c1">Si on ne met pas l’option, la valeur de 128 est prise en compte.</span></div></td>
</tr>
<tr>
<td><em><strong><code>--cuda-grid-size xxx</code></strong></em></td>
<td style="text-align: left">
<div><span class="c1">définit la taille de la grille CUDA à </span><span class="c1 c15">xxx</span><span class="c1">. </span></div>
<div><span class="c1">Si on ne met pas l’option, la valeur de 8192 (soit 128*64) est prise en compte.</span></div></td>
</tr>
<tr>
<td><em><strong><code>--cuda-streams x</code></strong></em></td>
<td style="text-align: left">
<div><span class="c1">définit le nombre de streams CUDA à </span><span class="c1 c15">x</span><span class="c1">. </span></div>
<div><span class="c1">Par défaut, c’est 2.</span></div></td>
</tr>
<tr>
<td><em><strong><code><span class="c1 c15">--cuda-devices</span><span class="c1"> </span><span class="c1 c15">0 1 ..n</span></code></strong></em></td>
<td style="text-align: left">
<div>permet de définir les GPU CUDA qui vont miner. Par défaut, tous.</div>
<div>Mettre leur numéros, séparés par un espace.</div>
<div>Le premier chiffre est 0</div></td>
</tr>
</tbody>
</table>
<h4 class="c10 c24"><span class="c3 c1">Options qui fonctionnent </span><span style="text-decoration: underline"><span class="c3 c1 c8">avec l’attribut -G</span></span><span class="c3 c1"><span style="text-decoration: underline"> (OpenCL)</span> :</span></h4>
<p class="c10 c24"><span class="c1">Pour pouvoir régler au mieux sa config, utiliser au préalable l’option </span><code><strong><em><span class="c1 c15">--list-devices</span></em></strong></code><span class="c1"> qui est très utile pour connaître ses périphériques OpenCL. Une des indications donnée, </span><span class="c1"><code>CL_DEVICE_MAX_WORK_GROUP_SIZE</code> permet de connaître la valeur à donner à l’option </span><code><strong><em><span class="c1 c15">--cl-local-work</span></em></strong></code><span class="c1">.</span></p>

<table style="height: 183px" width="1091">
<tbody>
<tr>
<td><em><strong><code>--opencl-platform x</code></strong></em></td>
<td style="text-align: left">
<div>Force l’utilisation de la plateforme x.</div>
<div>Les différentes plateformes disponibles sont données en faisant un <code><strong><em>--list-devices</em></strong></code>)</div></td>
</tr>
<tr>
<td><em><strong><code>--opencl-device x </code></strong></em></td>
<td style="text-align: left">
<div>Force l’utilisation du périphérique x.</div>
<div>Les différents périphériques disponibles sont donnés en faisant un <code><strong><em>--list-devices</em></strong></code>)</div></td>
</tr>
<tr>
<td><em><strong><code><span class="c1 c15">--opencl-devices  0 1 2 ..n</span></code></strong></em></td>
<td style="text-align: left">
<div>Force l’utilisation simultanée des périphériques spécifiés.</div>
<div>Les différents périphériques disponibles sont donnés en faisant un <code><strong><em>--list-devices</em></strong></code>)</div></td>
</tr>
<tr>
<td><em><strong><code>--allow-opencl-cpu</code></strong></em></td>
<td style="text-align: left">
<div>Permet de considérer le CPU comme un périphérique OpenCL,</div>
<div>Si tant est que la plateforme OpenCL le supporte.</div></td>
</tr>
<tr>
<td><em><strong><code>--cl-extragpu-mem xxx</code></strong></em></td>
<td style="text-align: left">
<div><span class="c1">Permet de ne pas utiliser </span><span class="c1 c15">xxx</span><span class="c1">MB de mémoire du GPU.</span></div>
<div><span class="c1">Pour permettre de faire autre chose que du minage.</span></div></td>
</tr>
<tr>
<td><em><strong><code>--cl-local-work xxx</code></strong></em></td>
<td style="text-align: left">
<div><span class="c1">Définit la taille du travail local OpenCL à </span><span class="c1 c15">xxx</span><span class="c1">. </span></div>
<div><span class="c1">Si on ne met pas l’option, la valeur de 64 est prise en compte.</span></div></td>
</tr>
<tr>
<td><em><strong><code>--cl-global-work xxx</code></strong></em></td>
<td style="text-align: left">
<div><span class="c1">Définit la taille du travail local OpenCL à </span><span class="c1 c15">xxx</span><span class="c1">. </span></div>
<div><span class="c1">Doit être un multiple de la valeur prise pour </span><code><strong><em><span class="c1 c15">--cl-local-work</span></em></strong></code><span class="c1">.  </span></div>
<div><span class="c1">Si on ne met pas l’option, la valeur de 4096 (64*64) est prise en compte.</span></div></td>
</tr>
</tbody>
</table>
<h3 class="c10 c24"><span class="c13">Exemples</span></h3>
<p class="c10"><span class="c1">Fonctionnement réduit avec 1 GPU Nvidia pour pouvoir bosser en même temps :</span></p>

<pre class="c21"><span class="c7 c1">cmd /K "start /B ethminer.exe <strong>-U</strong> -S URL_POOL:PORT_POOL -O </span><span class="c7 c1">VOTRE</span><span class="c7 c1">_WALLET.NOM_DU_WORKER </span><strong><span class="c1 c15 c8">--cuda-extragpu-mem 1024 --cl-local-work 32 --cuda-grid-size 1024 --cuda-streams 1</span></strong><span class="c7 c1">”
p</span><span class="c7 c1">ause</span></pre>
<p class="c10"><span class="c1">Fonctionnement réduit avec 1 GPU AMD pour pouvoir bosser en même temps :</span></p>

<pre class="c21"><span class="c7 c1">cmd /K "start /B ethminer.exe <strong>-G</strong> -S URL_POOL:PORT_POOL -O </span><span class="c7 c1">VOTRE</span><span class="c7 c1">_WALLET.NOM_DU_WORKER </span><strong><span class="c1 c15 c8">--cl-extragpu-mem 1024 --cl-local-work 32 --cl-global-work 1024</span></strong><span class="c7 c1">”
p</span><span class="c7 c1">ause</span></pre>
<p class="c10"><span class="c1">U</span><span class="c1">n PC avec 2 GPU</span><span class="c1"> Nvidia</span><span class="c1"> où l’on ne veut faire fonctionner que la seconde pour pouvoir taffer à côté :</span></p>

<pre class="c21"><span class="c7 c1">cmd /K "start /B ethminer.exe <strong>-U</strong> -S URL_POOL:PORT_POOL -O </span><span class="c7 c1">VOTRE</span><span class="c7 c1">_WALLET.NOM_DU_WORKER </span><strong><span class="c1 c15 c8">--cuda-devices 1</span></strong><span class="c7 c1">”
</span><span class="c7 c1">pause</span></pre>
<p class="c10"><span class="c1">Pour être sûr de faire fonctionner les deux Nvidia en même temps :</span></p>

<pre class="c21"><span class="c7 c1">cmd /K "start /B ethminer.exe <strong>-U</strong> -S URL_POOL:PORT_POOL -O </span><span class="c7 c1">VOTRE</span><span class="c7 c1">_WALLET.NOM_DU_WORKER </span><strong><span class="c1 c15 c8">--cuda-devices 0 1</span></strong><span class="c7 c1">”
</span><span class="c7 c1">pause</span></pre>
<p class="c10"><span class="c1">Un PC avec 1 CG AMD + 1 CG Nvidia où l’on ne veut faire fonctionner que celle qui n’est pas utilisée pour l’affichage (ici la AMD, le cable de l’écran est sur la Nvidia) pour pouvoir taffer à côté :</span></p>

<pre class="c21"><span class="c7 c1">cmd /K "start /B ethminer.exe <strong>-G</strong> -S URL_POOL:PORT_POOL -O </span><span class="c7 c1">VOTRE</span><span class="c7 c1">_WALLET.NOM_DU_WORKER </span><strong><span class="c1 c15 c8">--opencl-platform 1</span></strong><span class="c7 c1">”
</span><span class="c7 c1">pause</span></pre>
<p class="c10"><span class="c1">Si l’on avait voulu faire fonctionner la Nvidia, il aurait suffit de mettre :</span></p>

<pre class="c21"><span class="c7 c1">cmd /K "start /B ethminer.exe <strong>-U</strong> -S URL_POOL:PORT_POOL -O </span><span class="c7 c1">VOTRE</span><span class="c7 c1">_WALLET.NOM_DU_WORKER”
p</span><span class="c7 c1">ause</span></pre>
<p class="c21"><span class="c1">Car le seul périphérique CUDA existant est la carte Nvidia.</span></p>
&nbsp;
<h2 class="c21">Qt-miner</h2>
<p class="c10"><span class="c0">C’est un fork du logiciel Ethereum, je ne sais pas trop qui l’a fait (je crois que c’est la Ethpool, peut-être quelqu’un pourra-t-il me confirmer), mais certaines pools le proposent (au hasard, ethpool.org et ethermine.org). Il ne change pas énormément du logiciel de base mais ajoute quelques fonctions de paramétrage et Stratum-Proxy est implémenté (on ne peut pas faire fonctionner le logiciel sans, donc il ne fonctionne pas avec certaines pools comme Nanopool).</span></p>

<h3>Miner avec Qt-Miner</h3>
<p class="c10"><span class="c1">1. Téléchargez et installez le Qt-Miner :</span></p>
<p class="c21 c28" style="text-align: center"><span class="c0 c3 c20"><a class="c19" href="http://cryptomining-blog.com/wp-content/download/qtminer-windows.zip" target="_blank">http://cryptomining-blog.com/wp-content/download/qtminer-windows.zip</a></span></p>
<p class="c10"><span class="c1">2. Ouvrez le Bloc-Notes, et écrivez les lignes suivantes : </span></p>

<pre><span class="c6 c1">cmd /K "start /B qtminer.exe -s </span><span class="c1 c2 c18">URL_POOL</span><span class="c6 c1">:</span><span class="c1 c2 c18">PORT_POOL</span><span class="c7 c1"> </span><span class="c6 c1">-u</span><span class="c7 c1"> </span><span class="c1 c2 c18">VOTRE</span><span class="c1 c2 c18">_WALLET</span><span class="c6 c1">.</span><span class="c1 c2 c18">NOM_DU_WORKER</span><span class="c7 c1"> </span><span class="c6 c1">-G"
</span><span class="c6 c1">pause</span></pre>
<p class="c10 c24"><span class="c3 c1">Si vous avez:</span></p>

<ul class="c5 lst-kix_j2lwdifuoy79-0">
 	<li class="c10 c16"><span class="c1">un PC portable avec un combo carte intégré Intel + GPU AMD/Nvidia</span></li>
 	<li class="c10 c16"><span class="c1">un combo carte AMD+Nvidia</span></li>
</ul>
<pre class="c14"><span class="c6 c1">cmd /K "start /B qtminer.exe -s </span><span class="c1 c2 c18">URL_POOL</span><span class="c6 c1">:</span><span class="c1 c2 c18">PORT_POOL</span><span class="c7 c1"> </span><span class="c6 c1">-u</span><span class="c7 c1"> </span><span class="c1 c2 c18">VOTRE</span><span class="c1 c2 c18">_WALLET</span><span class="c6 c1">.</span><span class="c1 c2 c18">NOM_DU_WORKER</span><span class="c7 c1"> </span><span class="c6 c1">-G --opencl-platform 1”
</span><span class="c6 c1">pause</span></pre>
<p class="c10 c24"><span class="c1">Notez que l’on ne peut pas miner avec une CG Nvidia+AMD en même temps. Donc selon la carte sur laquelle vous désirez miner (la plus puissante ?), changez </span><code><strong><em><span class="c6 c1">--opencl-platform</span></em></strong></code><span class="c1 c18"><em> </em>(</span><code><strong><span class="c1 c15 c8">0</span></strong></code><span class="c1 c18">=</span><span class="c1">1ère carte, celle qui gère l’affichage, </span><code><strong><span class="c1 c15 c8">1</span></strong></code><span class="c1">=2ème carte</span><span class="c1 c18">).</span></p>
<p class="c10 c24"><span class="c1">Evidemment, changez </span><code><em><span class="c1 c2">URL_POOL</span></em></code><span class="c1">, </span><code><em><span class="c1 c2">PORT_POOL</span></em></code><span class="c1"> et </span><code><em><span class="c1 c2">VOTRE</span><span class="c1 c2">_WALLET</span></em></code> <span class="c1">(la mienne par exemple : 0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64) et ne mettez <code><em><strong>.</strong>NOM_DU_WORKER</em></code> que si ça vous est utile. Les url et ports de la pool désirée sont détaillées dans les paragraphes plus loin.</span></p>
<p class="c10"><span class="c1">3. Sauvez votre fichier en <em>.bat</em> </span><strong><span class="c1 c8">dans le dossier du logiciel</span></strong><span class="c1"><strong> </strong>c’est à dire là où vous l’avez décompressé (enregistrer sous -&gt; LAUNCH.bat)</span></p>
<p class="c10"><span class="c1">4. Lancez le logiciel en double-cliquant sur votre fichier LAUNCH.bat.</span></p>

<h3 class="c10"><span class="c13">Les options du logiciel</span></h3>
<p class="c10"><span class="c1">Pour info, il y a des options possibles, à rajouter à la fin, mais tout ça dépend de votre matériel et de la configuration que vous voulez faire.</span></p>
<p class="c10"><span class="c1">Mais pour pouvoir régler au mieux sa config, il faut utiliser au préalable l’option </span><code><strong><em><span class="c1 c15">--list-devices</span></em></strong></code><span class="c1"> qui est très utile pour connaître ses périphériques OpenCL. Une des indications donnée, <code>CL_DEVICE_MAX_WORK_GROUP_SIZE</code> permet de connaître la valeur à donner à l’option </span><code><strong><em><span class="c1 c15">--cl-local-work</span></em></strong></code><span class="c1">.</span></p>

<table style="height: 183px" width="1091">
<tbody>
<tr>
<td><em><strong><code>--opencl-platform x</code></strong></em></td>
<td style="text-align: left">
<div>Force l’utilisation de la plateforme x.</div>
<div>Les différentes plateformes disponibles sont données en faisant un <code><strong><em>--list-devices</em></strong></code>)</div></td>
</tr>
<tr>
<td><em><strong><code>--opencl-device x</code></strong></em></td>
<td style="text-align: left">
<div>Force l’utilisation du périphérique x.</div>
<div>Les différents périphériques disponibles sont donnés en faisant un <code><strong><em>--list-devices</em></strong></code>)</div></td>
</tr>
<tr>
<td><em><strong><code><span class="c1 c15">--opencl-devices  0 1 2 ..n</span></code></strong></em></td>
<td style="text-align: left">
<div>Force l’utilisation simultanée des périphériques spécifiés.</div>
<div>Les différents périphériques disponibles sont donnés en faisant un <code><strong><em>--list-devices</em></strong></code>)</div></td>
</tr>
<tr>
<td><em><strong><code>--allow-opencl-cpu</code></strong></em></td>
<td style="text-align: left">
<div>Permet de considérer le CPU comme un périphérique OpenCL,</div>
<div>Si tant est que la plateforme OpenCL le supporte.</div></td>
</tr>
<tr>
<td><em><strong><code>--cl-extragpu-mem xxx</code></strong></em></td>
<td style="text-align: left">
<div><span class="c1">Permet de ne pas utiliser </span><span class="c1 c15">xxx</span><span class="c1">MB de mémoire du GPU.</span></div>
<div><span class="c1">Pour permettre de faire autre chose que du minage.</span></div></td>
</tr>
<tr>
<td><em><strong><code>--cl-local-work xxx</code></strong></em></td>
<td style="text-align: left">
<div><span class="c1">Définit la taille du travail local OpenCL à </span><span class="c1 c15">xxx</span><span class="c1">.</span></div>
<div><span class="c1">Si on ne met pas l’option, la valeur de 64 est prise en compte.</span></div></td>
</tr>
<tr>
<td><em><strong><code>--cl-global-work xxx</code></strong></em></td>
<td style="text-align: left">
<div><span class="c1">Définit la taille du travail local OpenCL à </span><span class="c1 c15">xxx</span><span class="c1">.</span></div>
<div><span class="c1">Doit être un multiple de la valeur prise pour </span><code><strong><em><span class="c1 c15">--cl-local-work</span></em></strong></code><span class="c1">.  </span></div>
<div><span class="c1">Si on ne met pas l’option, la valeur de 4096 (64*64) est prise en compte.</span></div></td>
</tr>
</tbody>
</table>
<h3 class="c10 c24"><span class="c13">Exemples</span></h3>
<p class="c10"><span class="c1">Fonctionnement réduit avec 1 GPU pour pouvoir bosser en même temps :</span></p>

<pre class="c21"><span class="c7 c1">cmd /K "start /B </span><span class="c1 c15">qtminer.exe -s URL_POOL:PORT_POOL -u </span><span class="c1 c15">VOTRE</span><span class="c1 c15">_WALLET.NOM_DU_WO</span><span class="c7 c1">RKER -G </span><strong><span class="c6 c1">--cl-extragpu-mem 1024 </span><span class="c1 c15 c8">--cl-local-work 32 --cl-global-work 1024</span></strong><span class="c7 c1">”
</span><span class="c7 c1">pause</span></pre>
<p class="c10"><span class="c1">Un PC avec 2 CG (1 AMD, 1 Nvidia) où l’on ne veut faire fonctionner que la seconde (celle où il n’y a pas l’écran branché dessus) pour pouvoir taffer à côté :</span></p>

<pre class="c21"><span class="c7 c1">cmd /K "start /B </span><span class="c1 c15">qtminer.exe -s URL_POOL:PORT_POOL -u </span><span class="c1 c15">VOTRE</span><span class="c1 c15">_WALLET.NOM_DU_WO</span><span class="c7 c1">RKER -G </span><strong><span class="c1 c15 c8">--opencl-platform 1</span></strong><span class="c7 c1">”
</span><span class="c7 c1">pause</span></pre>
<p class="c10"><span class="c1">Un PC avec 2 CG (2 AMD ou 2 Nvidia) où l’on ne veut faire fonctionner que la seconde (celle où il n’y a pas l’écran branché dessus) pour pouvoir taffer à côté :</span></p>

<pre class="c21"><span class="c7 c1">cmd /K "start /B </span><span class="c1 c15">qtminer.exe -s URL_POOL:PORT_POOL -u </span><span class="c1 c15">VOTRE</span><span class="c1 c15">_WALLET.NOM_DU_WO</span><span class="c7 c1">RKER -G </span><strong><span class="c1 c15 c8">--opencl-device 1</span></strong><span class="c7 c1">”
</span><span class="c7 c1">pause</span></pre>
&nbsp;
<h2 class="c21">EthOS</h2>
<p class="c10" style="text-align: center"><span class="c3 c1 c20"><a class="c19" href="http://ethosdistro.com/" target="_blank">http://ethosdistro.com/</a></span></p>
<p class="c10 c32"><span class="c1">On trouve en cherchant un peu un OS Linux orienté minage d’ether. Je n’ai personnellement pas utilisé EthOS, dans la mesure le logiciel est payant et qu’il ne marche pas avec les cartes Nvidia. Mais il a un avantage, c’est qu’il est fourni sur un SSD et qu’il n’y a plus qu’à booter dessus, à faire 2-3 réglages et à commencer à miner. </span><span class="c1">Je n</span><span class="c1">’en ai pas eu besoin.</span></p>
&nbsp;
<h1 class="c10 c32">Les pools et comment y participer</h1>
<p class="c10"><span class="c1">Pour miner, le plus aisé actuellement est de rejoindre une pool. Ça permet d’optimiser le travail de mining. Notez qu’il est peu contraignant d’être dans une pool. En effet, la majorité ne nécessitent aucune inscription, pour y participer il suffit d’utiliser leur serveur, on s’identifie grâce à son wallet. La seule chose à bien vérifier, c’est comment la pool rémunère et combien de temps il faut pour commencer à avoir un aperçu de vos statistiques (oui, mesdames et messieurs, vous êtes bien souvent très/trop pressé(e)s!).</span></p>
<p class="c10"><span class="c1">Notez que je ne donne que les méthodes pour miner avec </span><strong><span class="c1 c8">CUDA Miner</span></strong><span class="c1"> vu qu’il est passe-partout et </span><strong><span class="c1 c8">Qt-Miner</span></strong><span class="c1">. Ce sont les 2 logiciels les plus sollicités. Si vous voulez utiliser autre chose, inspirez-vous de ce que vous avez ici et des FAQ propre à la pool que vous avez choisi.</span></p>
&nbsp;
<h2 class="c10">Dwarfpool</h2>
<p class="c10" style="text-align: center"><span class="c3 c1 c20"><a class="c19" href="http://dwarfpool.com/eth" target="_blank">http://dwarfpool.com/eth</a></span></p>
<p class="c10"><span class="c1">La Dwarfpool, c’est la plus grosse, historiquement au dessus du lot il me semble, mais ça n’est plus tellement vrai, d’autres pools sont techniquement bien au point. Selon les envies, le fait qu’ils ne paient que 4 fois par jour, uniquement si le montant est d’au moins 1 ether, peut être frustrant pour certains.</span></p>
<p class="c10"><span class="c1">Le minage est anonyme (pas de compte à créer). </span></p>
<p class="c10"><span class="c1">La page des stats n’est pas folichonne, mais il y a l’essentiel et l’évolution de vos stats va assez vite. Les vitesses affichées sont calculées selon les derniers partages reçus c’est assez vite juste (environ 30min).</span></p>
<p class="c10"><span class="c1"> </span></p>
<p class="c10"><span class="c1">A noter que cette pool fait l’immense partie du Hash de la Blockchain, aussi il me semble qu’il vaudrait mieux ne pas l’utiliser pour ne pas lui conférer le pouvoir d’avoir la main sur la Blockchain (ce qui peut être le cas si elle dépasse 50%).</span></p>

<h3 class="c10"><span class="c1">Pour miner sur Dwarfpool</span></h3>
<ol class="c5 lst-kix_xtz30ut0r1v3-0 start" start="1">
 	<li class="c10 c11"><span class="c1">Installer CUDA Miner et le paramétrer avec la config pour miner <strong>avec</strong> Stratum-Proxy (plus efficace de 10 à 20% selon eux), </span><span class="c1 c8"><strong>comme décrit dans le paragraphe dédié à la présentation du logiciel</strong>. </span></li>
 	<li class="c10 c11"><span class="c1">Utilise les paramètres suivants pour créer ton fichier .bat :</span></li>
</ol>
<ul>
 	<li class="c10 c25 c24"><strong><span class="c1 c8 c2">URL_POOL = <code><em>eth-eu.dwarfpool.com</em></code></span></strong></li>
 	<li class="c10 c25 c24"><strong><span class="c1 c8 c2">PORT_POOL = <code><em>8008</em></code></span></strong></li>
</ul>
<p class="c14 c17" style="text-align: center"><strong><span class="c1 c8">OU</span></strong></p>

<ol class="c5 lst-kix_1ay95vhio7lk-0 start" start="1">
 	<li class="c10 c11"><span class="c1">Installer Qt-Miner (qui contient  Stratum-Proxy, donc également plus efficace de 10 à 20% selon eux) et le paramétrer </span><span class="c1 c8"><strong>comme décrit dans le paragraphe dédié à la présentation du logiciel</strong>. </span></li>
 	<li class="c10 c11"><span class="c1">Utiliser les paramètres suivants pour créer ton fichier .bat :</span></li>
</ol>
<ul>
 	<li class="c10 c25 c24"><strong><span class="c1 c8 c2">URL_POOL = <code><em>eth-eu.dwarfpool.com</em></code></span></strong></li>
 	<li class="c10 c25 c24"><strong><span class="c1 c8 c2">PORT_POOL = <code><em>8008</em></code></span></strong></li>
</ul>
<p class="c14 c17" style="text-align: center"><strong><span class="c1 c8">OU</span></strong></p>

<ol class="c5 lst-kix_rwp4v0ww4ifj-0 start" start="1">
 	<li class="c10 c11">Installer CUDA Miner et le paramétrer avec la config pour miner <strong>sans</strong> Stratum-Proxy, <strong>comme décrit dans le paragraphe dédié à la présentation du logiciel.</strong></li>
 	<li class="c10 c11"><span class="c1">Utiliser les paramètres suivants pour créer ton fichier .bat :</span></li>
</ol>
<ul>
 	<li class="c10 c25 c24"><strong><span class="c1 c8 c2">URL_POOL = <code><em>eth-eu.dwarfpool.com</em></code></span></strong></li>
 	<li class="c10 c25 c24"><strong><span class="c1 c8 c2">PORT_POOL = <code><em>80</em></code></span></strong></li>
</ul>
&nbsp;
<h3 class="c10"><span class="c3 c1">Exemples</span></h3>
<p class="c10"><span class="c1">Commande passe-partout avec CUDA Miner :</span></p>

<pre class="c14"><span class="c7 c1">cmd /K “start /B ethminer.exe </span><span class="c6 c1">-G</span><span class="c7 c1"> -S http://</span><span class="c1 c15">eth-eu.dwarfpool.com</span><span class="c7 c1">:8080 -O 0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64</span><span class="c7 c1">.WORKWELL”
</span><span class="c7 c1">pause</span></pre>
<p class="c14"><span class="c1">Ou sans Stratum-Proxy :</span></p>

<pre class="c14"><span class="c7 c1">cmd /K “start /B ethminer.exe </span><span class="c6 c1">-G</span><span class="c7 c1"> -F http://</span><span class="c1 c15">eth-eu.dwarfpool.com:80</span><span class="c7 c1">/0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64</span><span class="c7 c1">/WORKWELL”
</span><span class="c7 c1">pause</span></pre>
<p class="c14"><span class="c1">Ou lorsque l’on a installé Qt-Miner au lieu de CUDA Miner :</span></p>

<pre class="c14"><span class="c7 c1">cmd /K “start /B qtminer.exe -s http://</span><span class="c1 c15">eth-eu.dwarfpool.com</span><span class="c7 c1">:8080 -u 0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64.WWORKWELL -G”
</span><span class="c7 c1">pause</span></pre>
<p class="c10"><span class="c1">Commande pour carte Nvidia avec CUDA Miner :</span></p>

<pre class="c14"><span class="c7 c1">cmd /K “start /B ethminer.exe </span><span class="c6 c1">-U</span><span class="c7 c1"> -S http://</span><span class="c1 c15">eth-eu.dwarfpool.com</span><span class="c7 c1">:8080 -O 0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64</span><span class="c7 c1">.WORKNVIDIA”
</span><span class="c7 c1">pause</span></pre>
<p class="c14"><span class="c1">Ou sans Stratum-Proxy :</span></p>

<pre class="c14"><span class="c7 c1">cmd /K “start /B ethminer.exe </span><span class="c6 c1">-U </span><span class="c7 c1">-F http://</span><span class="c1 c15">eth-eu.dwarfpool.com:80</span><span class="c7 c1">/0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64</span><span class="c7 c1">/WORKWELL”
</span><span class="c7 c1">pause</span></pre>
<p class="c10"><span class="c1">Commande pour carte graphique sur PC portable avec CUDA Miner :</span></p>

<pre class="c14"><span class="c7 c1">cmd /K “start /B ethminer.exe -G -S http://</span><span class="c1 c15">eth-eu.dwarfpool.com</span><span class="c7 c1">:8080 -O 0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64</span><span class="c7 c1">.WORKLAPTOP </span><span class="c6 c1">--opencl-platform 1</span><span class="c7 c1">”
</span><span class="c7 c1">pause</span></pre>
<p class="c14"><span class="c1">Ou sans Stratum-Proxy :</span></p>

<pre class="c14"><span class="c7 c1">cmd /K “start /B ethminer.exe -U -F http://</span><span class="c1 c15">eth-eu.dwarfpool.com:80</span><span class="c7 c1">/0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64</span><span class="c7 c1">/WORKWELL </span><span class="c6 c1">--opencl-platform 1</span><span class="c7 c1">”
</span><span class="c7 c1">pause</span></pre>
<p class="c14"><span class="c1">Ou lorsque l’on a installé Qt-Miner au lieu de CUDA Miner :</span></p>

<pre class="c14"><span class="c7 c1">cmd /K “start /B qtminer.exe -s http://</span><span class="c1 c15">eth-eu.dwarfpool.com</span><span class="c7 c1">:8080 -u 0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64.WORKWELL -G </span><span class="c6 c1">--opencl-platform 1</span><span class="c7 c1">”
</span><span class="c7 c1">pause</span></pre>
<p class="c21 c28" style="text-align: center"><strong><span class="c6 c1">N’OUBLIEZ PAS DE METTRE VOTRE PROPRE WALLET A LA PLACE DU MIEN</span></strong></p>
<p class="c10"><span class="c1">Pour voir ses stats, attendre 30 min maximum, et aller à l’adresse :</span></p>
<p class="c21 c28" style="text-align: center"><span class="c1 c15">http://dwarfpool.com/eth/address?wallet=</span><em><strong><span class="c1 c2">VOTRE</span><span class="c1 c2">_WALLET</span></strong></em></p>
&nbsp;
<h2 class="c21 c28">Ethermine</h2>
<p class="c10" style="text-align: center"><span class="c3 c1 c20"><a class="c19" href="http://ethermine.org/" target="_blank">http://ethermine.org/</a></span><span class="c1"> </span></p>
<p class="c10"><span class="c1">La Ethermine c’est une bonne pool. Elle est directement issue de Ethpool.org qui est techniquement très au point. La seule chose qui change est le mode de paiement, calqué sur ce que fait la Dwarfpool par exemple. Il est possible de paramétrer dans account settings la fréquence de transfert de l’ether que l’on réalise avec la pool (Payment threshold in Ether). Attention par contre, il y a des commissions sur les payout si votre seuil est inférieur à 1 Ether.</span></p>
<p class="c10"><span class="c1">Le minage est anonyme (pas de compte à créer). </span></p>
<p class="c10"><span class="c1">J’aime bien leur page de statistiques. Attention, le Hashrate est pas juste les 60 premières minutes (ils font une moyenne sur les partages reçus). Ils mettent aussi une moyenne sur 24h glissantes.</span></p>

<h3 class="c10"><span class="c1">Pour miner sur Ethermine</span></h3>
<ol class="c5 lst-kix_xzglo5zh34jh-0 start" start="1">
 	<li class="c10 c11"><span class="c1">Installer CUDA Miner et le paramétrer avec la config pour miner <strong>avec</strong> Stratum-Proxy, </span><span class="c1 c8"><strong>comme décrit dans le paragraphe dédié à la présentation du logiciel</strong>. </span></li>
 	<li class="c10 c11"><span class="c1">Utiliser les paramètres suivants pour créer ton fichier .bat :</span></li>
</ol>
<ul>
 	<li class="c10 c25 c24"><strong><span class="c1 c8 c2">URL_POOL = <code>eu1.ethermine.org</code></span></strong></li>
 	<li class="c10 c25 c24"><strong><span class="c1 c8 c2">PORT_POOL = <code>4444</code></span></strong></li>
</ul>
<p class="c14 c17" style="text-align: center"><strong><span class="c1 c8">OU</span></strong></p>

<ol class="c5 lst-kix_yp17zwwwpdsu-0 start" start="1">
 	<li class="c10 c11"><span class="c1">Installer Qt-Miner (qui contient  Stratum-Proxy) et le paramétrer </span><span class="c1 c8"><strong>comme décrit dans le paragraphe dédié à la présentation du logiciel</strong>. </span></li>
 	<li class="c10 c11"><span class="c1">Utiliser les paramètres suivants pour créer ton fichier .bat :</span></li>
</ol>
<ul>
 	<li class="c10 c25 c24"><strong><span class="c1 c8 c2">URL_POOL = <strong><span class="c1 c8 c2"><code>eu1.ethermine.org</code></span></strong></span></strong></li>
 	<li class="c10 c25 c24"><strong><span class="c1 c8 c2">PORT_POOL = <strong><span class="c1 c8 c2"><code>4444</code></span></strong></span></strong></li>
</ul>
<p class="c21"><span class="c1">Ils conseillent </span><span class="c1 c8">de <strong>ne pas miner sans Stratum-Proxy</strong></span><span class="c1">.</span></p>
<p class="c10"><span class="c3 c1">Exemples :</span></p>
<p class="c10"><span class="c1">Commande passe-partout avec CUDA Miner :</span></p>

<pre class="c14"><span class="c7 c1">cmd /K “start /B ethminer.exe </span><span class="c6 c1">-G</span><span class="c7 c1"> -S http://eu1.ethermine.org:4444 -O 0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64</span><span class="c7 c1">.WORKWELL”
p</span><span class="c7 c1">ause</span></pre>
<p class="c14"><span class="c1">Ou lorsque l’on a installé Qt-Miner au lieu de CUDA Miner :</span></p>

<pre class="c14"><span class="c7 c1">cmd /K “start /B qtminer.exe -s http://eu1.ethermine.org:4444 -u 0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64.OkkohAMD -G”
</span><span class="c7 c1">pause</span></pre>
<p class="c10"><span class="c1">Commande pour carte Nvidia avec CUDA Miner :</span></p>

<pre class="c14"><span class="c7 c1">cmd /K “start /B ethminer.exe </span><span class="c6 c1">-U</span><span class="c7 c1"> -S http://eu1.ethermine.org:4444 -O 0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64</span><span class="c7 c1">.WORKNVIDIA”
</span><span class="c7 c1">pause</span></pre>
<p class="c10"><span class="c1">Commande pour carte graphique sur PC portable avec CUDA Miner :</span></p>

<pre class="c14"><span class="c7 c1">cmd /K “start /B ethminer.exe -G -S http://eu1.ethermine.org:4444 -O 0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64</span><span class="c7 c1">.WORKLAPTOP </span><span class="c6 c1">--opencl-platform 1</span><span class="c7 c1">”
</span><span class="c7 c1">pause</span></pre>
<p class="c14"><span class="c1">Ou lorsque l’on a installé Qt-Miner au lieu de CUDA Miner :</span></p>

<pre class="c14"><span class="c7 c1">cmd /K “start /B qtminer.exe -s http://eu1.ethermine.org:4444 -u 0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64.OkkohAMD -G </span><span class="c6 c1">--opencl-platform 1</span><span class="c7 c1">”
</span><span class="c7 c1">pause</span></pre>
<p class="c21 c28" style="text-align: center"><strong><span class="c6 c1">N’OUBLIEZ PAS DE METTRE VOTRE PROPRE WALLET A LA PLACE DU MIEN</span></strong></p>
<p class="c10"><span class="c1">Pour voir ses stats, attendre 30 min, et aller à l’adresse :</span></p>
<p class="c21 c28" style="text-align: center"><span class="c1 c15">http://ethermine.org/miners/</span><em><strong><span class="c1 c2">VOTRE</span><span class="c1 c2">_WALLET</span></strong></em></p>
&nbsp;
<h2 class="c21 c28" style="text-align: left"><span class="c13">Nanopool</span></h2>
<p class="c10" style="text-align: center"><span class="c3 c1 c20"><a class="c19" href="http://nanopool.org/" target="_blank">http://nanopool.org/</a></span><span class="c1"> </span></p>
<p class="c10"><span class="c1">Cette pool paie 4 fois par jours, avec un minimum de 100 Finney par paiement ( 0.1 Ether). Il y a 0.5 Finney de commission (0.0005 Ether) par payout.</span></p>
<p class="c10"><span class="c1">Le minage est anonyme (pas de compte à créer). </span></p>
<p class="c10"><span class="c1">Ils recommandent de ne pas miner chez eux si vous n’avez pas un hashrate d’au moins 5 Mh/s.</span></p>
<p class="c10"><span class="c1">Enfin, ils ne précisent pas s’il est avisé de miner chez eux avec Qt-Miner. Ça marche certainement, après est-ce que c’est optimisé, je ne saurais dire.</span></p>

<h3 class="c10"><span class="c1">Pour miner sur Nanopool</span></h3>
<ol class="c5 lst-kix_8fih5ss5uhpm-0 start" start="1">
 	<li class="c10 c11"><span class="c1">Installer CUDA Miner et le paramétrer avec la config pour miner <strong>avec</strong> Stratum-Proxy, </span><span class="c1 c8">c<strong>omme décrit dans le paragraphe dédié à la présentation du logiciel</strong>. </span></li>
 	<li class="c10 c11"><span class="c1">Utiliser les paramètres suivants pour créer ton fichier .bat :</span></li>
</ol>
<ul>
 	<li class="c10 c25 c24"><strong><span class="c1 c8 c2">URL_POOL = </span><code><span class="c26 c8 c2">eth-eu1.nanopool.org</span></code><span class="c1"><code> </code>OU </span><code><span class="c26 c8 c2">eth-eu2.nanopool.org</span></code></strong></li>
 	<li class="c10 c25 c24"><strong><span class="c1 c8 c2">PORT_POOL = <code>9999</code></span></strong></li>
</ul>
<p class="c14 c17" style="text-align: center"><strong><span class="c1 c8">OU</span></strong></p>

<ol class="c5 lst-kix_rkf5miihmx40-0 start" start="1">
 	<li class="c10 c11">Installer CUDA Miner et le paramétrer avec la config pour miner <strong>sans</strong> Stratum-Proxy, <strong>comme décrit dans le paragraphe dédié à la présentation du logiciel.</strong></li>
 	<li class="c10 c11"><span class="c1">Utiliser les paramètres suivants pour créer ton fichier .bat :</span></li>
</ol>
<ul>
 	<li class="c10 c25 c24"><strong><span class="c1 c8 c2">URL_POOL = <code><span class="c26 c8 c2">eth-</span></code></span><code><span class="c26 c8 c2">eu1.nanopool.org</span></code><span class="c1"><code> </code>OU <code><span class="c26 c8 c2">eth-</span></code></span><code><span class="c26 c8 c2">eu2.nanopool.org</span></code></strong></li>
 	<li class="c10 c25 c24"><strong><span class="c1 c8 c2">PORT_POOL = <code>8888</code></span></strong></li>
</ul>
<h3 class="c10"><span class="c3 c1">Exemples</span></h3>
<p class="c10"><span class="c1">Commande passe-partout avec CUDA Miner :</span></p>

<pre class="c14"><span class="c7 c1">cmd /K “start /B ethminer.exe </span><span class="c6 c1">-G</span><span class="c7 c1"> -S http://</span><span class="c7 c26">eu1.nanopool.org:9999</span><span class="c7 c1"> -O 0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64</span><span class="c1 c7">.WORKWELL”
p</span><span class="c7 c1">ause</span></pre>
<p class="c14"><span class="c1">Ou sans Stratum-Proxy :</span></p>

<pre class="c14"><span class="c7 c1">cmd /K “start /B ethminer.exe </span><span class="c6 c1">-G</span><span class="c7 c1"> -F http://</span><span class="c7 c26">eu1.nanopool.org:</span><span class="c7 c26">8888</span><span class="c7 c1">/0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64</span><span class="c7 c1">/WORKWELL”
</span><span class="c7 c1">pause</span></pre>
<p class="c10"><span class="c1">Commande pour carte Nvidia avec CUDA Miner :</span></p>

<pre class="c14"><span class="c7 c1">cmd /K “start /B ethminer.exe </span><span class="c6 c1">-U</span><span class="c7 c1"> -S http://</span><span class="c7 c26">eu1.nanopool.org:9999</span><span class="c7 c1"> -O 0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64</span><span class="c7 c1">.WORKNVIDIA”
</span><span class="c7 c1">pause</span></pre>
<p class="c14"><span class="c1">Ou sans Stratum-Proxy :</span></p>

<pre class="c14"><span class="c7 c1">cmd /K “start /B ethminer.exe </span><span class="c6 c1">-U </span><span class="c7 c1">-F http://</span><span class="c7 c26">eu1.nanopool.org:</span><span class="c7 c26">8888</span><span class="c7 c1">/0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64</span><span class="c7 c1">/WORKWELL”
</span><span class="c7 c1">pause</span></pre>
<p class="c10"><span class="c1">Commande pour carte graphique sur PC portable avec CUDA Miner :</span></p>

<pre class="c14"><span class="c7 c1">cmd /K “start /B ethminer.exe -G -S http://</span><span class="c7 c26">eu1.nanopool.org:9999</span><span class="c7 c1"> -O 0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64</span><span class="c7 c1">.WORKLAPTOP </span><span class="c6 c1">--opencl-platform 1</span><span class="c7 c1">”
</span><span class="c7 c1">pause</span></pre>
<p class="c14"><span class="c1">Ou sans Stratum-Proxy :</span></p>

<pre class="c14"><span class="c7 c1">cmd /K “start /B ethminer.exe -U -F http://</span><span class="c7 c26">eu1.nanopool.org:</span><span class="c7 c26">8888</span><span class="c7 c1">/0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64</span><span class="c7 c1">/WORKWELL </span><span class="c6 c1">--opencl-platform 1</span><span class="c7 c1">”
</span><span class="c7 c1">pause</span></pre>
<p class="c21 c28" style="text-align: center"><strong><span class="c6 c1">N’OUBLIEZ PAS DE METTRE VOTRE PROPRE WALLET A LA PLACE DU MIEN</span></strong></p>
<p class="c10"><span class="c1">Pour voir ses stats, attendre 30 min, et aller à l’adresse :</span></p>
<p class="c21 c28" style="text-align: center"><span class="c1 c15">http://eth.nanopool.org/account/</span><strong><em><span class="c1 c2">VOTRE</span><span class="c1 c2">_WALLET</span></em></strong></p>
&nbsp;
<h2 class="c21 c28" style="text-align: left"><span class="c13">Coinotron</span></h2>
<p class="c10 c32" style="text-align: center"><span class="c3 c1 c20"><a class="c19" href="https://www.coinotron.com/app?action=home" target="_blank">https://www.coinotron.com/app?action=home</a></span><span class="c1"> </span></p>
<p class="c10"><span class="c1">Voilà une pool qui nécessite de s’enregistrer avant de démarrer. Attention, la pool prélève 0.01 ETH pour les paiements inférieurs à 1 ETH</span></p>
<p class="c10"><span class="c1">Ils recommandent d’utiliser CUDA Miner.</span></p>

<h3 class="c10"><span class="c1">Pour miner sur Coinotron</span></h3>
<ol class="c5 lst-kix_8fih5ss5uhpm-0" start="3">
 	<li class="c10 c11"><span class="c1">Installer CUDA Miner et le paramétrer avec la config pour miner <strong>avec</strong> Stratum-Proxy, </span><span class="c1 c8"><strong>comme décrit dans le paragraphe dédié à la présentation du logiciel</strong>. </span></li>
 	<li class="c10 c11"><span class="c1">Utilise les paramètres suivants pour créer ton fichier .bat :</span></li>
</ol>
<ul>
 	<li class="c10 c24 c25"><strong><span class="c1 c8 c2">URL_POOL</span><span class="c26 c8 c2"> = </span><code><span class="c26 c8 c2">coinotron.com</span></code></strong></li>
 	<li class="c10 c25 c24"><strong><span class="c1 c8 c2">PORT_POOL = <code>3344</code></span></strong></li>
</ul>
<p class="c21 c39"><span class="c1 c8">Attention, les liens à insérer sont un peu différents chez eux (mais ils l’expliquent bien </span><span class="c3 c1 c20 c8"><a class="c19" href="https://www.google.com/url?q=https://www.coinotron.com/app?action%3Dhelp&amp;sa=D&amp;ust=1460027167920000&amp;usg=AFQjCNHmdCeQkIXYuXWRsuS-qj9rOnw4LA">sur leur page d’aide</a></span><span class="c1 c8">) :</span></p>

<pre><span class="c7 c1">cmd /K “start /B ethminer.exe </span><span class="c6 c1">-G</span><span class="c7 c1"> -S </span><span class="c7 c26 c46">coinotron.com:3344</span><span class="c7 c1"> -O </span><span class="c1 c2 c18">USERNAME</span><span class="c7 c1">.</span><span class="c1 c2 c18">WORKERNAME</span><span class="c7 c1">:</span><span class="c1 c2 c18">WORKERPASSWORD</span><span class="c7 c1">”
</span><span class="c7 c1">pause
</span></pre>
&nbsp;
<h2><span class="c13">Coinmine</span></h2>
<p class="c10" style="text-align: center"><span class="c3 c1 c20"><a class="c19" href="https://www2.coinmine.pl/eth/" target="_blank">https://www2.coinmine.pl/eth/</a></span></p>
<p class="c10"><span class="c1">Encore une pool qui nécessite de s’enregistrer. Je ne vais pas m’attarder sur celle-ci, elle explique bien les démarches à suivre </span><span class="c3 c1 c20"><a class="c19" href="https://www2.coinmine.pl/eth/index.php?page=gettingstarted" target="_blank">sur sa page d’aide</a></span><span class="c1">. Elle propose même en téléchargement les logiciels pré-configurés. Trop simple !</span></p>
&nbsp;
<h2 class="c10"><span class="c13">Suprnova</span></h2>
<p class="c10 c32" style="text-align: center"><span class="c3 c1 c20"><a class="c19" href="https://eth.suprnova.cc" target="_blank">https://eth.suprnova.cc</a></span><span class="c3 c1 c20">/ </span></p>
<p class="c10"><span class="c1">Pour finir, encore une pool qui nécessite de s’enregistrer. Elle ressemble grandement à Coinmine. Je ne vais donc pas plus m’attarder sur celle-ci, voyez </span><span class="c3 c1 c20"><a class="c19" href="https://eth.suprnova.cc/index.php?page=gettingstarted" target="_blank">sur sa page d’aide</a></span><span class="c1">. Elle aussi propose en téléchargement les logiciels pré-configurés.</span></p>
&nbsp;
<h1 class="c10"><span class="c13">Quelques combines pour maximaliser son Hashrate</span></h1>
<h2>Petites astuces simples</h2>
<p class="c10"><span class="c1">Si vous avez le sentiment d’être lésé niveau Hashrate, vous pouvez toujours :</span></p>

<ul class="c5 lst-kix_u2quv95w90zx-0 start">
 	<li class="c10 c11"><span class="c1">Vérifier que vous n’avez pas un mauvais pilote graphique (voir en préambule du paragraphe des logiciels)</span></li>
 	<li class="c10 c11"><span class="c1">insérer ces quelques commandes au tout début de votre fichier .bat (si vous avez une carte graphique AMD) :</span></li>
</ul>
<pre class="c10"><span class="c7 c1">setx GPU_FORCE_64BIT_PTR 0
</span><span class="c7 c1">setx GPU_MAX_HEAP_SIZE 100
</span>setx GPU_USE_SYNC_OBJECTS 1
setx GPU_MAX_ALLOC_PERCENT 100</pre>
Mettre 95 à cette dernière valeur si votre carte graphique n'a que 2GB de GDDR (Merci à gaznseb).
<ul class="c5 lst-kix_u2quv95w90zx-0">
 	<li class="c10 c11"><span class="c1">Rajouter l’option </span><code><span class="c7 c1">/affinity 0x1</span></code><span class="c1"> après </span><code><span class="c7 c1">start</span></code><span class="c1"> dans votre ligne de commande de votre fichier <strong><em>.bat</em></strong> . Cela va forcer à ce que le programme soit contrôlé par le second cœur de votre processeur, moins utilisé que le premier.</span></li>
</ul>
<h2>Exemple de script malin</h2>
Pour ceux qui ont à peu près compris l'esprit des commandes et qui veulent simplifier le redémarrage du miner après un arrêt, vous pouvez toujours faire un batch un peu plus solide. Pour ma part par exemple, j'ai fait ça (j'avoue, j'ai aussi fait un peu de cosmétique ^^):
<pre>@echo off

set exe=ethminer.exe
set arguments= -S eu1.ethermine.org:4444 -O 0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64.OkkohAMD -G --opencl-platform 1 --cl-local-work 256 --cl-global-work 16384
set duree_redem=1
set /a nb_redemarrages=0

cls
color 80
setx GPU_FORCE_64BIT_PTR 0
setx GPU_MAX_ALLOC_PERCENT 95
setx GPU_USE_SYNC_OBJECTS 1
setx GPU_MAX_HEAP_SIZE 100

:start
start /min /affinity 0x1 "Ethminer" %exe% %arguments%

:recom
set duree=9000

:prez
cls
echo                      .+` 
echo                     -omd.
echo                    :ssmNm-
echo                  `/sssmNNN/ 
echo                 <code>+ssssmNNNNs</code>'
echo                .osssssmNNNNNh. 
echo               :sssssssmNNNNNNd-
echo             `/ssssssssmNNNNNNNm/
echo            `+ssssssssyNNNNNNNNNNo' 
echo           .ossssyhdmNNMMMMMMNNNNNy' 
echo          -syyhdmNNNNNNMMMMMMMMMMNNd- 
echo         :hmNNNNNNNNNNNMMMMMMMMMMMMMd.
echo         `-ohmNNNNNNNNNMMMMMMMMMMmy/- 
echo          ::.-/sdNNNNNNMMMMMMNds::/s: 
echo           -oo/-.-ohmNNMMMmy+-:ohmh- 
echo            .+sso+:-./yhs:-/sdNNNo` 
echo              :osssoo/-:+hmNNNNd:
echo               .+ssssssdNNNNNNs` 
echo                `:sssssmNNNNm:
echo                  .osssmNNNy.
echo                   `/ssmNm/
echo                     -omh.
echo                       `:                                       Script by Okkoh
echo ------------------------------------------------------------------------------
echo Le minage sous %exe% va durer encore %duree% secondes (redemarrage num. %nb_redemarrages%)
echo ------------------------------------------------------------------------------
set /a duree-=1
if %duree%==-1 goto redem
choice /C onr /N /T 1 /D n /M "O pour redemarrer le logiciel maintenant, R pour redemarrer le compteur"
if errorlevel ==3 goto recom
if errorlevel ==2 goto prez
if errorlevel ==1 goto redem
goto prez

:redem
taskkill /f /im %exe%
cls
echo:
echo Le logiciel redemarre dans %duree_redem% secondes
timeout %duree_redem%
set /a nb_redemarrages+=1
goto start</pre>
Sans trop détailler le tout, ce qu'il faut savoir c'est qu'il permet, toutes les 7200 secondes, d'arrêter mon miner et de le redémarrer 2 secondes plus tard. Si jamais il avait buggé / planté, je n'ai pas perdu l'après midi, mais maximum 2h. Et si je suis là, j'appuie sur O et il redémarre tout de suite. Ce code s'inspire d'un autre que vous trouverez ici : <a href="https://forum.ethereum.org/discussion/4507/anyway-to-automatically-restart-ethminer-when-it-crashes" target="_blank">https://forum.ethereum.org/discussion/4507/anyway-to-automatically-restart-ethminer-when-it-crashes</a>

Le batch peut être récupéré <a href="http://www.petit-fichier.fr/2016/07/12/ethermine-cuda-script-okkoh/" target="_blank">ici</a>.

<em>[Edit: Il y avait un petit bug dans le batch, la coquille est maintenant corrigée dans le texte et dans le fichier joint. J'ai également rajouté la possibilité de relancer le compte à rebours depuis sa valeur initiale.]</em>

&nbsp;
<p style="text-align: center"><em>Voilà, n'hésitez pas à me dire si ce tuto vous a plus et vous a aidé. </em></p>
<p style="text-align: center"><em>Et si vous remarquez des coquilles, dites le moi discrètement ;)</em></p>