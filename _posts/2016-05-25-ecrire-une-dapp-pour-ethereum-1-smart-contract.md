---
ID: 689
post_title: 'Écrire une application décentralisée pour Ethereum – Partie 1 : le smart contract'
author: Sébastien Castiel
post_excerpt: ""
layout: post
permalink: >
  https://www.ethereum-france.com/ecrire-une-dapp-pour-ethereum-1-smart-contract/
published: true
post_date: 2016-05-25 09:02:52
---
<img class="size-medium wp-image-698 alignright" src="https://www.ethereum-france.com/wp-content/uploads/2016/05/lego-keyboard-300x151.jpg" alt="lego-keyboard" width="300" height="151" />

Les possibilités offertes par la blockchain en terme de sécurité, de transparence et de confiance sont à présent reconnues de tous et notamment des médias les plus généralistes. Mais là où Ethereum apporte une nouvelle dimension, c'est dans ce qu'il offre pour intégrer dans la blockchain non pas uniquement des données (transactions monétaires, horodatage de documents...) mais également des programmes, dont l'exécution peut être contrôlée et certifiée au même titre qu'une transaction de Bitcoin.

En tant que développeur, lorsque j'ai découvert Ethereum et compris les possibilités qu'offraient les <em>smart contracts</em> (lire l'article <a href="https://www.ethereum-france.com/smart-contract-ou-le-contrat-auto-executant/">« Smart contract », où le contrat auto-exécutant</a>), ma nouvelle obsession a été de comprendre comment cela fonctionnait techniquement, et comment créer ma propre application décentralisée.<!--more-->

Cette série d’article sera consacrée à l’écriture d’une application entièrement décentralisée profitant des possibilités d’Ethereum. Elle s’adresse plus spécifiquement aux développeurs (web notamment, mais pas nécessairement) qui souhaitent découvrir les possibilités offertes par Ethereum. J’ai choisi de faire reposer ces articles sur un exemple concret d’application, en l’occurrence un jeu de roulette (extrêmement simplifié) de ceux que l’on trouve dans les casinos.

Mais avant de commencer à écrire notre application, voyons d’abord comment s’organise une application décentralisée sur Ethereum, et comment va s’organiser la suite.
<h2>Constitution d’une dApp</h2>
Une application décentralisée (aussi appelée dApp) est généralement accessible depuis un site web. Rien de très nouveau ici me direz-vous, c’est ce qui se fait dans le web depuis son commencement. Ce qui est nouveau en revanche, c’est que cette application web se connecte non pas à un serveur centralisée (serveur web) mais directement à la blockchain d’Ethereum. Cette connexion se fait en se connectant via une API à une application tournant sur le poste de l’utilisateur : son portefeuille.

Autrement dit, sur une application web classique (moderne) :
<ul>
 	<li>l’utilisateur se connecte à un serveur web qui lui renvoie l’interface à afficher dans le navigateur (partie <em>front-end</em>) ;</li>
 	<li>l’interface se connecte à une API (partie <em>back-end</em>) en lui envoyant des données, qui lui renvoient à son tour d’autres données.</li>
</ul>
L’application fonctionne en mode centralisé, dans le sens où a priori tous les utilisateurs se connectent au même serveur web, et font donc confiance à ce serveur. Impossible a priori de vérifier que le serveur web centralisé traite les données comme cela est promis. De plus si le serveur tombe (piratage, fermeture de la société…), toutes les données sont potentiellement perdues.

Dans le cas d’une application décentralisée en revanche :
<ul>
 	<li>l’utilisateur se connecte à un serveur web qui lui renvoie l’interface à afficher dans le navigateur (partie <em>front-end</em>, jusque là pas de changement) ;</li>
 	<li>l’interface se connecte au <em>portefeuille</em> local de l’utilisateur via une API (<em>web3</em>, nous verrons cela plus tard) en créant un contrat ou en appelant une méthode d’un contrat spécifique ;</li>
 	<li>le portefeuille exécute le contrat dans la blockchain, puis renvoie le résultat au front-end.</li>
</ul>
Si l’on fait l’analogie avec une application web classique, on peut donc dire que le rôle de back-end est assuré par le portefeuille local, qui se connecte à la blockchain. Plus de notion de serveur centralisé donc, si ce n’est celui qui sert l’interface web. Mais cette interface web peut après tout être intégrée au sein d’une application desktop par exemple.
<h2>Les étapes de développement de notre dApp</h2>
Au fur et à mesure de cette série d’articles nous allons donc mettre en place une application décentralisée de bout en bout :
<ul>
 	<li>écrire le contrat : ce sera la base applicative de notre jeu de roulette, qui sera distribuée dans la blockchain ;</li>
 	<li>déployer le contrat dans une « blockchain locale », et le tester via la console du navigateur ;</li>
 	<li>écrire une interface web permettant de créer un jeu de roulette d’une part, et d’y jouer d’autre part ;</li>
 	<li>déployer le contrat dans la blockchain réelle, et rendre disponible l’application web pour que d’autres puissent jouer.</li>
</ul>
<strong>Mise en garde</strong> : un contrat Ethereum peut contenir d’importantes failles de sécurité, d’autant plus que la technologie est très jeune. Cela est d’autant plus risqué que l’on manipule indirectement de l’argent (de l’Ether, échangeable contre des euros). Le jeu développé dans cette série d’articles l’est à but purement pédagogique ; en aucun cas je ne recommande de déployer dans la blockchain d’Ethereum contrat (et encore moins un jeu d’argent) sans avoir pris toutes les précautions nécessaires en matière d’audit du code par un expert en sécurité.<code></code>
<h2>Outils de développement nécessaires</h2>
Afin de développer une dApp, nul besoin d’installer une artillerie lourde d’outils, l’environnement reste assez léger. Deux outils sont à installer dans un premier temps :
<ul>
 	<li><a href="http://truffle.readthedocs.org/en/latest/getting_started/installation/">Truffle</a> : il s’agit d’une petite suite de développement créée par ConsenSys comprenant le nécessaire pour compiler très facilement un contrat, le déployer dans la blockchain, et générer un squelette de dApp permettant d’y accéder ;</li>
 	<li><a href="https://github.com/ethereumjs/testrpc">Test RPC</a> : un petit client permettant de simuler un portefeuille local connecté à une blockchain locale également ; idéal pour les tests :)</li>
</ul>
À noter que l’installation de ces outils nécessite l’installation préalable de <a href="https://nodejs.org/en/download/">Node.js</a>. Une fois ces outils installés, il est temps de passer à la première étape du développement de notre application : le contrat.
<h1>Écrire le smart contract pour Ethereum</h1>
Plongeons dans le vif du sujet avec l’écriture du contrat ; mais pas trop vite, prenons quelques minutes pour spécifier le comportement attendu de notre contrat dans le contexte de notre application de roulette.
<h2>Spécifications fonctionnelles du contrat</h2>
Techniquement, les contrats Ethereum sont stockés dans la blockchain sous forme de code binaire assemblé semblable au code machine exécuté par nos ordinateurs. Mais bien évidemment il existe un langage de plus haut niveau permettant l’écriture des contrats : ￼Solidity￼. À mi-chemin entre le C et le JavaScript, il ne vous dépaysera pas si vous êtes un habitué des langages de programmation répandus.

[caption id="attachment_730" align="alignright" width="300"]<img class="wp-image-730 size-medium" src="https://www.ethereum-france.com/wp-content/uploads/2016/05/3503351816_906db0ffd7_z-300x225.jpg" alt="roulette" width="300" height="225" /> Licence <a href="https://creativecommons.org/licenses/by/2.0/" target="_blank">CC-BY-2.0</a> (<a href="https://flic.kr/p/6kzArw" target="_blank">Source</a>)[/caption]

Commençons par définir le comportement attendu de notre contrat. Le but est donc de gérer un jeu de roulette simplifié. Le principe est le suivant : à intervalles réguliers, un nombre aléatoire est choisi entre 0 et 36. Avant cela les joueurs ont le choix de miser :
<ul>
 	<li>soit sur un numéro (entre 0 et 36 donc) : le joueur gagne 35 fois sa mise si ce numéro tombe ;</li>
 	<li>soit sur la case « pair » : le joueur gagne deux fois sa mise si un numéro pair et différent de 0 tombe ;</li>
 	<li>soit sur la base « impair » : le joueur gagne deux fois sa mise si un numéro impair tombe.</li>
</ul>
Le jeu de roulette inclut également la possibilité de miser « à cheval » sur deux ou quatre numéros, sur des lignes, des colonnes, etc. mais nous nous en tiendrons pour l’instant à ces trois possibilités.

Notre contrat devra donc :
<ul>
 	<li>être créé avec comme paramètre l’intervalle de temps entre deux tours ;</li>
 	<li>recevoir les paris des joueurs : chacun est constitué d’un type (numéro simple <em>single</em>, pair <em>even</em> ou impair <em>odd</em>), du numéro le cas échéant, et du montant misé ;</li>
 	<li>lorsque le temps est écoulé, choisir un numéro aléatoire entre 0 et 36, et payer les joueurs gagnants.</li>
</ul>
Rien de très compliqué, mais certains points méritent quelques précisions. Tout d’abord les mises des joueurs et le paiement des gagnants sera fait directement grâce à de l’Ether inclut dans les transactions. Il aurait été possible d’utiliser une cryptomonnaie personnalisée comme cela est assez facile à implémenter avec Ethereum, mais il est intéressant de présenter l’intégration de l’Ether dans un contrat.

Deuxième point : il n’est pas possible nativement de programmer l’appel à une méthode d’un contrat. Il faut nécessairement qu’un utilisateur ou un autre contrat l’appelle. C’est pourquoi notre contrat donnera la possibilité à tout le monde de « tourner » la roulette et ainsi déclencher les paiements aux gagnants, tant que l’intervalle défini entre deux tours est bien écoulé. Ainsi chacun sait que ses mises ne seront pas bloquées parce que la roulette n’a pas été lancée.

Dernier point : il n’est pas non plus possible de tirer un nombre aléatoire dans un contrat Ethereum. En effet, le principe même de la blockchain veut que le résultat final de l’exécution soit le même quelque soit le nœud ayant procédé à l’exécution. Pour simuler ce tirage, nous utiliserons donc le hash du dernier block reçu avant l’exécution. Théoriquement il est donc possible de « manipuler » le tirage, mais cela reste difficile et coûteux ; et pour sécuriser davantage, on peut toujours utiliser les 2, 3…n derniers blocs.

À noter que certaines vérifications seront effectuées à chaque pari demandé :
<ul>
 	<li>il faudra que la transaction comprenne de l’Ether (le montant de la mise) ;</li>
 	<li>il faudra que la banque dispose d’assez de réserve pour payer les joueurs en partant du principe que tous seront gagnants ; autrement dit il faudra que l’adresse du contrat dispose d’assez d’Ether pour payer tous les paris cumulés depuis le dernier tour si ceux-ci s’avèrent gagnants.</li>
</ul>
Notre contrat est spécifié, il est temps à présent de l’écrire.
<h2>Écrire le contrat</h2>
Tout d’abord, un contrat réside dans un bloc <code>contract</code>. Typiquement, chaque contrat réside dans un fichier <em>.sol</em>. Ici notre application ne contiendra qu’un seul contrat ; plaçons-le dans le fichier <em>Roulette.sol</em>.
<pre>contract Roulette {
	// ...
}
</pre>
<h3>Variables et types de données</h3>
Commençons à présent par déclarer quelques variables :
<pre>uint public lastRoundTimestamp;
uint public nextRoundTimestamp;
uint _interval;
address _creator;
</pre>
[caption id="attachment_747" align="alignright" width="400"]<img class="wp-image-747" src="https://www.ethereum-france.com/wp-content/uploads/2016/05/Capture-d’écran-2016-05-24-à-22.30.08-278x300.png" alt="L'éditeur Atom dispose d'un paquet pour la coloration syntaxique de Solidity" width="400" height="431" /> L'éditeur <a href="https://atom.io/" target="_blank">Atom</a> dispose d'un <a href="https://atom.io/packages/language-ethereum" target="_blank">paquet</a> pour la coloration syntaxique de Solidity[/caption]

La syntaxe de déclaration d’une variable est la suivante : <code>&lt;type&gt; [modifier] &lt;name&gt;</code>. Ici nous avons donc trois variables de type <code>uint</code> (entier non signé, c’est-à-dire positif), dont deux sont publiques, ce qui signifie qu’il sera possible à tout le monde de demander au contrat leur valeur actuelle. Il s’agit ici de <em>timestamps</em>, en l’occurrence celui du dernier tour et du prochain tour.

La troisième est privée, donc inaccessible à l’extérieur du contrat. Il s’agit de l’intervalle en secondes entre deux tours. La dernière variable enfin est type <em>address</em> : elle contient l’adresse du créateur du contrat, c’est-à-dire le compte Ethereum qui a créé et lancé le jeu. Cette information nous servira car elle nous permettra lorsque l’on souhaitera arrêter la partie de verser les Ethers restants sur le compte du contrat au compte ayant lancé le jeu.

Il nous reste une dernière variable à déclarer : celle qui contiendra les paris des joueurs pour le tour en cours. Cette variable est de type tableau et contient un type d’objet plus complexe : des structures, elles-mêmes comportant des énumérations.
<pre>enum BetType { Single, Odd, Even }
struct Bet {
	BetType betType;
	address player;
	uint number;
	uint value;
}
Bet[] public bets;
</pre>
Tout d’abord nous déclarons une énumération, comme cela existe dans plusieurs langages de programmation. Celle-ci contient les différents types de paris possibles : numéro simple, impair et pair.

La structure <code>Bet</code> déclarée ensuite représente un pari. Elle comprend donc :
<ul>
 	<li>le type du pari (en utilisant notre énumération <code>BetType</code>) ;</li>
 	<li>l’adresse du joueur ayant fait le pari ;</li>
 	<li>le numéro sur lequel a misé le joueur (non utilisé pour les paris de types pair et impair) ;</li>
 	<li>la valeur du pari, autrement dit la mise (en <em>wei</em>, fraction la plus petite d’Ether, un Ether comportant 10^18 weis, autrement dit un milliard de millards de weis).</li>
</ul>
Les paris sont stockés dans la variable <code>bets</code>, de type tableau de <code>Bet</code>s. Notez qu’il a été décidé ici de rendre les paris publics (comme cela est le cas dans un vrai jeu de roulette : tout le monde peut voir la table de jeu avec les paris en cours).

Dernière chose à déclarer avant de passer aux fonctions du contrat : les évènements. Dans notre cas nous n’en aurons qu’un seul, déclenché lorsque le tour est terminé et qu’un numéro a été tiré :
<pre>event Finished(uint number, uint nextRoundTimestamp);
</pre>
Nous déclarons ici que notre contrat est susceptible de déclencher cet évènement, en y associant deux paramètres de type entier. Il s’agira du numéro tiré, et du <em>timestamp</em> correspondant à l’heure du prochain tour.

C’est terminé pour les déclarations, passons maintenant au cœur du contrat : les fonctions.
<h3>Les fonctions de notre contrat</h3>
Dans Solidity un contrat peut en réalité être considéré comme une classe, comme on en trouve en programmation orientée objet. C’est-à-dire qu’à partir d’une classe on peut créer plusieurs objets (les instances de la classe), et que chacun aura son propre espace mémoire pour stocker les valeurs des variables que nous avons déclarées dans le paragraphe précédent.

Ainsi de la même manière que dans les autres langages orientés objets, on peut définir pour un contrat des méthodes, qui sont plutôt nommées <em>fonctions </em>dans Solidity.

Et l’une d’elles est particulière puisque c’est elle qui est automatiquement appelée à la création (ou plutôt l’instanciation) d’un contrat : le constructeur. Comme dans beaucoup de langages, elle a pour signe distinctif d’avoir un nom identique au contrat :
<pre>function Roulette(uint interval) {
	_interval = interval;
	_creator = msg.sender;
	nextRoundTimestamp = now + _interval;
}
</pre>
Notre constructeur prend un paramètre <code>interval</code> de type entier non signé, qui nous sert à initialiser la variable <code>_interval</code> évoquée plus haut, contenant le nombre de secondes entre deux tours de jeu.

Le constructeur initialise également la variable <code>_creator</code> contenant l’adresse du créateur de la partie. Pour cela il accède à l’objet global <code>msg</code> contenant les informations de la transactions courantes, et en particulier sa propriété <code>sender</code> qui comprend l’adresse de l’émetteur de la transaction. Enfin la variable publique <code>nextRoundTimestamp</code> est initialisée à partir du timestamp courant.

Passons aux fonctions publiques permettant aux joueurs de faire des paris :
<pre>function betSingle(uint number) public transactionMustContainEther() bankMustBeAbleToPayForBetType(BetType.Single) {
	if (number &gt; 36) throw;
	bets.push(Bet({
		betType: BetType.Single,
		player: msg.sender,
		number: number,
		value: msg.value
	}));
}
</pre>
La fonction <code>betSingle</code> permet de miser sur un numéro. Elle est publique, c’est-à-dire qu’elle peut être appelée par n’importe qui. Nous reviendrons plus loin sur le reste de la première ligne ; il s’agit de <em>modifiers</em> qui nous permettent ici de vérifier que l’appel est autorisé, à savoir que la transaction contient de l’Ether (la valeur de la mise) et que la banque sera en mesure de payer si tous les joueurs gagnent.

La première ligne du corps de la fonction vérifie la validité du paramètre <code>number</code> : il faut qu’il soit inférieur ou égal à 36 (le fait qu’il soit supérieur ou égal à 0 est assuré par le type même du paramètre). Dans le cas contraire, par l’instruction <code>throw</code> nous arrêtons purement et simplement l’exécution de l’appel à la fonction. Si l’état du contrat avait été modifié (changement de valeur d’une variable), ces modifications sont annulées.

Puis on ajoute à la liste des paris en cours un nouveau pari. Notez à nouveau l’utilisation de <code>msg.sender</code> pour stocker l’adresse du joueur, à savoir l’adresse du compte à l’origine de la transaction, ainsi que de <code>msg.value</code> qui contient le solde en weis associé à la transaction, et qui correspond donc ici à la mise du pari.

On remarque donc que l’appel à une fonction d’un contrat n’est rien d’autre qu’une simple transaction. Celle-ci peut contenir une valeur en weis et/ou demander l’exécution d’une fonction sur un contrat. Elle peut également retourner une valeur, comme c’est le cas dans cette fonction permettant de connaître le nombre de paris en cours, et la valeur totale des paris :
<pre>function getBetsCountAndValue() public constant returns(uint, uint) {
	uint value = 0;
	for (uint i = 0; i &lt; bets.length; i++) {
		value += bets[i].value;
	}
	return (bets.length, value);
}
</pre>
En plus de la rendre publique, on déclare également que cette fonction ne modifie pas l’état du contrat (<code>constant</code>), et qu’elle renvoie une paire d’entiers non signés (<code>returns(uint, uint)</code>). Peu de choses à dire sur cette fonction, vous ne devriez pas avoir trop de mal à comprendre comment elle fonctionne !

Analysons à présent la fonction qui permet de faire tourner la roulette :
<pre>function launch() public {
	if (now &lt; nextRoundTimestamp) throw;

	uint number = uint(block.blockhash(block.number - 1)) % 37;
	
	for (uint i = 0; i &lt; bets.length; i++) {
		bool won = false;
		uint payout = 0;
		if (bets[i].betType == BetType.Single) {
			if (bets[i].number == number) {
				won = true;
			}
		} else if (bets[i].betType == BetType.Even) {
			if (number &gt; 0 &amp;&amp; number % 2 == 0) {
				won = true;
			}
		} else if (bets[i].betType == BetType.Odd) {
			if (number &gt; 0 &amp;&amp; number % 2 == 1) {
				won = true;
			}
		}
		if (won) {
			bets[i].player.send(bets[i].value * getPayoutForType(bets[i].betType));
		}
	}

	uint thisRoundTimestamp = nextRoundTimestamp;
	nextRoundTimestamp = thisRoundTimestamp + _interval;
	lastRoundTimestamp = thisRoundTimestamp;

	bets.length = 0;

	Finished(number, nextRoundTimestamp);
}
</pre>
Rien de très compliqué à nouveau. On vérifie tout d’abord que l’opération est autorisée, c’est à dire si l’heure actuelle est bien supérieure à l’heure prévue pour le tour suivant. Dans le cas contraire, on arrête l’exécution.

On tire ensuite un nombre « aléatoire » : comme expliqué dans le paragraphe consacré aux spécifications du contrat, il n’est pas possible d’utiliser un nombre réellement aléatoire, puisque l’exécution doit être déterministe. Autrement dit, toute exécution du contrat dans la blockchain doit donner le même résultat. C’est pourquoi on se base sur le hash du dernier bloc généré, converti en entier, et auquel on applique un « modulo 37 », ce qui nous donne un entier compris entre 0 et 36 : <code>uint(block.blockhash(block.number - 1))</code>.

La suite consiste à parcourir chaque pari, et vérifier s’il est gagnant ou non en fonction de son type. Le cas échéant, on émet une transaction grâce à la méthode <code>send</code> applicable aux variables de type <code>address</code> . La fonction <code>getPayoutForType</code> nous permet ici de récupérer le coefficient multiplicateur de la mise si le pari est gagnant (×35 pour un numéro simple, ×2 pour les pairs/impairs) :
<pre>function getPayoutForType(BetType betType) constant returns(uint) {
	if (betType == BetType.Single) return 35;
	if (betType == BetType.Even || betType == BetType.Odd) return 2;
	return 0;
}
</pre>
À la fin de notre fonction <code>launch</code>, on réinitialise les variables pour le prochain tour :
<ul>
 	<li>on définit la date du prochain tour ;</li>
 	<li>on vide le tableau des paris en cours (en lui définissant sa taille à zéro) ;</li>
</ul>
Enfin, on émet un évènement <code>Finished</code> (comme déclaré plus haut), contenant le numéro tiré, et la date du prochain tour.
<h3>Ajouter des comportements aux fonctions grâce aux <em>modifiers</em></h3>
Revenons à la notion de <em>modifier</em> que nous avions mise de côté. Partons de la fonction <em>betEven</em> permettant de faire un pari de type « pair » :
<pre>function betEven() public transactionMustContainEther() bankMustBeAbleToPayForBetType(BetType.Even) {
	bets.push(Bet({
		betType: BetType.Even,
		player: msg.sender,
		number: 0,
		value: msg.value
	}));
}
</pre>
Dans la déclaration de la fonction, <code>transactionMustContainEther</code> et <code>bankMustBeAbleToPayForBetType</code> sont des modifiers, c’est-à-dire des comportement assignés par défaut à la fonction. Examinons par exemple la déclaration du premier modifier :
<pre>modifier transactionMustContainEther() {
	if (msg.value == 0) throw;
	_
}
</pre>
Finalement c’est très simple : un modifier ressemble en tout point à une fonction, sauf :
<ul>
 	<li>qu’il est déclaré avec le mot-clé <code>modifier</code> ;</li>
 	<li>que son corps comporte l’opérateur underscore <code>_</code> : c’est à cet endroit que sera exécuté le code de la fonction modifiée.</li>
</ul>
Autrement dit, ici notre modifier ajoute une instruction au début des fonctions sur lesquels il est utilisé ; cette instruction déclenche une erreur si la transaction ne comporte pas d’Ether.

Le deuxième modifier est légèrement plus complexe, mais le principe est exactement le même :
<pre>modifier bankMustBeAbleToPayForBetType(BetType betType) {
	uint necessaryBalance = 0;
	for (uint i = 0; i &lt; bets.length; i++) {
		necessaryBalance += getPayoutForType(bets[i].betType) * bets[i].value;
	}
	necessaryBalance += getPayoutForType(betType) * msg.value;
	if (necessaryBalance &gt; this.balance) throw;
	_
}
</pre>
De la même manière, il s’agit d’ajouter une vérification avant l’exécution de la fonction modifiée. On parcourt les paris en cours pour calculer la somme maximale que la banque devra payer si tous les joueurs gagnent. On y ajoute le pari demandé dans la transaction en cours, et si le nouveau montant est supérieur au solde de la banque, alors on refuse la transaction.

C’en est fini pour l’écriture du contrat ; vous pouvez retrouver <a href="https://gist.github.com/scastiel/f2a6bd31427fa183a8dc24acf5802fa1">ici son code complet</a>. Il est temps désormais de le compiler et de le déployer dans la blockchain (de test pour le moment) afin de commencer à jouer un peu avec !
<h2>Compilation et test du contrat</h2>
Comme je l’ai précisé en introduction, nous allons tester notre contrat non pas dans la blockchain d’Ethereum, mais dans une sorte de blockchain locale de test, <em>Test RPC</em>, que vous avez dû installer. Il s’agit d’un petit logiciel, qui une fois lancé permet de recevoir des connexions provenant d’une dApp, comme s’il s’agissait de la blockchain d’Ethereum.
<h3>Découverte de Test RPC et de l’API web3</h3>
Pour lancer Test RPC, il suffit de taper la commande <code>testrpc</code> dans votre terminal :
<pre>$ testrpc
EthereumJS TestRPC v2.0.0

Available Accounts
==================
(0) 0xf8974c13f35c2309f9850f633d02f357e4d57601
(1) 0x7f867900fd1e2a9b5efd17c2e1deb12b4de4155a
(...)
</pre>
Par défaut, Test RPC initialise sa blockchain avec 10 comptes (adresses), chacun étant crédité d’une quantité quasiment infinie d’Ether. Cela peut être très pratique, mais pour tester notre contrat, il sera préférable d’avoir une quantité plus raisonnable d’Ethers. Pour cela, il faut passer en paramètres des clés privées et les montants associés (en weis) au programme <em>testrpc</em>. Pour générer une clé privée, vous pouvez par exemple utiliser le site <a href="https://www.myetherwallet.com/">MyEtherWallet</a>.

J’ai par exemple généré deux clés privées ; voici la commande permettant de lancer Test RPC en créditant ces deux adresses de 10 000 Ethers :
<pre>$ testrpc --account="0x40e16bbfe219ecaa733169b9192604338d0c55d48a3c90dae45badaede6822ff,10000000000000000000000" --account="0xf5d09e61086d537581377e29c93edcf19de73b42230c7b9fe390e4dd560ffc0a,10000000000000000000000"
</pre>
<img class="aligncenter wp-image-713" src="https://www.ethereum-france.com/wp-content/uploads/2016/05/Capture-d’écran-2016-05-24-à-15.06.47-1024x689.png" alt="testrpc screenshot" width="500" height="336" />

À présent que notre wallet local tourne, il s’agit de s’y connecter. Bien évidemment, au final la connexion sera réalisée par la partie web de notre application, mais pour le moment, tentons simplement d’accéder à une console qui nous permettra de tester notre contrat.

La méthode la plus simple selon moi est d’utiliser directement l’API JavaScript d’Ethereum : <a href="https://github.com/ethereum/wiki/wiki/JavaScript-API">web3</a>. C’est celle qui sera utilisée dans notre application, mais nous pouvons également l’utiliser indépendamment de toute interface web en passant par Node.js. Pour cela :
<ol>
 	<li>Créez un nouveau répertoire quelque part sur votre machine, et rendez-y-vous dans votre terminal : <code>mkdir -p ~/Documents/testweb3 ; cd $_</code> ;</li>
 	<li>Installez localement le module <em>web3</em> pour Node.js : <code>npm install web3</code> ;</li>
 	<li>Lancez l’invite de commande Node.js (<code>node</code>) et importez le module <em>web3</em> : <code>var Web3 = require('web3')</code>.</li>
</ol>
À présent, vous pouvez vous connecter à votre serveur Test RPC, et vérifiez que les adresses initialisées sont bien présentes, et disposent bien du bon solde d’Ether :
<pre>&gt; var Web3 = require('web3');
&gt; var web3 = new Web3(new Web3.providers.HttpProvider("http://localhost:8545"));
&gt; web3.eth.accounts
[ '0x00ae1858ea41f5667cda17c7915c2f289c4ee819',
  '0x7f8105da4dd1af61da7bf587766103ba8534fcdc' ]
&gt; web3.fromWei(web3.eth.getBalance(web3.eth.accounts[0]), "ether").toNumber()
10000
</pre>
Grâce à <code>web3.eth.accounts</code>, nous accédons l’ensemble des comptes locaux pour lesquels nous disposons de la clé privée. Il s’agit d’un tableau contenant les adresses des comptes sous forme de chaîne de caractère.

La méthode <code>web3.eth.getBalance</code> permet tout simple de récupérer le solde en Ethers d’une adresse, en weis. Notez que dans la mesure où ces montants sont la plupart du temps très élevés (1 Ether = 10^18 weis), l’API web3 a recours à la bibliothèque <a href="https://github.com/MikeMcl/bignumber.js/">bignumber.js</a>, permettant comme son nom l’indique de manipuler des grands nombres. C’est pourquoi si vous appelez <code>web3.eth.getBalance("&lt;addr&gt;")</code>, vous n’aurez sans doute pas la valeur que vous espériez. Pour obtenir une valeur numérique, il faut utiliser la méthode <code>toNumber()</code> du résultat.

Enfin web3 propose aussi de convertir des valeurs en Ether, weis, etc. Dans l’exemple présenté plus haut, nous convertissons donc une valeur initialement en weis (retournée par <code>getBalance</code>) en Ethers.
<h3>Compilation et déploiement du contrat</h3>
Il est temps de compiler notre contrat avant de le déployer dans la blockchain. Pour cela nous allons utiliser l’outil <a href="https://github.com/ConsenSys/truffle">Truffle</a>. Théoriquement nous pouvons compiler et déployer notre contrat directement depuis la console de Node avec l’API web3, mais Truffle va grandement nous simplifier la tâche.

Truffle permet de créer facilement des dApps, en allant de la compilation du contrat jusqu’à la phase de build de l’application web (à l’instar de ce que font Grunt, Gulp et autre Webpack).

Tout d’abord il nous faut créer un projet Truffle. Pour cela, créez un répertoire vide, puis tapez-y la commande <code>truffle init</code>. Vous pouvez alors voir que Truffle a créé plusieurs répertoires et fichiers. Pour le moment, intéressons-nous à notre contrat. Supprimons donc purement et simplement le contenu du répertoire <em>contracts</em>, et créons-y un fichier <em>Roulette.sol</em>, contenant le code de notre contrat .

De plus, ouvrez le fichier <em>truffle.json</em> à la racine du répertoire, et remplacez la valeur de l’attribut <code>deploy</code> (actuellement « Metacoin ») par « Roulette ».

La compilation est ensuite très simple, il suffit de taper la commande <code>truffle compile</code>. Si tout se passe bien (ce qui devrait être le cas), déployer le contrat dans notre blockchain locale ne sera pas plus compliqué : <code>truffle deploy</code>. (Assurez-vous bien que <em>testrpc</em> est lancé, cela est nécessaire même pour la compilation du contrat.)

<img class="aligncenter wp-image-718" src="https://www.ethereum-france.com/wp-content/uploads/2016/05/Capture-d’écran-2016-05-24-à-18.31.39-300x202.png" alt="truffle screenshot" width="500" height="336" />
<h3>Test du contrat déployé</h3>
Pour tester notre contrat, il est possible de lancer une console Node.js dont l'environnement a été initialisé avec les contrats du projet. C'est-à-dire que les bibliothèques nécessaires à l'appel de l'API <em>web3</em> ont déjà été importées. Encore mieux, lors de la compilation d'un contrat, Truffle génère un fichier <em>(Roulette.sol.js)</em> contenant en quelques sortes une classe <em>Roulette</em> dont les méthodes sont justement les méthodes publiques de notre contrat (ce n'est pas exactement cela, mais dans l'utilisation cela revient ça). De plus ce fichier contient également l'adresse à laquelle a été déployée le contrat lors de la commande <code>truffle deploy</code>. Pratique ;)

Pour lancer cette console, utilisez simplement la commande : <code>truffle console</code>

<img class="aligncenter wp-image-739" src="https://www.ethereum-france.com/wp-content/uploads/2016/05/Capture-d’écran-2016-05-24-à-21.52.50-300x210.png" alt="truffle console screenshot" width="500" height="350" />

Commençons donc par créer une partie de roulette. Pour cela nous appelons la méthode <code>new</code> de l’objet <code>Roulette</code>, qui appellera le constructeur de notre contrat. Les premiers paramètres correspondent aux paramètres du constructeur (dans notre cas il n’y en a qu’un seul, le nombre de secondes minimal entre deux parties), puis le paramètre suivant est un objet contenant les informations sur la transaction. (Rappelez-vous que dans Ethereum, tout appel à une méthode d’un contrat, ou même la création d’un contrat, est fait dans une transaction, ayant donc un émetteur, un destinataire, et éventuellement un solde d’Ether qui y est attaché.)

Dans notre cas l’émetteur sera la première des deux adresses que nous avons paramétrées dans <em>testrpc</em>. Le solde d’Ether attaché sera la réserve de la banque. Notez que rien ne nous empêche d’envoyer ce solde au contrat (qui dispose désormais d’une adresse qui lui est propre) dans une autre transaction.

La création de notre contrat se fait de manière asynchrone grâce aux <em>promises</em> de JavaScript, déclarons-donc d’abord une variable qui contiendra le contrat créé :
<pre>&gt; var contract = null;
</pre>
Puis appelons enfin la méthode <code>Roulette.new</code> afin de créer le contrat :
<pre>&gt; Roulette.new(10, { from: web3.eth.accounts[0], value: web3.toWei(100, "ether") }).then(function(_contract) { contract = _contract; });
</pre>
La création ne devrait pas prendre plus de quelques fractions de secondes, nous pouvons donc inspecter le contenu de l’objet <code>contract</code> (en tapant simple <code>contract</code> dans la console). Comme vous pouvez le voir, cet objet dispose notamment des méthodes <code>betSingle</code>, <code>betEven</code>, etc. correspondant aux méthodes de notre contrat Solidity. Notez également que les variables publiques sont accessibles par des méthodes également.

Consultons à présent le solde de notre contrat :
<pre>&gt; web3.fromWei(web3.eth.getBalance(contract.address), "ether").toNumber()
</pre>
En toute logique cela devrait vous retourner 100, puisque c’est le solde que nous avons envoyé au contrat.

Effectuons maintenant un pari avec l’adresse du deuxième compte paramétré dans <em>testrpc</em> :
<pre>&gt; contract.betEven({ from: web3.eth.accounts[1], value: web3.toWei(1, "ether") })
</pre>
Si vous reconsultez le solde du contrat, celui-ci dont être désormais de 101. Il ne nous reste qu’à faire tourner la roulette :
<pre>&gt; contract.launch({ from: web3.eth.accounts[0] })
</pre>
Pour le moment nous ne nous sommes pas abonnés aux évènements déclenchés par le contrat, il faut donc consulter les soldes de la banque (du contrat) ou du joueur pour savoir qui a gagné. En répétant les trois dernières commandes plusieurs fois, vous devriez valider que parfois le joueur gagne, et parfois la banque :)

Arrêtons-nous ici pour le test du contrat. Bien évidemment il est possible de faire beaucoup plus, nous verrons cela dans l’article suivant consacré à la mise en place de l’application web qui va se connecter au contrat. Comme vous le verrez ce seront exactement les mêmes concepts, mis à part que grâce à Truffle cela paraîtra plus simple.

J’espère que cette introduction à l’écriture de contrats Ethereum grâce à Solidity vous a donné envie de continuer à suivre cette série d’articles. En attendant la publication du prochain article, n’hésitez pas à m’adresser vos remarques ou questions en commentaire. À bientôt pour la suite de nos aventures !

&nbsp;
<h3>Ressources utiles :</h3>
<ul>
 	<li><a href="https://solidity.readthedocs.io/en/latest/index.html" target="_blank">Documentation de Solidity</a></li>
 	<li><a href="http://truffle.readthedocs.io/en/latest/" target="_blank">Documentation de Truffle</a></li>
</ul>