---
ID: 2728
post_title: 'Caveat Contractor: retour sur le bug du Multisig de Parity'
author: JdeTychey
post_excerpt: ""
layout: post
permalink: >
  https://www.ethereum-france.com/caveat-contractor-retour-sur-le-bug-du-multisig-de-parity/
published: true
post_date: 2017-10-09 15:18:33
---
[caption id="attachment_media-19" align="alignnone" width="1434"]<img class="alignnone size-full wp-image-2774" src="https://www.ethereum-france.com/wp-content/uploads/2017/09/Tax-collector.jpg" alt="Tax collector.jpg" width="1434" height="1792" /> Marinus van Reymerswaele - deux collecteurs d'impôts (vers 1540)[/caption]

Le 19 juillet un bug a été exploité dans le contrat multisig que permet de déployer le client Parity v1.5. Au total 83 017 éthers ont été subtilisés, ces fonds avaient été initialement collectés par Edgeless Casino, Swarm City, et æternity lors de leurs ICOs respectives. Cet article revient sur le fonctionnement de l'attaque et les réactions de la communauté.

&nbsp;
<h2>Multisig: un contrat pour partager le contrôle de ses éthers</h2>
Les wallets de multisig existent longtemps sur bitcoin, le principe général est de partager entre plusieurs clés le contrôle d'une adresse et donc des bitcoins qui y pointent. On parle alors de signatures M-of-N, ou M-sur-N en français, pour exprimer le fait qu'il faille la signature de M clés sur les N clés qui se partagent le contrôle pour que la transaction émanant de l'adresse multisig soit valide.

Sur Ethereum les wallet multisig prennent la forme de contrats avec leur logique et fonctionnalités propres. Parmi les implémentations les plus populaire on trouve celle de <a href="https://github.com/gnosis/MultiSigWallet">Gnosis</a> avec son interface web et celui <a href="https://github.com/ethereum/dapp-bin/blob/master/wallet/wallet.sol">maintenu par la Fondation Ethereum</a> dont l'auteur n'est autre que <a href="http://gavwood.com/">Gavin Wood</a> - fondateur et CTO de Parity technologies.

&nbsp;
<h2>Le multisig de Parity, un contrat de qualité mais mal déployé</h2>
Le client Parity possède une interface graphique pour générer un Multisig:

[caption id="attachment_2849" align="alignnone" width="1520"]<img class="alignnone size-full wp-image-2849" src="https://www.ethereum-france.com/wp-content/uploads/2017/09/Capture-du-2017-09-27-17-53-56-907506050-1506528111631.png" alt="Parity Multisig.png" width="1520" height="786" /> L'interface graphique de création de Multisig sur Parity[/caption]

Cette interface permet de déployer facilement un contrat de multisig paramétré. Dans sa version 1.5, ce processus comportait une vulnérabilité importante que nous allons détaillé.

Dans <a href="https://github.com/paritytech/parity/blob/4d08e7b0aec46443bf26547b17d10cb302672835/js/src/contracts/snippets/enhanced-wallet.sol#L216">cette version</a> le multisig s'initialise au déploiement en faisant appel à un smartcontrat déjà déployé, la librairie "WalletLibrary". A la ligne 395, le contrat Wallet commence avec la description de son constructor, cette fonction porte le nom du contrat et ne s'exécute qu'une seule fois lors du déploiement. Regardons cette fonction de plus prêt.

En premier lieu, on passe au constructor les paramètres du futur Multisig, à savoir la listes des propriétaires, le nombre d'avis positifs de propriétaire nécessaire à l'exécution d'une transaction et la limite de transactions par jour.

En second lieu, le constructor prépare un appel à "WalletLibrary" avec les paramètres indiqués supra. Cette partie du code est très optimisée et se termine en assembleur par l'appel en lui-même <em>delegatecall </em>ligne 417.

Enfin, la conséquence de ce <em>delegatecall</em> est d'exécuter "initWallet" (ligne 216) qui termine d'initialiser le Multisig.

Simple non? Le déploiement de ce Multisig est très peu coûteux car il se sert d'une librairie pour externaliser son initialisation et ne contient aucune méthode superflue. En effet, si une transaction vers le Multisig contient du code, le traitement de ce code est lui même externalisé vers la librairie (cf.ligne 428)! Au final le Multisig est près de 70% moins cher à déployer.
<p style="text-align: center;"><strong>[Alerte Spoiler, le bug exploité est révélé après cette image]</strong></p>


[caption id="attachment_media-19" align="alignnone" width="1053"]<img class="alignnone size-full wp-image-2892" src="https://www.ethereum-france.com/wp-content/uploads/2017/10/DCEGihXW0AAvWvn.jpg" alt="DCEGihXW0AAvWvn.jpg" width="1053" height="989" /> <em>What could possibly go wrong?</em>[/caption]

Que ce passe-t-il si quelqu'un envoie au contrat Multisig une transaction contenant des données d'initialisation avec un nouveau et unique propriétaire? Le contrat exécute un delegatecall vers la librairie qui exécute initWallet avec les paramètres reçus, tout simplement. La liste des propriétaires est ni plus ni moins mise à jour! Il ne reste plus qu'à envoyer une transaction ordonnant le transfert des fonds.

Le 18 juillet au bloc <a href="https://etherscan.io/tx/0x0e0d16475d2ac6a4802437a35a21776e5c9b681a77fef1693b0badbb6afdb083">4041179</a>,  une première transaction exploitant ce bug est lancée sur un contrat Multisig, puis deux autres contrats sont compromis aux blocs <a href="https://etherscan.io/tx/0x97f7662322d56e1c54bd1bab39bccf98bc736fcb9c7e61640e6ff1f633637d38">4043791</a> et <a href="https://etherscan.io/tx/0xeef10fc5170f669b86c4cd0444882a96087221325f8bf2f55d6188633aa7be7c">4043802</a>. Au total, 153 037 ETH ont été détournés des Multisig de æternity, Edgeless Casino, et Swarm City par ce  <a href="https://etherscan.io/address/0xb3764761e297d6f121e79c32a65829cd1ddb4d32">compte</a>.

[gallery ids="2909,2910,2911"]

Hasard ou coïncidence, les 3 compagnies concernées arborent un signe infini dans leur logo tandis que 596 Multisigs étaient vulnérables.

&nbsp;
<h2>La réaction de la communauté</h2>
Au bloc <a href="https://etherscan.io/tx/0x00551b69995fdabb1ae8fc650bee038aecfdeeb2462f97c9c466cdcd4891632f">4044981</a>, soit un peu moins de 5 heures après la dernière transaction de l'attaquant, un groupe de White Hat Hacker a pris l'initiative de vider les autres contrats buggés. Ce groupe a par la suite redéployer des contrats mis à jour de multisig avec les paramètres initiaux et les fonds prélevés

Question en suspens, pourquoi n'avoir attaqué que ces 3 contrats ? En effet, les autres comptes vulnérables possédaient près de 78 million de dollars en tokens et plus de 377,105 ETH. Aversion particulière pour le signe ∞ ? Peur d'une fork ? Le mystère reste entier.

&nbsp;
<h2>Comment cette attaque aurait pu être évitée</h2>
L'utilisation des librairies n'est pas à écarter, bien au contraire. Outre le fait qu'elles permettent d'économiser le coût de stockage dans la blockchain, elles viennent aussi avec leur lot de tests, de standardisation et d'optimisation. Le problème ici est d'éviter que l'initialisation soit invoquée postérieurement au déploiement. On peut citer au moins deux approches pour éviter cela:
<ul>
	<li>retirer la fonction initWallet de la librairie pour l'intégrer dans le contrat Wallet <strong>sans oublie</strong>r de lui ajouter un modifier <em>internal;</em></li>
	<li>ajouter un modifier rejetant les transactions en direction du Wallet qui invoquent initWallet (solution choisie par Parity Technologies).</li>
</ul>
[caption id="attachment_2933" align="alignnone" width="1000"]<img class="alignnone size-full wp-image-2933" src="https://www.ethereum-france.com/wp-content/uploads/2017/10/portrait-of-two-friends.jpg" alt="Jacopo da Pontormo - Portrait de deux amis 1524" width="1000" height="1274" /> Jacopo da Pontormo - Portrait de deux amis 1524[/caption]

&nbsp;
<h2>Protéger ses fonds en Multisig</h2>
Si vous cherchez des ressources en anglais sur ce bug, je vous recommande de cliquer <a href="https://medium.com/@codetractio/a-look-into-paritys-multisig-wallet-bug-affecting-100-million-in-ether-and-tokens-356f5ba6e90a">ici</a>, <a class="markup--anchor markup--p-anchor" href="https://blog.parity.io/the-multi-sig-hack-a-postmortem/" target="_blank" rel="nofollow noopener" data-href="https://blog.parity.io/the-multi-sig-hack-a-postmortem/">là</a>, <a class="markup--anchor markup--p-anchor" href="https://blog.zeppelin.solutions/on-the-parity-wallet-multisig-hack-405a8c12e8f7" target="_blank" rel="nofollow noopener" data-href="https://blog.zeppelin.solutions/on-the-parity-wallet-multisig-hack-405a8c12e8f7">là</a>, <a class="markup--anchor markup--p-anchor" href="https://medium.com/@raulk/dissecting-the-two-malicious-ethereum-messages-that-cost-30m-but-couldve-cost-100m-155e023a9500" target="_blank" rel="noopener" data-href="https://medium.com/@raulk/dissecting-the-two-malicious-ethereum-messages-that-cost-30m-but-couldve-cost-100m-155e023a9500">par ici</a> et <a class="markup--anchor markup--p-anchor" href="https://www.youtube.com/watch?v=VUH4gRDQYsA" target="_blank" rel="nofollow noopener" data-href="https://www.youtube.com/watch?v=VUH4gRDQYsA">par là</a>. Si vous souhaitez participer à la sécurisation d'un contrat multisig il y a actuellement une bounty ouvert pour des contributions sur <a href="https://github.com/danny-wu/MultiSigWallet/blob/master/BOUNTY.md">celui-ci</a>. Dérivé de Gnosis, ce dernier simplifie beaucoup le fonctionnement et prévoit un mode récupération après une période d'inactivité des autres signataires.

Au-delà des différents contrats Multisig évoqués supra, on peut citer la solution entreprise proposée récemment par Ledger, la startup française spécialisé dans les hardware wallets. Cette dernière a développé <a href="https://www.ledger.fr/fr/enterprise-solutions/">Ledger Vault</a> un produit modulable qui permet de faire du Multisig directement en hardware.

&nbsp;