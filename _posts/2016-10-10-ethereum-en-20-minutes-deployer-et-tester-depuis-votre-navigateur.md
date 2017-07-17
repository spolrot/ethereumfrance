---
ID: 1507
post_title: 'Ethereum en 20 minutes : déployer et tester depuis votre navigateur'
author: JdeTychey
post_excerpt: ""
layout: post
permalink: >
  https://www.ethereum-france.com/ethereum-en-20-minutes-deployer-et-tester-depuis-votre-navigateur/
published: true
post_date: 2016-10-10 18:36:45
---
<span style="font-weight: 400;">La blockchain Ethereum offre la possibilité d’héberger des programmes informatiques. Ces programmes sont donc qualifiés d’« applications décentralisées » puisque chacun des nœuds du réseau pair à pair Ethereum en conserve une copie et l’exécute à la demande. Sur Ethereum ces programmes sont aussi appelés des contrats (ou smartcontracts) en référence notamment au fait que le code du programme et son exécution sont publics.</span>

<span style="font-weight: 400;">Dans ce tutoriel nous allons déployer un contrat puis interagir avec cette application décentralisée (dapp) directement depuis le navigateur Google Chrome (et prochainement depuis Firefox). Pour cela nous allons nous servir de deux outils, Metamask et le Browser-Solidity. En une vingtaine de minutes vous allez vous créer un compte Ethereum avec Metamask (installé en 1.), abonder ce compte en ethers de test (gratuitement en 2.) pour déployer et interagir avec un programme écrit dans le Browser-Solidity (étapes 3 et 4).</span>

[caption id="attachment_1534" align="aligncenter" width="384"]<img class="size-full wp-image-1534" src="https://www.ethereum-france.com/wp-content/uploads/2016/10/rsz_768px-domenico-fetti_archimedes_1620.jpg" alt="Archimède Domenico Fetti, 1620, Musée Alte Meister, Dresde" width="384" height="512" /> Archimède Domenico Fetti, 1620, Musée Alte Meister, Dresde[/caption]
<ol>
 	<li><b></b> <strong>Etape 1 : Installer Metamask</strong></li>
</ol>
<span style="font-weight: 400;">Le plugin Chrome Metamask est distribué par une équipe de Consensys composée notamment d’</span><strong><a href="https://twitter.com/kumavis_">Aaron Davis</a></strong><span style="font-weight: 400;"> et</span><strong><a href="https://twitter.com/danfinlay"> Dan Finlay</a></strong><span style="font-weight: 400;">. Metamask permet d’envoyer des transactions sur le réseau Ethereum depuis Chrome sans avoir de nœud Ethereum sur son ordinateur. Metamask prépare une version de son plugin pour Firefox et le présent tutoriel sera mis-à-jour quand il sera disponible.
</span>

<span style="font-weight: 400;">Pour ajouter Metamask à Chrome c’est par ici :</span>

<strong><a href="https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn">https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn</a></strong>

<img class="aligncenter wp-image-1517 size-full" src="https://www.ethereum-france.com/wp-content/uploads/2016/10/2.png" alt="2" width="266" height="105" />

<span style="font-weight: 400;">Au lancement de </span><strong><span style="color: #ff0000;">Metamask</span> </strong><span style="font-weight: 400;">:</span>

<span style="font-weight: 400;">-</span><span style="font-weight: 400;">          </span><span style="font-weight: 400;">Cliquez sur « <strong><span style="color: #ff0000;">create a new vault</span></strong> » pour générer un compte Ethereum</span>

<img class="aligncenter size-full wp-image-1518" src="https://www.ethereum-france.com/wp-content/uploads/2016/10/metamask-wallet.png" alt="metamask-wallet" width="702" height="389" />

<span style="font-weight: 400;">-</span><span style="font-weight: 400;">         </span><span style="font-weight: 400;">Choisissez un mot de passe pour votre compte</span>

<img class="aligncenter wp-image-1516 size-full" src="https://www.ethereum-france.com/wp-content/uploads/2016/10/3.png" alt="3" width="217" height="301" />

<span style="font-weight: 400;">-</span><span style="font-weight: 400;">    </span><span style="font-weight: 400;">Metamask génère alors 12 mots associés à votre compte et permettant de récupérer votre compte si vous perdez votre mot de passe ou votre ordinateur. Notez cette liste de mots quelque part et stockez la en sécurité (autre méthode : apprendre ces mots par cœur). Elle permet d’utiliser la fonction « Restore existing vault » de Metamask.</span>

<img class="aligncenter size-full wp-image-1515" src="https://www.ethereum-france.com/wp-content/uploads/2016/10/4a.png" alt="4a" width="251" height="347" />

<span style="font-weight: 400;">Une fois votre compte créé, vous constaterez que Metamask est connecté sur le Testnet « </span><span style="font-weight: 400;">Morden </span><span style="font-weight: 400;">» dans le coin en haut à droite et que vous avez 0 ether. Morden est une blockchain de test maintenue par la communauté Ethereum, de nombreux smart-contracts y sont déployés avant leur mise en production.</span>

<span style="font-weight: 400;">En cliquant sur « Testnet » vous pouvez changer de réseau et ainsi communiquer avec le livenet (c’est-à-dire la blockchain publique ethereum, celle où les ethers ETH sont cotés sur les exchanges comme </span><strong><a href="https://dwq4do82y8xi7.cloudfront.net/widgetembed/?symbol=ETHEUR&amp;interval=D&amp;symboledit=1&amp;toolbarbg=f1f3f6&amp;hideideas=1&amp;studies=&amp;theme=White&amp;style=1&amp;timezone=exchange">Kraken</a></strong><span style="font-weight: 400;">), ou encore une blockchain locale… Pour ce tutoriel nous resterons sur le Testnet, cette blockchain est publique et dispose de plusieurs exploreurs, essayez celui-ci :</span>

<strong><a href="https://testnet.etherscan.io/">https://testnet.etherscan.io/</a></strong>

<span style="font-weight: 400;">Si vous collez l’adresse de votre compte dans la barre de recherche en haut à droite vous pouvez suivre votre historique et retrouver diverses informations. Parmi ces informations, vous avez notamment le solde de votre adresse : zéro, nous allons remédier à cela en 2.</span>

&nbsp;
<ol start="2">
 	<li><b></b> <strong>Etape 2 : recevoir gratuitement des ethers du Testnet</strong></li>
</ol>
<img class="aligncenter size-full wp-image-1514" src="https://www.ethereum-france.com/wp-content/uploads/2016/10/5.png" alt="5" width="252" height="351" />

<span style="font-weight: 400;">Cliquez sur l’icon de renard Metamask puis sur « <strong><span style="color: #ff0000;">buy</span> </strong>», « <span style="color: #ff0000;"><strong>go to Test Faucet</strong></span> » et enfin « <strong><span style="color: #ff0000;">Request 1 ether from the faucet</span></strong> ». Après quelques instants votre adresse sera créditée d’1 ether ce qui est suffisant pour le reste du tutoriel.</span>

<span style="font-weight: 400;">Vous pouvez également vérifier le changement de votre solde sur l’exploreur <strong><a href="https://testnet.etherscan.io/">etherscan</a> </strong>cité supra. Il est temps de déployer un contrat.</span>

&nbsp;
<ol start="3">
 	<li><b></b> <strong>Ecrire un contrat dans le Browser-Solidity</strong></li>
</ol>
<span style="font-weight: 400;">Le Browser-Solidity est un compileur Solidity et un environnement de développement intégré (IDE) conçu par la Fondation Ethereum. Vous pouvez en découvrir les arcanes</span><a href="https://github.com/ethereum/browser-solidity"> <span style="font-weight: 400;">ici</span></a><span style="font-weight: 400;">, mais pour le moment nous nous contenterons de cette adresse :</span>

<strong><a href="https://ethereum.github.io/browser-solidity">https://ethereum.github.io/browser-solidity</a></strong>
<img class="aligncenter size-full wp-image-1513" src="https://www.ethereum-france.com/wp-content/uploads/2016/10/6.png" alt="6" width="253" height="165" />

&nbsp;
<p style="text-align: left;"><span style="font-weight: 400;">A l’ouverture, Browser-Solidity contient un contrat par défaut appelé « Ballot », nous n’allons pas nous en servir aujourd’hui. De manière général l’environnement peut sembler compliqué mais nous aurons l’occasion de passer en revue les différentes fonctionnalités ultérieurement. Cliquez en haut à gauche sur « </span><strong><span style="color: #ff0000;">new file</span></strong><span style="font-weight: 400;"> » et collez le code suivant, il s'agit d'un contrat simple permettant de stocker une chaîne de caractères dans la blockchain :</span></p>
<p style="text-align: left;"><!-- HTML generated using hilite.me --></p>

<div style="background: #eeeedd; overflow: auto; width: auto; border: solid gray; border-width: .1em .1em .1em .8em; padding: .2em .6em;">
<table>
<tbody>
<tr>
<td style="text-align: left;">
<pre style="margin: 0; line-height: 125%;"> 1
 2
 3
 4
 5
 6
 7
 8
 9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
48
49</pre>
</td>
<td style="text-align: left;">
<pre style="margin: 0; line-height: 125%;">pragma solidity ^<span style="color: #b452cd;">0.4</span>.<span style="color: #b452cd;">2</span>;
<span style="color: #228b22;">/*'pragma' indique au compileur dans quelle version de Solidity ce code est écrit */</span>
contract storer {
<span style="color: #228b22;">/*'contract' indique le début du contrat a proprement parler 'contract' est similaire</span>
<span style="color: #228b22;">à 'class' dans d'autres langages (class variables, inheritance, etc.)*/</span>
address <span style="color: #8b008b; font-weight: bold;">public</span> owner;
string <span style="color: #8b008b; font-weight: bold;">public</span> log;
<span style="color: #228b22;">/* Les deux lignes précédentes déclarent les variables du contrat et leur type</span>
<span style="color: #228b22;">'owner' est une adresse ethereum et est publique (on peut la lire publiquement</span>
<span style="color: #228b22;">dans la blockchain)</span>
<span style="color: #228b22;">'log' est une chaîne de caractères de taille indéfinie et est publique */</span>
<span style="color: #8b008b; font-weight: bold;">function</span> storer() {
    owner = msg.sender ;
}
<span style="color: #228b22;">/* 'storer' est une fonction un peu particulière, il s'agit du constructeur du contrat.</span>
<span style="color: #228b22;">Cette fonction s'exécute une seule fois au moment de la création du contrat.</span>
<span style="color: #228b22;">La création du contrat est une transaction et comme toute transaction elle est</span>
<span style="color: #228b22;">représentée en Solidity par "msg", "msg.sender" correspond  à l'adresse qui</span>
<span style="color: #228b22;">émet cette transaction.  </span>
<span style="color: #228b22;">A la création du contrat la variable owner reçoit l'adresse qui a déployé le</span>
<span style="color: #228b22;">contrat */</span>
modifier onlyOwner {
        <span style="color: #8b008b; font-weight: bold;">if</span> (msg.sender != owner)
            <span style="color: #8b008b; font-weight: bold;">throw</span>;
        _;
    }
<span style="color: #228b22;">/* le 'modifier' permet de poser des conditions à l'exécution des fonctions.</span>
<span style="color: #228b22;">Ici, 'onlyOwner' sera ajouté à la syntaxe des fonctions que l'on</span>
<span style="color: #228b22;">veut réserver au 'owner'. Le modifier teste la condion msg.sender != owner</span>
<span style="color: #228b22;">si le requêteur de la fonction n'est pas le owner alors l'exécution</span>
<span style="color: #228b22;">s'interrompt, c'est le sens du 'throw'; s'il s'agit bien du owner alors</span>
<span style="color: #228b22;">la fonction s'exécute. Notez le '_' underscore après le test, il signifie</span>
<span style="color: #228b22;">à la fonction de continuer son exécution.*/</span>    
<span style="color: #8b008b; font-weight: bold;">function</span> store(string _log) onlyOwner() {
    log = _log;
}
<span style="color: #228b22;">/*La fonction 'store' reçoit une chaîne de caractères qu'elle associe à une</span>
<span style="color: #228b22;">variable d'état '_log'. Cette fonction n'est utilisable que par l'adresse qui</span>
<span style="color: #228b22;">est 'owner', si c'est bien cette adresse qui fait la requête alors la variable</span>
<span style="color: #228b22;">'log' devient '_log'.*/</span>
<span style="color: #8b008b; font-weight: bold;">function</span> kill() onlyOwner() {
  selfdestruct(owner); }
<span style="color: #228b22;">/* Cette dernière fonction permet de "nettoyer" la blockchain en supprimant le</span>
<span style="color: #228b22;">contrat. Il est important de la faire figurer pour libérer de l'espace sur</span>
<span style="color: #228b22;">la blockchain mais aussi pour supprimer un contrat buggé. En précisant une</span>
<span style="color: #228b22;">adresse selfdestruct(address), tous les ethers stockés par le contrat y sont</span>
<span style="color: #228b22;">envoyés. Attention si une transaction envoie des ethers à un contrat qui s'est</span>
<span style="color: #228b22;">"selfdestruct" ces ethers seront perdus*/</span>
}
</pre>
</td>
</tr>
</tbody>
</table>
</div>
<span style="font-weight: 400;">Les commentaires en vert décrivent explicitement les lignes du code, s’ils ne sont pas assez clairs ne vous en faites pas car le déploiement et l’utilisation des fonctions devraient répondre à vos questions. </span>

<span style="font-weight: 400;">Avant de passer à l’étape 4, cliquez sur l’icône </span><strong><span style="color: #ff0000;">cube</span> </strong><span style="font-weight: 400;">en haut à gauche et vérifiez que l’option «</span><strong><span style="color: #ff0000;"> Injected Web3</span></strong><span style="font-weight: 400;"> » est bien cochée puis cliquez sur l’icône </span><span style="color: #99cc00;"><strong>paramètres</strong></span><span style="font-weight: 400;"> pour revenir à l’interface précédente.</span>

<img class="aligncenter size-full wp-image-1512" src="https://www.ethereum-france.com/wp-content/uploads/2016/10/7.png" alt="7" width="339" height="346" />

&nbsp;
<ol start="4">
 	<li><strong>Déployer et interagir avec le programme</strong></li>
</ol>
<span style="font-weight: 400;">Cliquez sur le bouton rouge « </span><strong><span style="color: #ff0000;">create</span> </strong><span style="font-weight: 400;">», une transaction Metamask va être générée et un pop-up Metamask devrait s’ouvrir. Entrez votre mot de passe et </span><span style="font-weight: 400; color: #00ff00;"><strong>acceptez</strong> </span><span style="font-weight: 400;">cette transaction.</span>

<img class="aligncenter size-full wp-image-1511" src="https://www.ethereum-france.com/wp-content/uploads/2016/10/8.png" alt="8" width="604" height="366" />

<span style="font-weight: 400;">Cette transaction une fois minée va déployer le code à une adresse sur la blockchain Ethereum Testnet. Cette adresse est automatiquement récupérée par le Browser-Solidity qui va de plus générer une interface basique pour ce contrat. Vous pouvez retrouver l’adresse de votre application décentralisée en cherchant dans les détails de la transaction de création dans l’exploreur </span><a href="https://testnet.etherscan.io/"><span style="font-weight: 400;">etherscan</span></a><span style="font-weight: 400;"> par exemple.</span>

<img class="aligncenter size-full wp-image-1510" src="https://www.ethereum-france.com/wp-content/uploads/2016/10/9.png" alt="9" width="289" height="415" />

<span style="font-weight: 400;">Vous retrouvez en bleu les variables publiques définies à savoir « </span><strong><span style="color: #3366ff;">owner</span> </strong><span style="font-weight: 400;">» avec votre adresse et « </span><strong><span style="color: #3366ff;">log</span> </strong><span style="font-weight: 400;">» ou il n’y a rien de stocké pour le moment. En rouge se trouvent les fonctions du contrat à l’exception du constructeur, attention à ne pas lancer « </span><span style="font-weight: 400;">kill </span><span style="font-weight: 400;">» tout de suite.</span>

<span style="font-weight: 400;">Dans la case à côté de « </span><strong><span style="color: #00ff00;">store</span> </strong><span style="font-weight: 400;">» entrez le message de votre choix entre guillemets, par exemple :</span>
<p style="text-align: center;"><span style="font-size: 14pt;"><b>"Ethereum j’adore, à l’Asseth j’adhère"</b></span></p>
<span style="font-weight: 400;">Puis cliquez sur le bouton « <strong><span style="color: #00ff00;">store</span> </strong>», ceci va générer une nouvelle transaction Metamask… Attendez quelques secondes que la transaction soit minée, et rafraîchissez la valeur de <strong><span style="color: #3366ff;">log</span> </strong>en cliquant sur le bouton bleu correspondant.</span>

<span style="font-weight: 400;">Votre message est stocké ! Vous pouvez le modifier en réutilisant la fonction store mais n’oubliez pas les guillemets.</span>

&nbsp;

<span style="font-weight: 400;">J’espère que ce tutoriel vous a donné envie de déployer et de tester d’autres contrats, sachez qu’il y a des ressources en ligne en anglais assez nombreuses sur le sujet</span><strong><a href="http://solidity.readthedocs.io/en/develop/solidity-by-example.html"> ici</a></strong><span style="font-weight: 400;">,</span><strong><a href="https://ethereumbuilders.gitbooks.io/guide/content/en/solidity_tutorials.html"> là</a></strong><span style="font-weight: 400;"> ou encore</span><strong><a href="https://dappsforbeginners.wordpress.com/"> là</a></strong><span style="font-weight: 400;">… Mais surtout, il y a l’Asseth, une association loi 1901 de passionnés d’Ethereum qui peuvent répondre à toutes vos questions sur le slack</span><strong><a href="https://asseth.slack.com/"> https://asseth.slack.com/</a></strong><span style="font-weight: 400;"> (réservé aux adhérents pour le moment).</span>

<img class="aligncenter size-full wp-image-1539" src="https://www.ethereum-france.com/wp-content/uploads/2016/10/19.jpg" alt="19" width="242" height="178" /><span style="font-weight: 400;">L’Asseth organise des ateliers de découverte, de code et de rencontre pour fédérer les initiatives et diffuser les connaissances sur Ethereum. Vous pouvez d’ores et déjà vous inscrire au prochain rendez-vous de l’Asseth, le samedi 15 octobre pour<a href="http://www.meetup.com/fr-FR/blockchains/events/234758385/?eventId=234758385"><strong> un meetup de présentation et de discussion au studio Abel14</strong></a>. Si vous souhaitez soutenir les initiatives de l'Asseth, vous pouvez y adhérer ou faire un don <a href="https://www.helloasso.com/associations/asseth/adhesions/adhesion-a-l-asseth"><strong>en visitant ce lien</strong></a>.</span>

&nbsp;