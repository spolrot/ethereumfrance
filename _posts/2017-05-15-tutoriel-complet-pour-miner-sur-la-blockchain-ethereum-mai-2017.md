---
ID: 2190
post_title: 'Tutoriel complet pour miner sur la blockchain Ethereum &#8211; mai 2017'
author: Okkoh
post_excerpt: ""
layout: post
permalink: >
  https://www.ethereum-france.com/tutoriel-complet-pour-miner-sur-la-blockchain-ethereum-mai-2017/
published: true
post_date: 2017-05-15 09:30:06
---
<h1><strong>Introduction</strong></h1>
Le minage d’Ethereum a pas mal évolué en peu de temps, et il y a eu beaucoup de questions dans les commentaires sur les précédents tutos. Si je fais l’effort de répondre le plus rapidement et le plus souvent possible, force est de constater que souvent les mêmes questions reviennent. J’ai donc rédigé un nouvel article pour tenter de répondre à un maximum de questions, sur le matériel, sur les manières de miner, sur la rentabilité. Cet article propose également un tuto pour utiliser un logiciel aujourd’hui fréquemment utilisé sous Windows. Afin de ne pas écrire une encyclopédie, seule cette méthode pour miner sera expliquée, ainsi que son utilisation sur 3 pools. Il est possible de miner avec d’autres logiciels, de manière différente, mais les pools l’expliquent presque tous très bien, et un mauvais niveau d’anglais suffit à comprendre quoi faire.

Comme dans mon tuto précédent, je ne parlerai que du minage dans un « pool » qui permet de mutualiser la puissance de calcul de plusieurs personnes pour mutualiser les moyens de minages. La difficulté est aujourd’hui telle qu’il me paraît illusoire de vouloir miner tout seul avec ses quelques gros GPU.

Notez que mon ancien tuto « complet » reste assez valable, il faut juste bien vérifier si les pools n’ont pas changé leurs adresses de serveurs. Parfois elles ne permettent plus non plus de miner sans Stratum-proxy.

Enfin, quelques mots de vocabulaire pour rappel :
<ul>
 	<li>Fork = Logiciel modifié</li>
 	<li>Pool = équipe de minage</li>
 	<li>Wallet = un portefeuille qui stocke vos ethers</li>
 	<li>Worker/Rig = machine qui mine (le plus souvent, votre PC)</li>
</ul>
<h1><strong>Wallet</strong></h1>
Pour miner de l’ether (ETH) en participant à la blockchain Ethereum, vous avez besoin d’un wallet sur lequel envoyer vos ether (de type 0xD95DC4cf508fDDC10870...). Si vous n’en avez pas encore, vous pouvez aller le <span style="text-decoration: underline"><a href="https://www.google.com/url?q=http://www.ethereum-france.com/creer-et-gerer-son-portefeuille-dether-en-2-minutes-avec-myetherwallet-com/&amp;sa=D&amp;ust=1460027167751000&amp;usg=AFQjCNGkP4Svg-lOydOBuauSSBjC2FK11g">créer ici</a></span>.

Une fois votre wallet créé, vous n’êtes pas obligé de retourner sur le site du wallet pour connaitre votre solde et vos transactions, vous pouvez aller tout consulter sur des sites explorateurs de la blockchain, comme par exemple : <span style="text-decoration: underline"><a href="https://etherchain.org/">https://etherchain.org/</a></span> ou <span style="text-decoration: underline"><a href="https://etherscan.io/">https://etherscan.io/</a></span>. Dans l’outil de recherche, en haut à droite de ces sites, vous collez votre adresse de wallet et vous accéder à toutes les infos : solde, transactions.
<h1><strong>Avertissements préalables et aperçu rapide des risques financiers</strong></h1>
Je préfère vous prévenir tout de suite : miner sur Ethereum est devenu incroyablement dur en moins de 2 ans. Quand j’ai commencé à miner il y a 1 an, je n’avais qu’une GTX970 et il ne me fallait que 3 jours pour cumuler 1ETH. Maintenant j’ai une GTX970, une R9 290 et une RX480 et un hashrate de 71.5MH/s. J’ai observé récemment :
<ul>
 	<li>à la date du 18/03/2017, <strong>j’obtenais environ 0.1 ETH en 1 journée</strong>, soit 10 jours pour atteindre 1ETH</li>
 	<li>à la date d’aujourd’hui (12/05/2017), <strong>j’obtiens environ 0.085 ETH en 1 journée</strong>, soit 12 jours pour atteindre 1ETH.</li>
</ul>
Depuis la flambée récente du cours, plein de gens se découvrent mineurs et plein de gros mineurs ont réinvestit. Or plus il y a de machines qui minent, plus c’est dur de miner donc moins l’on gagne d’ether pour ce que l’on participe. Faites bien votre calcul avant de vous lancer, il existe bien évidemment un risque financier et ça n’est pas moi qui serait responsable de vos pertes financières s’il devait y en avoir !

Petit exemple de calcul volontairement simpliste pour vous permettre de mieux cerner la problématique :
<ul>
 	<li>Un Rig avec 6 RX480 (je vous donne quelques conseils pour construire une telle machine tout à la fin de mon article), c’est environ <strong>2000€</strong> pour 0.195ETH/jour, environ 71 ETH/an sans tenir compte du fait que la difficulté augmente ce qui est une hypothèse assez mauvaise (vous aurez moins d'ether en réalité car la difficulté augmente tous les jours),</li>
 	<li>La consommation électrique d’un tel engin, c’est 1000W. Donc 1000W*24h*365j*0.1449€/kWh≈<strong>1300€/an</strong>,</li>
 	<li>En prenant pour hypothèse que vous ne vendrez vos Ether que dans 1 an (pour un peu spéculer sur un cours à la hausse !) et en prenant un taux de change de 82€/ETH à ce moment-là, vous en obtiendrez <strong>5822€</strong>.</li>
</ul>
Si la valeur de l’ether ne bouge pas trop en un an, vous voyez avec ce calcul simpliste que votre matériel ne sera rentabilisé au mieux qu’après 200 jours environ. Si la valeur de l’ether grimpe, évidemment vous êtes gagnant plus rapidement. Par contre, et c’est là-dessus que j’attire votre attention, si la valeur chute (ce qui peut évidemment arriver vu la montée extrêmement brutale du cours ces derniers mois), <strong><u>vous risquez de vous retrouver avec de gros frais d’électricité restant à votre charge.</u></strong>

Enfin, n’oubliez pas qu’à un moment donné <strong>Ethereum passera d'un système de validation</strong><a href="https://fr.wikipedia.org/wiki/Preuve_de_travail"><strong> Proof of Work</strong></a><strong> à un système</strong><strong> <a href="https://fr.wikipedia.org/wiki/Preuve_d%27enjeu">Proof of Stake</a></strong>, ce qui signifiera que l’on ne pourra plus miner avec nos GPU. A ma connaissance cette modification majeure du fonctionnement de la blockchain n’est pas encore défini, mais l’équipe travaille dessus. Lorsque cela se produira, tout le monde se rabattra sur des blockchains différentes. Bien que d’autres blockchains semblent très attractives, n’oubliez pas non plus que la migration massive de mineurs vers ces autres blockchains vont faire exploser leurs difficultés de minage (donc vous gagnerez moins que ce que l’on gagne actuellement en les minant).

[caption id="attachment_2207" align="alignright" width="169"]<img class="wp-image-2207 size-medium" src="https://www.ethereum-france.com/wp-content/uploads/2017/05/Minage-169x300.jpg" alt="" width="169" height="300" /> Un mineur Ethereum, monté par un lecteur du site (merci Guillaume !)[/caption]
<h1><strong>Matériel pour miner</strong></h1>
Pour miner sur Ethereum il faut un ordinateur doté d’une carte graphique assez puissante et (actuellement) de 3Go minimum de mémoire vidéo. Il peut être important, si l’on se soucie de ses finances et que l’on paie son électricité, de choisir un matériel qui soit un minimum efficient (calcule vite mais consomme peu d’électricité). Moi je n’ai aucun ami qui travaille chez EDF, snif…

Et pourquoi donc 3Go de mémoire vive embarquée me direz-vous ? En réalité, la mémoire vidéo est nécessaire pour charger un fichier nommé <span style="text-decoration: underline"><a href="https://github.com/ethereum/wiki/wiki/Ethash-DAG">DAG</a></span> qui va permettre de faire les calculs. Et ce fichier est actuellement supérieur à 2Go et grossit petit à petit selon une règle définie à l’avance. La prévision de son évolution de taille est la suivante :
<p style="text-align: center">La limite de 2GB a été dépassée à la  mi-décembre 2016
La limite de 3GB sera dépassée à la mi-Avril 2018
La limite de 4GB sera dépassée à la mi-septembre 2019</p>
<p style="text-align: center"><strong>Si votre carte graphique n’a pas assez de mémoire vidéo pour charger le fichier DAG, vous ne pourrez pas miner avec celle-ci.</strong></p>
Attention ! Sachez que toutes les cartes graphiques ne sont pas égales. Les vielles cartes genre GTX6xx, 7xx, AMD R7, etc sont plutôt dépassées : vous ne minerez pas très vite et consommerez pas mal de courant (chic, ça chauffe l’appart en hiver !). Les R9, genre R9 290 ou R9 390 sont valables niveau hashrate, mais elles consomment beaucoup d’électricité et chauffent beaucoup. Actuellement, je trouve que les RX470 et 480 sont un bon compromis, d’autant que leur prix devrait prochainement baisser avec l’apparition des RX5xx. Les GTX1070 sont performantes, mais à choisir et à l’heure d’écrire cet article, je préfère 2 RX480 pour le prix d’une GTX1070. En règle générale, plus la carte est récente, plus elle est efficiente. Mais attention, c’est rarement les modèles très hauts de gamme qui sont les meilleurs à ce jeu, car un peu gonflées et du coup gourmandes en électricité. Elles sont même parfois super mauvaises, comme la GTX1080 (aux dernières nouvelles, la mémoire GDDR5x qu'elle embarque n'est pas très bonne pour miner).

Bref, vous seul êtes maître de votre budget et de votre objectif : choisissez des cartes efficientes pour être rentable rapidement et pouvoir mettre à jour son matériel fréquemment, quitte à tout abandonner et ne pas perdre grand-chose si le cours de l’ether se casse la figure. Investissez toutes vos économies pour avoir le hashrate le plus élevé possible et gagner rapidement le plus d’ether possible si vous faites le pari que son cours grimpera encore longtemps et qu’à terme, ce gros investissement sera largement rentable.

Je vous mets quelques liens vers des outils pour que vous puissiez vous faire une opinion personnelle :
<ul>
 	<li>Vous pouvez voir quelques stats de hashrate de cartes graphiques ici : <span style="text-decoration: underline"><a href="http://62.212.74.86/~mining/list/nvidia/index.php?algo=eth">http://62.212.74.86/~mining/list/nvidia/index.php?algo=eth</a></span>.</li>
 	<li>Vous pouvez avoir une idée de rentabilité de votre matériel ici : <span style="text-decoration: underline"><a href="https://whattomine.com">https://whattomine.com</a></span> ou <span style="text-decoration: underline"><a href="https://www.cryptocompare.com/mining/#/equipment?f1=Ethash">https://www.cryptocompare.com/mining/#/equipment?f1=Ethash</a></span>. Attention, les sites proposent souvent un Hashrate élevé pour les cartes, je pense qu'ils partent du principe que vous avez complètement optimisé votre machine voire mis un custom BIOS sur votre GPU (ce qui vous fait perdre la garantie il me semble).</li>
 	<li>Si vous voulez calculer de manière précise la rentabilité de votre affaire c’est ici : <span style="text-decoration: underline"><a href="https://cryptowizzard.github.io/eth-mining-calculator/">https://cryptowizzard.github.io/eth-mining-calculator/</a></span></li>
</ul>
Pour finir, si ces mises en garde ne vous ont pas refroidi et que vous souhaitez toujours acquérir un outil dédié pour miner, vous trouverez quelques conseils dans le dernier paragraphe de cet article.
<h1><strong>Miner, partie logicielle</strong></h1>
Nous allons maintenant entrer dans le vif du sujet et présenter un logiciel qui va vous permettre d’entrer de plain-pied dans votre nouvelle activité d’ouvrier des temps modernes, mais avant cela quelques prérequis et conseils :
<ul>
 	<li>Pour les possesseurs de cartes <strong>AMD jusqu’à R9</strong>, <strong>n’utilisez pas les pilotes Catalyst 16.3</strong>, ils feront chuter votre Hashrate. Préférez les 15.11 que l’on peut trouver sur le site Guru3D par exemple.</li>
 	<li>Pour les possesseurs de <strong>AMD RX</strong>, prenez les 16.12.2, disponibles également sur le site de Guru3D.</li>
 	<li><strong>Désactivez le SLI/Crossfire</strong> pour pouvoir bénéficier de la puissance de chaque carte graphique, c’est plus intéressant.</li>
 	<li>Quel que soit le logiciel que vous utilisez, <strong>soyez patients,</strong> <strong>utilisez l’aide du programme </strong>avant de venir demander de l’aide.</li>
 	<li>Il existe des <strong>FAQ et des pages Help</strong> sur les sites de chaque pool. Utilisez de préférence ce qu’ils vous recommandent. Évidemment, c’est en anglais, mais si vous vous lancez dans le minage, il est préférable d’avoir quelques connaissances en anglais, en commandes MS-DOS et en dépatouillages et petits bidouillages de programmes.</li>
 	<li><strong>Miner sous Windows 10, c’est compliqué</strong>, surtout si vous avez une carte Nvidia.</li>
 	<li>Je propose ici de démarrer votre logiciel en passant par un fichier .bat, avec un tout petit peu de code <strong><em>cmd /K “start /B …”</em></strong>. Ça n’est pas obligatoire, on peut tout à fait mettre les attributs dans un raccourci, mais avec ma méthode vous pourrez lire les indications du logiciel si jamais vous avez tapé une erreur (par défaut la fenêtre se ferme et sauf si vous êtes un super sayan, vous n’aurez pas le temps de lire le message). De plus, vous pouvez rajouter d’autres choses à effectuer avant le lancement du programme (quelques lignes d’optimisation, lancer un minuteur,... ou autre chose qui vous passe par la tête). <strong>Attention, ce fichier .bat doit être dans le dossier du logiciel, et si cela ne vous convient pas il vous faut taper dans le fichier .bat toute l’arborescence pour atteindre votre fichier exécutable.</strong></li>
</ul>
<h2><strong>Claymore Dual Miner</strong></h2>
C’est le logiciel que j’utilise actuellement, dans sa version 7.4. Le nom complet c’est <strong>Claymore's Dual Ethereum + Decred/Siacoin/Lbry/Pascal AMD+NVIDIA GPU Miner</strong> (sic). Très stable, il peut s’utiliser indifféremment avec des cartes AMD et/ou NVIDIA. Il existe aussi une version un peu différente pour Zcash (mais pas de dual miner). On peut paramétrer tout un tas de choses et on peut même miner 2 blockchains en même temps (Ethereum + Decred ou SIA ou PASCAL ou Lbry). Evidemment, ça mine avec le reste de puissance disponible, donc ça ne mine pas non plus extrêmement fort. On peut régler l’intensité, mais si la valeur est trop forte, ça peut un peu réduire la vitesse de minage sur Ethereum.

Il y a un fichier Readme!!!.txt à lire pour connaitre tous les paramètres. Je vais en rappeler certains ici, mais ça évolue au fil des versions donc n'hésitez pas à aller vérifier ce qui y est mentionné! Je n'expliquerai pas non plus comment faire pour miner sur une 2ème blockchain (lire le readme pour comprendre comment ça marche).
<ol>
 	<li>Téléchargez et installez Claymore's Dual Ethereum + Decred/Siacoin/Lbry/Pascal AMD+NVIDIA GPU Miner :</li>
</ol>
<p style="text-align: center"><u>https://bitcointalk.org/index.php?topic=1433925.0 </u></p>

<ol start="2">
 	<li>Ouvrez le Bloc-Notes, et écrivez les lignes suivantes :</li>
</ol>
<pre>cmd /K “start /B EthDcrMiner64.exe -epool URL_POOL:PORT_POOL -ewal VOTRE_WALLET -eworker NOM_DU_WORKER -epsw x”
pause</pre>
Si vous voulez miner uniquement sur votre seconde carte, y compris pour un PC portable avec un combo carte intégré Intel + GPU AMD ou Nvidia :
<pre>cmd /K “start /B EthDcrMiner64.exe -epool URL_POOL:PORT_POOL -ewal VOTRE_WALLET -eworker NOM_DU_WORKER -epsw x -di 1”
pause</pre>
Evidemment, changez <em>URL_POOL</em>, <em>PORT_POOL</em> et <em>VOTRE_WALLET</em> (la mienne par exemple : 0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64) et ne mettez <em>-eworker NOM_DU_WORKER</em> que si ça vous est utile (si vous avez plusieurs workers et que voulez les nommer spécifiquement pour mieux les suivre). Les url et ports du pool désiré sont détaillés dans les paragraphes plus loin.
<ol start="3">
 	<li>Sauvez votre fichier en <em>.bat</em> <strong>dans le dossier du logiciel</strong> c’est-à-dire là où vous l’avez décompressé (Fichier &gt; Enregistrer sous -&gt; Nom “LAUNCH.bat”)</li>
 	<li>Lancez le logiciel en double-cliquant sur votre fichier LAUNCH.bat.</li>
</ol>
<h2><strong>Les options du logiciel</strong></h2>
Pour info, il y a des options possibles, à rajouter à la fin, mais tout ça dépend de votre matériel et de la configuration que vous voulez faire. J’en rappelle quelques-unes :
<table class=" aligncenter" style="width: 672.25px">
<tbody>
<tr>
<td style="width: 115px">
<pre><strong><em>-di x</em></strong></pre>
</td>
<td style="width: 809.25px;text-align: left">
<div>Index des GPU (si on ne met pas ce paramètre, le logiciel démarre avec tout ce qui peut miner). Permet de dire quels GPU minent.</div>
<div>Par exemple -di 023 va permettre de miner avec le 1<sup>er,</sup> le 3<sup>ème</sup> et le 4ème GPU (oui, 0=1 je sais c’est bizarre :))</div></td>
</tr>
<tr>
<td style="width: 115px">
<pre><strong><em>-esm x</em></strong></pre>
</td>
<td style="width: 809.25px;text-align: left">
<div>Mode Stratum (x=0 par défaut) :</div>
<div>0 eth-proxy mode (dwarpool.com, ethermine.org,…)</div>
<div>1 qtminer mode (ethpool.org)</div>
<div>2 miner-proxy mode (coinotron.com)</div>
<div>3 nicehash mode</div></td>
</tr>
<tr>
<td style="width: 115px">
<pre><strong><em>-etha x</em></strong></pre>
</td>
<td style="width: 809.25px;text-align: left">
<div>Type d’algorithme Ethereum à utiliser pour les cartes AMD (si on ne met pas ce paramètre, le logiciel détecte automatiquement la valeur)</div>
<div>0 optimisé pour les cartes performantes</div>
<div>1 optimisé pour les cartes à Hashrate bas</div>
<div>2 optimisé pour les pilotes Linux</div>
<div>On peut spécifier l’algorithme pour chaque carte en séparant par une virgule chaque valeur par exemple : -etha 0,0,1,1</div></td>
</tr>
<tr>
<td style="width: 115px">
<pre><strong><em>-ethi x</em></strong></pre>
</td>
<td style="width: 809.25px;text-align: left">
<div>Définit l’intensité pour le calcul (x=8 par défaut). On peut diminuer volontairement cette valeur si on souhaite pouvoir avoir en parallèle une activité de bureau ou si on a des problèmes de stabilité. La valeur la plus basse est « -ethi 0 ». Attention, par expérience on constate souvent que ça n’est pas parce que l’intensité est la plus haute que le Hashrate sera le meilleur.</div>
<div>On peut spécifier l’intensité pour chaque carte en séparant par une virgule chaque valeur par exemple : -ethi 7,7,8,8</div></td>
</tr>
<tr>
<td style="width: 115px">
<pre><strong><em>-eres x</em></strong></pre>
</td>
<td style="width: 809.25px;text-align: left">
<div>Ce paramètre est à mettre si votre miner crashe lors de changement d’Epoch. Lors d’une changement d’Epoch, le logiciel recharge le DAG dans la mémoire GPU. Mais ce nouveau DAG étant légèrement plus gros que l’ancien, et parfois ca crashe. Pour éviter ça, ce paramètre réserve la mémoire qui sera nécessaire pour le DAG qui sera chargé dans x Epoch (par défaut x=2).</div></td>
</tr>
<tr>
<td style="width: 115px">
<pre><strong><em>-li x</em></strong></pre>
</td>
<td style="width: 809.25px;text-align: left">
<div>Low intensity mode. Pour réduire l’intensité de calcul, histoire que ça chauffe moins ou que ça freeze moins (si vous voulez avoir une activité de bureau en même temps). -li 10 mine moins que -li 1 (0 par défaut)</div></td>
</tr>
<tr>
<td style="width: 115px">
<pre><strong>-nofee</strong></pre>
</td>
<td style="width: 809.25px;text-align: left">
<div>Enlève la « taxe » instaurée par le développeur pour se rémunérer, mais réduit de 4% environ le hashrate.</div></td>
</tr>
<tr>
<td style="width: 115px">
<pre><strong><em>-tt x</em></strong></pre>
</td>
<td style="width: 809.25px;text-align: left">
<div>Cible de température du GPU. -tt 80 signifie une température cible de 80°C pour le 1<sup>er</sup> GPU. -tt 70,80,75 par exemple s’utilise pour spécifier la température cible pour les 3 premiers GPU. -tt -50 (négatif donc) permet de fixer la vitesse des ventilateurs (en %), ici 50%. Par défaut, le logiciel est configuré sur -tt 1, qui permet juste d’avoir l’info sur la température du GPU et la vitesse des ventilos.</div>
<div>Attention, pour les cartes NVIDIA on ne peut que monitorer et pas gérer la température.</div></td>
</tr>
<tr>
<td style="width: 115px">
<pre><strong><em>-ttli x</em></strong></pre>
</td>
<td style="width: 809.25px;text-align: left">
<div>Baisse l’intensité du minage pour rester à la température x. -ttli 70,80,75 par exemple s’utilise pour que les 3 premiers GPU restent aux températures cibles (70°, 80° et 75°)</div></td>
</tr>
<tr>
<td style="width: 115px">
<pre><strong><em>-fanmax x</em></strong></pre>
</td>
<td style="width: 809.25px;text-align: left">
<div>Spécifie la vitesse max des ventilos (en %). -fanmax 80 signifie une vitesse max de 80%. On le spécifie également par GPU : -fanmax 70,80,75 par exemple</div>
<div>Non supporté avec NVIDIA</div></td>
</tr>
<tr>
<td style="width: 115px">
<pre><strong><em>-fanmin x</em></strong></pre>
</td>
<td style="width: 809.25px;text-align: left">
<div>Spécifie la vitesse min des ventilos (en %). -fanmin 30 signifie une vitesse min de 30%. On le spécifie également par GPU : -fanmin 40,50,40 par exemple</div>
<div>Non supporté avec NVIDIA</div></td>
</tr>
</tbody>
</table>
Il <span style="text-decoration: underline">existe d’autres options</span>, que je ne détaillerai pas ici, mais qui sont disponibles dans le fichier <strong>Readme!!!.txt</strong>
<h1><strong>Les pools et comment y participer</strong></h1>
Il est obligatoire aujourd'hui de rejoindre un pool pour miner, sauf si on a une énorme capacité de minage, mais vous ne liriez pas ce tuto dans ce cas. Un pool permet de répartir le travail. On ne mine pas en trouvant des blocs toutes les 30 secondes (il faut beaucoup beaucoup de puissance de calcul pour y arriver), mais des solutions qui contribuent à trouver un bloc. Le pool permet de séparer le travail en petites entités, et vous confie des calculs que votre matériel tente de résoudre. Si votre machine trouve une solution au calcul suffisamment vite, elle la partage avec le pool (share). Ne croyez pas que vous trouvez des blocs toutes les minutes, c’est bien plus compliqué que ça.

Notez qu’il est souvent peu contraignant d’être dans un pool. En effet, la majorité ne demandent aucune inscription, pour y participer il suffit d’utiliser leur lien serveur dans votre logiciel, et on s’identifie grâce à son wallet sur le site pour voir le résultat de son travail. La seule chose à bien vérifier, c’est comment le pool rémunère et combien de temps il faut pour commencer à avoir un aperçu de vos statistiques (oui, mesdames et messieurs, vous êtes bien souvent très/trop pressé(e)s !).

Notez encore une fois que ci-dessous je ne donne que la méthode pour miner avec <strong>Claymore</strong>. Si vous voulez utiliser autre chose, inspirez-vous de ce que vous avez ici et des FAQ et autres Help propre au pool que vous souhaitez rejoindre.
<h2><strong>Dwarfpool</strong></h2>
<p style="text-align: center"><span style="text-decoration: underline"><a href="http://dwarfpool.com/eth">http://dwarfpool.com/eth</a></span></p>
Dwarfpool, c’était historiquement le plus gros pool, mais aujourd'hui d’autres pools se sont bien bien développées. Ils paient selon un système HBPPS (le pool compte le nombre de blocks qu'il a trouvé durant la dernière heure et répartit les gains à tous les mineurs proportionnellement au nombre de partages effectués par chacun durant cette même durée), avec 1% de frais de paiement, et paient 1 fois par heure (mais seulement si votre montant plafond est atteint). Le minage est anonyme (pas de compte à créer). On peut régler le montant plafond à partir duquel les ether cumulés pour le travail effectué sont versés sur le wallet.

La page des stats n’est pas folichonne, mais il y a l’essentiel et l’évolution de vos stats va assez vite. Les vitesses affichées sont calculées selon les derniers partages reçus c’est assez vite juste (environ 30min).

<strong>Pour miner sur Dwarfpool</strong>
<ol>
 	<li>Installer Claymore et le paramétrer avec la config pour miner <strong>comme décrit dans le paragraphe dédié à la présentation du logiciel</strong>.</li>
 	<li>Utilise les paramètres suivants pour créer ton fichier .bat :</li>
</ol>
<ul>
 	<li><strong>URL_POOL = </strong><strong><em>eth-eu.dwarfpool.com</em></strong></li>
 	<li><strong>PORT_POOL = </strong><strong><em>8008</em></strong></li>
</ul>
<strong>Exemple</strong>

Commande passe-partout :
<pre>cmd /K “start /B EthDcrMiner64.exe -epool  eth-eu.dwarfpool.com:8008 -ewal 0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64 -eworker WORKWELL -epsw x”
pause</pre>
<p style="text-align: center"><strong>N’OUBLIEZ PAS DE METTRE VOTRE PROPRE WALLET A LA PLACE DU MIEN</strong></p>
Pour voir ses stats, attendre au moins 15 min, et aller à l’adresse :
<p style="text-align: center">http://dwarfpool.com/eth/address?wallet=<strong><em>VOTRE_WALLET</em></strong></p>

<h2><strong>Ethermine</strong></h2>
<p style="text-align: center"><span style="text-decoration: underline"><a href="http://ethermine.org/">http://ethermine.org/</a></span></p>
Ethermine c’est un bon pool, actuellement le 2<sup>ème</sup> plus gros contributeur. Il est directement issu de Ethpool.org qui est techniquement très au point. La seule chose qui change est le mode de paiement PPLNS (Grosso-modo, ils redistribuent les gains obtenus pour le dernier bloc trouvé proportionnellement à la moyenne de vos partages durant les x derniers blocks trouvés). Il est possible de paramétrer dans account settings la fréquence de paiement (Payment threshold in Ether). Attention par contre, il y a des commissions sur les payouts si votre seuil est inférieur à 1 Ether. Les frais de paiements sont de 1%. Le minage est anonyme (pas de compte à créer).

J’aime bien leur page de statistiques. Attention, le Hashrate n’est pas juste les 60 premières minutes (ils font une moyenne sur les partages reçus).

<strong>Pour miner sur Ethermine</strong>
<ol>
 	<li>Installer Claymore et le paramétrer avec la config pour miner <strong>comme décrit dans le paragraphe dédié à la présentation du logiciel</strong>.</li>
 	<li>Utilise les paramètres suivants pour créer ton fichier .bat :</li>
</ol>
<ul>
 	<li><strong>URL_POOL = </strong><strong>eu1.ethermine.org ou eu2.ethermine.org</strong></li>
 	<li><strong>PORT_POOL = </strong><strong>4444 ou 14444</strong></li>
</ul>
<strong>Exemple</strong>

Commande passe-partout :
<pre>cmd /K “start /B EthDcrMiner64.exe -epool  eu2.ethermine.org:14444 -ewal 0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64 -eworker WORKWELL -epsw x”
pause</pre>
<p style="text-align: center"><strong>N’OUBLIEZ PAS DE METTRE VOTRE PROPRE WALLET A LA PLACE DU MIEN</strong></p>
Pour voir ses stats, attendre au moins 15 min, et aller à l’adresse :
<p style="text-align: center">http://ethermine.org/miners/<strong><em>VOTRE_WALLET</em></strong></p>

<h2><strong>Nanopool</strong></h2>
<p style="text-align: center"><span style="text-decoration: underline"><a href="https://eth.nanopool.org">https://eth.nanopool.org</a></span></p>
<p style="text-align: left">Ce pool paie 4 fois par jours, selon la méthode PPLNS (avec N le nombre de partages durant les dernières 20mins). Il n’y a pas de commission fixe sur les paiements, juste des frais de paiement à hauteur de 1%, comme les autres. Le minage est anonyme (pas de compte à créer). Ils recommandent de ne pas miner chez eux si vous n’avez pas un hashrate d’au moins 5 Mh/s. On trouve une appli Android et iOs pour suivre son travail​.</p>
<strong>Pour miner sur Nanopool</strong>
<ol>
 	<li>Installer Claymore et le paramétrer avec la config pour miner <strong>comme décrit dans le paragraphe dédié à la présentation du logiciel</strong>.</li>
 	<li>Utilise les paramètres suivants pour créer ton fichier .bat :</li>
</ol>
<ul>
 	<li><strong>URL_POOL =</strong><strong> eth-eu1.nanopool.org ou eth-eu2.nanopool.org</strong></li>
 	<li><strong>PORT_POOL = </strong><strong>9999</strong></li>
</ul>
<strong>Exemple</strong>

Commande passe-partout :
<pre>cmd /K “start /B EthDcrMiner64.exe -epool  eth1-eu1.nanopool.org:9999 -ewal 0x41bbe82fbeac4ba2d9afbac0dcc44c7769d13c64 -eworker WORKWELL -epsw x”
pause</pre>
<p style="text-align: center"><strong>N’OUBLIEZ PAS DE METTRE VOTRE PROPRE WALLET A LA PLACE DU MIEN</strong></p>
Pour voir ses stats, attendre au moins 15 min, et aller à l’adresse :
<p style="text-align: center">http://eth.nanopool.org/account/<strong><em>VOTRE_WALLET</em></strong></p>

<h1><strong>Quelques combines pour maximaliser son Hashrate</strong></h1>
Si vous avez le sentiment d’être lésé niveau Hashrate, vous pouvez toujours :
<ul>
 	<li>Vérifier que vous n’avez pas un mauvais pilote graphique (voir en préambule du paragraphe des logiciels)</li>
 	<li>insérer ces quelques commandes au tout début de votre fichier .bat (si vous avez une carte graphique AMD) :</li>
</ul>
<pre>setx GPU_FORCE_64BIT_PTR 0
setx GPU_MAX_HEAP_SIZE 100
setx GPU_USE_SYNC_OBJECTS 1
setx GPU_MAX_ALLOC_PERCENT 100
setx GPU_SINGLE_ALLOC_PERCENT 100</pre>
<ul>
 	<li>Rajouter l’option /affinity 0x1 après start dans votre ligne de commande de votre fichier <strong><em>.bat</em></strong> . Cela va forcer à ce que le programme soit contrôlé par le second cœur de votre processeur, moins utilisé que le premier.</li>
 	<li>Modder sa carte graphique, exemple ici : <a href="https://anorak.tech/t/anoraks-vbios-collection-optimized-settings-for-performance-power-saving/13">https://anorak.tech/t/anoraks-vbios-collection-optimized-settings-for-performance-power-saving/13</a>. Attention toutefois, prenez bien le temps de lire comment faire et ne faites pas n'importe quoi, perso je ne fais pas cela et je ne sais pas comment réparer ceux qui grilleront leur carte. Au passage, flasher le BIOS de sa carte fait perdre la garantie.</li>
</ul>
<h1><strong>Et comment je m'y prends personnellement ?</strong></h1>
Dans mon précédent tuto, j’avais fait un petit script BAT pour lancer CUDAminer et le relancer à une fréquence donnée. Je faisais cela parce que le logiciel plantait régulièrement, alors le script permettait de le redémarrer avant que ça n’arrive. Mais tout cela est de l’histoire ancienne, tout est beaucoup plus stable depuis un moment déjà. Plus tard, j’avais amélioré ce script pour pouvoir choisir le logiciel à lancer (mais celui-là je ne vous l’ai jamais montré). Cela étant, c’était un peu lourd à modifier car régulièrement, un nouveau logiciel ou une nouvelle blockchain sortait et il me fallait modifier le code pour l’utiliser et/ou miner. Bref, j’ai finalement opté pour autre chose.

Actuellement, j’utilise 2 PC pour miner. Il m’arrive aussi de miner autre chose qu’Ethereum. Comme je me débrouille pas trop mal sur Excel et VBA, je me suis fait une feuille avec une petite macro pour lancer/éteindre/redémarrer mes logiciels. C’est beaucoup plus souple à utiliser :

Dans l’onglet « Configuration des programmes » je peux écrire 30 configs différentes pointant vers des logiciels différents. Je mets une description de la ligne de commande histoire de la retrouver dans l’onglet « Start » (obligatoire et attention à ne pas mettre 2 fois la même chose), j’écris le logiciel concerné et sa version (optionnel), j’entre le chemin qui permettra à Excel de retrouver l’exécutable du logiciel (obligatoire), j’écris le nom exact de l’exécutable (obligatoire) et dans la dernière colonne je mets tous les arguments nécessaires pour le lancement du programme (obligatoire, et toujours démarrer par un espace). L’avantage, c’est que les copier/coller de paramètres sont faciles et rapides entre les configs pour tester plusieurs arguments, plusieurs optimisations, etc.

Dans l’onglet « Start », il y a 3 boutons, une coche et un tableau :
<ul>
 	<li>Le tableau permet de rentrer jusqu’à 3 logiciels à démarrer (menu déroulant rappelant les descriptions que vous avez entré dans l’onglet « Configuration des programmes »). L’ordre importe peu, de même que l’on peut très bien ne rentrer que le choix 3 et pas 1 et 2, ça fonctionnera quand même. A droite, en bleu, le rappel de l’exécutable et de la commande complète (ne pas toucher).</li>
 	<li>Le bouton « Miner », lance 1, 2 ou 3 logiciels choisis au préalable dans le petit tableau en dessous.</li>
 	<li>La coche "minimiser" permet d'indiquer si on veut démarrer le(s) logiciel(s) minimisé(s) ou visible(s).</li>
 	<li>Le bouton « Redémarrage », permet d’arrêter les 1, 2 ou 3 logiciels spécifiés dans le petit tableau puis de les redémarrer (s’ils sont buggés par exemple). Attention, cela n’arrête que les logiciels qui sont spécifiés donc si d’autres sont en fonctionnement, ils ne sont pas arrêtés.</li>
 	<li>Le bouton « Stop », permet d’arrêter les 1, 2 ou 3 logiciels spécifiés dans le petit tableau</li>
</ul>
Dans cet onglet, il ne faut rien supprimer et ne pas ajouter/supprimer de lignes. J’ai donc mis un mot de passe (Ethereum-France) pour éviter les bêtises accidentelles.

Vous pouvez télécharger cette feuille ici : <span style="text-decoration: underline"><a href="https://okkoh-owncloud.cloud.seedboxes.cc/index.php/s/8BtDPVf7fvZqRRf">https://okkoh-owncloud.cloud.seedboxes.cc/index.php/s/8BtDPVf7fvZqRRf</a></span> Libre à vous de l’utiliser ou de la modifier comme bon vous semble. Par contre, je ne fais aucun support !
<h1><strong>Créer son outil de minage intensif</strong></h1>
Vous l’aurez peut-être remarqué, mais miner avec son PC gamer ça marche, mais le nombre d’ether gagné par semaine n’est pas légion. Si en plus vous stoppez le logiciel pour tout dézinguer pendant 4h sur le dernier Battlefield, vous ne devez pas avoir énormément d'Ether dans les poches.. Du coup, pour ceux qui souhaiteraient investir un peu plus, il est possible de monter une machine de compétition, dédiée au minage. Il y a mille et une manière de faire ça, mais je vais vous donner quelques idées sur les composants qui me paraissent réellement adaptés (tout en notant bien que personnellement, je n'ai pas de telle machine !). Ainsi, pour bien réussir sa machine de minage, il faut :
<ul>
 	<li>Prendre une carte mère (CM) pas chère mais qui a beaucoup de slots PCi express 1x (ASRock H81 Pro BTC R2.0 par exemple) pour pourvoir brancher un max de GPU.</li>
 	<li>Prendre un processeur entrée de gamme (Intel Celeron G1840 par exemple). Il ne sera de toute façon que très peu sollicité pas la peine d’y mettre plein d’argent.</li>
 	<li>Prendre un peu de mémoire vive, 4Go de RAM suffisent.</li>
 	<li>Préférer, si possible des cartes graphiques (GPU) avec au moins 4Go de mémoire vidéo. Attention, il parait que Windows ne sait pas gérer par défaut plus de 4 GPU mais que ca se contourne. Pas de problème avec Linux (EthOS, Simplemining,…).</li>
 	<li>Ne prévoyez pas d’enfermer le tout dans un boitier, ça va dégager beaucoup de chaleur. Attention également à la pièce dans laquelle vous mettez la chose vu qu'encore une fois ça fait du bruit et ça dégage de la chaleur. En été, s’il fait trop chaud, c’est probable que le hashrate soit diminué pour préserver les cartes graphiques. Voire que ca se coupe!</li>
 	<li>Pour une machine dédiée, préférez un OS dédié, soit EthOS (payant), soit Simplemining OS (gratuit et AMD uniquement, mais on ne peut pas mélanger les RX series avec les R series), soit KopiemTu (Nvidia). Ces logiciels ne sont pas limités pour le nombre de GPU, tant que votre CM les reconnais, ils les gèrent. <span style="text-decoration: underline"><a href="http://ethosdistro.com/">http://ethosdistro.com/</a></span> ou <span style="text-decoration: underline"><a href="https://simplemining.net/">https://simplemining.net/</a></span> ou <span style="text-decoration: underline"><a href="https://bitcointalk.org/index.php?topic=520998.0">https://bitcointalk.org/index.php?topic=520998.0</a></span> Notez que ces distributions fonctionnent toutes avec Linux et qu’il doit probablement être possible d’installer Teamviewer par exemple pour les contrôler à distance si besoin est.</li>
 	<li>Question stockage, un petit SSD de 32Go (on peut acheter EthOS sur un SSD directement) voire une clé USB avec des taux de lecture/écriture rapides suffiront.</li>
 	<li>Il vous faut des risers pour déporter vos GPU de la CM. Préférez des risers alimentés PCIe 1x-16x avec des câbles USB plutôt qu’avec des rubans : <span style="text-decoration: underline"><a href="https://www.amazon.fr/XCSOURCE-Adaptateur-dextension-dalimentation-AC330/dp/B01ER2Z1GY/ref=sr_1_1?ie=UTF8&amp;qid=1487923697&amp;sr=8-1&amp;keywords=riser">https://www.amazon.fr/XCSOURCE-Adaptateur-dextension-dalimentation-AC330/dp/B01ER2Z1GY/ref=sr_1_1?ie=UTF8&amp;qid=1487923697&amp;sr=8-1&amp;keywords=riser</a></span> . Selon les produits, il a été reporté que la qualité des soudures pour les rubans n’est pas toujours au rendez-vous. Pas de problème avec des câbles USB !</li>
 	<li>Pour l’alimentation, sa puissance dépendra du nombre de GPU. Pour être large, comptez 170W/GPU + 150W.</li>
 	<li>Essayez de prendre des alims avec une bonne certification, genre Gold ou Platinium, ça garantit un bon rendement électrique (peu de pertes dans la transformation du courant 220V). Faites attention à avoir un maximum de câbles d'alim PCIe et Molex (on peut acheter des adaptateurs 2*Molex-&gt;PCIe). Si vous voyez une bonne offre sur une alim moins grosse, sachez que vous pouvez travailler avec 2 alims grâce à ça <span style="text-decoration: underline"><a href="http://www.thermaltake.com/products-model.aspx?id=C_00002406">http://www.thermaltake.com/products-model.aspx?id=C_00002406</a></span>. Ou ca <span style="text-decoration: underline"><a href="http://www.la-boutique-du-mineur.com/connectique/11-coupleur-alimentation-dual-psu-50cm.html">http://www.la-boutique-du-mineur.com/connectique/11-coupleur-alimentation-dual-psu-50cm.html</a></span>. Ce câble permet de réveiller la seconde alim, celle qui n’est pas branchée à la carte mère, en même temps que l’autre et d’alimenter les GPU supplémentaires sans retard (et du coup sans casse :) )</li>
</ul>
Attention, je vous rappelle à la prudence concernant vos investissements (voir mon paragraphe sur le sujet plus haut).

<em> </em>
<p style="text-align: center"><em>Voilà, n'hésitez pas à me dire si ce tuto vous a plu et vous a aidé. Pour les quelques personnes prêtes à soutenir/remercier un bénévole, mon wallet : 0x14D65bEa9D868e77C7cbBF2787077A66d760F8bb</em></p>
<p style="text-align: center"><em>Et si vous remarquez des coquilles, dites-le-moi discrètement, je corrigerai ;)</em></p>