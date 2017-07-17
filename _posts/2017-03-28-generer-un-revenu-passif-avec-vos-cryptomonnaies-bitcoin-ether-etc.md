---
ID: 2096
post_title: >
  Générer un revenu passif avec vos
  cryptomonnaies (bitcoin, ether, etc.)
author: Marc Zeller
post_excerpt: ""
layout: post
permalink: >
  https://www.ethereum-france.com/generer-un-revenu-passif-avec-vos-cryptomonnaies-bitcoin-ether-etc/
published: true
post_date: 2017-03-28 16:30:41
---
Sur certaines plateformes d'échange, il est possible de prêter vos cryptomonnaies à des traders pour que ceux-ci jouent à la hausse ou à la baisse sur le cours d'un actif, avec un effet de levier permis par votre prêt. Ces prêts sont généralement très bien rémunérés par les emprunteurs. Il est donc possible de vous constituer un "revenu passif" par ce biais. L’objectif de l’article n’est pas de vous faire un cours de finance, mais de vous fournir une méthode étape par étape pour automatiser et optimiser ce processus pouvant vous générer de nouvelles unités de monnaie.

<strong><em>Avant propos : L’auteur de l’article possède des unités de crypto-monnaies différentes, n’a aucun partenariat ni liens avec l’exchange Poloniex. Il n’existe pas de revenu sans risque et/ou travail tout personne vous présentant les choses différemment est en train d’essayer de vous voler votre argent. Ici il y a deux risques forts à considérer avec attention : la chute de l’exchange (l’histoire de la crypto-monnaie nous a démontré que ce risque est non-nul) et le fait que votre argent est “bloqué” pendant au moins deux jours en cas de chute brutale du cours de la monnaie concernée, détruisant tout vos gains et la possibilité de limiter vos pertes. Nous ne pouvons qu’encourager nos lecteurs à une gestion responsable de leur capital et de ne jamais investir tous leurs actifs dans le même investissement.</em></strong>

Si la procédure peut sembler fastidieuse sachez que vous en avez pour 10 min et que vous n’aurez presque plus rien à faire par la suite.

<strong>Attention, si vous utilisez cette méthode, de part sa nature de “crédits” il faudra théoriquement jusqu’à 48h pour disposer de vos fonds le jour ou vous souhaitez arrêter.</strong>

Cette méthode est sans frais, le seul coût sera le risque pris (voir le début de l’article) ainsi que le temps que vous y avez consacré. Du fait de sa présence importante sur le parc informatique cette méthode est destinée aux utilisateurs de Windows, les petits malins de Linux n'ont certainement pas besoin de nous mais si la demande est forte, nous pourrons éventuellement faire une version  adapté aux utilisateurs macOS.

<strong>Dernier point : suivez scrupuleusement l’ensemble de ces étapes, en effet, il y a votre argent en jeu, une petite case mal cochée est un risque que vous ne voulez pas prendre.</strong>
<h1>De quoi on a besoin ?</h1>
<ul>
 	<li>un compte chez Poloniex : <a href="https://poloniex.com/signup">c'est par là !</a></li>
 	<li>un ordinateur (oui, oui… un clavier et une connexion internet, tu veux pas dire un écran aussi ?)</li>
 	<li>un compte chez AWS : <a href="https://www.amazon.com/ap/signin?openid.assoc_handle=aws&amp;openid.return_to=https%3A%2F%2Fsignin.aws.amazon.com%2Foauth%3Fresponse_type%3Dcode%26client_id%3Darn%253Aaws%253Aiam%253A%253A015428540659%253Auser%252Fawssignupportal%26redirect_uri%3Dhttps%253A%252F%252Fportal.aws.amazon.com%252Fbilling%252Fsignup%253Flanguage%253Dfr_fr%2526nc2%253Dh_ct%2526redirect_url%253Dhttps%25253A%25252F%25252Faws.amazon.com%25252Fregistration-confirmation%2526state%253DhashArgs%252523%2526isauthcode%253Dtrue%26noAuthCookie%3Dtrue&amp;openid.mode=checkid_setup&amp;openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0&amp;openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;action=&amp;disableCorpSignUp=&amp;clientContext=&amp;marketPlaceId=&amp;poolName=&amp;authCookies=&amp;pageId=aws.ssop&amp;siteState=registered%2Cfr_FR&amp;accountStatusPolicy=P1&amp;sso=&amp;openid.pape.preferred_auth_policies=MultifactorPhysical&amp;openid.pape.max_auth_age=120&amp;openid.ns.pape=http%3A%2F%2Fspecs.openid.net%2Fextensions%2Fpape%2F1.0&amp;server=%2Fap%2Fsignin%3Fie%3DUTF8&amp;accountPoolAlias=&amp;forceMobileApp=0&amp;language=fr_FR&amp;forceMobileLayout=0">c'est ici !</a> (à noter si vous êtes clients chez amazon vous avez déjà un compte chez AWS)</li>
 	<li>des sous : <a href="http://www.pole-emploi.fr/accueil/">par ici ! </a></li>
</ul>
<h1>Etape 1 : Préparation de votre compte sur Poloniex</h1>
<ol>
 	<li>Transférez sur votre compte “lending” la somme que vous souhaitez mettre à disposition (onglet balances puis transfert balances)</li>
 	<li>Générez une clé API de votre compte poloniex</li>
</ol>
<img class="aligncenter size-medium wp-image-2101" src="https://www.ethereum-france.com/wp-content/uploads/2017/03/Lending-image00-4-300x110.jpg" alt="" width="300" height="110" />

Vous allez générer une autorisation pour qu’un programme se connecte et fasse des choses sur votre compte (ça vous fait peur ? vous avez raison ! suivez avec attention cette étape)
<ul>
 	<li>Dans l’onglet “outil” cliquez sur “API KEYS”</li>
 	<li>Cliquez sur Enable API, oui le gros bouton jaune :<img class="aligncenter size-medium wp-image-2097" src="https://www.ethereum-france.com/wp-content/uploads/2017/03/Lending-image00-1-300x151.jpg" alt="" width="300" height="151" /></li>
</ul>
<p style="padding-left: 30px;">(vous allez devoir entrer votre 2fa et valider un lien reçu par e-mail, si ce n’est pas le cas, vous prenez votre sécurité à la légère !)</p>

<ul>
 	<li>Cliquez sur Show et sélectionnez “<em>Unrestricted (less secure)</em>” (d’où l’importance de ce qui va suivre :)</li>
</ul>
<p style="padding-left: 30px;"><strong>!!! NE COCHEZ PAS “ENABLE TRADING” ET “ENABLE WITHDRAWALS” !!!</strong> (ne risquez pas votre argent</p>

<ul>
 	<li>Notez votre “Api-Key” et votre “Secret” quelque part vous en aurez bientôt besoin. (Ne communiquez ces informations à personne !)</li>
</ul>
<h1>Etape 2 : Créer votre instance EC2</h1>
A cette étape nous allons vous créer un serveur dans un datacenter chez Amazon qui fonctionnera 24h/24 (c’est pas tout à fait cela mais si vous voulez en apprendre plus sur les VPS, internet est votre ami)
<ul>
 	<li>Connectez vous à AWS (<a href="https://aws.amazon.com/fr/console/">c'est ici pour les gens perdus</a>)</li>
</ul>
<p style="padding-left: 60px;">AWS n’est pas réputé pour être gentil avec les personnes non-techniques, pas d’inquiétudes, suivez le guide!</p>

<ul>
 	<li>Sélectionnez “Launch a Virtual Machine” et faites “Get Started” (gros bouton bleu)<img class="aligncenter size-medium wp-image-2099" src="https://www.ethereum-france.com/wp-content/uploads/2017/03/Lending-image00-2-300x168.jpg" alt="" width="300" height="168" /></li>
 	<li>Sélectionnez les options suivantes, et appuyez sur “Download” (puis confirmez), un petit fichier en .pem va être téléchargé. cliquez désormais sur “Create this instance”</li>
</ul>
<img class="aligncenter wp-image-2105 size-medium" src="https://www.ethereum-france.com/wp-content/uploads/2017/03/Lending-image00-8-300x245.jpg" alt="" width="300" height="245" />
<p style="padding-left: 60px;">Votre serveur est en train de naître. si comme moi vous lui avez donné un nom intelligent, bravo ! Cela prendra moins de 5 minutes. cliquez sur “Proceed to EC2 console” dès que c’est prêt.</p>
<p style="padding-left: 60px;"><img class="aligncenter size-medium wp-image-2111" src="https://www.ethereum-france.com/wp-content/uploads/2017/03/Lending-image00-14-300x155.jpg" alt="" width="300" height="155" /></p>
<p style="padding-left: 60px;">Vous êtes perdus ? pas d’inquiétudes c’est dernière fois que vous regardez cette page ! Copiez simplement ce qui est indiqué à “Public DNS”</p>
<img class="aligncenter size-medium wp-image-2106" src="https://www.ethereum-france.com/wp-content/uploads/2017/03/Lending-image00-9-300x118.jpg" alt="" width="300" height="118" />
<h1>Etape 3 : Télécharger et configurer Putty</h1>
Pour télécharger Putty &amp; PuttyGen <a href="http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html">c'est par là !</a>
<ul>
 	<li>Lancez PuttyGen, cliquez sur load et allez chercher le petit fichier en .pem (pensez à sélectionner “all files” pour qu’il soit visible).</li>
 	<li>Déterminez un mot de passe complexe (si vous n’avez pas d’idée : <a href="https://strongpasswordgenerator.com/">un coup de main</a>)</li>
 	<li>Cliquez sur “Save Private Key” et donnez le même nom à ce fichier qu’au fichier précédent. vous avez désormais un petit fichier .ppk (dans notre cas prout.ppk)</li>
</ul>
<img class="aligncenter size-medium wp-image-2107" src="https://www.ethereum-france.com/wp-content/uploads/2017/03/Lending-image00-10-300x296.jpg" alt="" width="300" height="296" />

C’est fini pour PuttyGen nous passons désormais à la dernière étape !
<ul>
 	<li>Lancez Putty</li>
</ul>
&nbsp;
<ul>
 	<li>Dans “Host Name” indiquez ubuntu@ et copiez-collez votre “Public DNS” (Que vous avez noté à la fin de l’étape 2)<img class="aligncenter size-medium wp-image-2112" src="https://www.ethereum-france.com/wp-content/uploads/2017/03/Lending-image00-15-300x292.jpg" alt="" width="300" height="292" /></li>
 	<li>Cliquez ensuite sur “SSH” puis sur “AUTH”. Cliquez sur “Browse” et allez chercher le petit fichier .ppk (ne pas confondre avec le .pem)</li>
</ul>
<img class="aligncenter size-medium wp-image-2102" src="https://www.ethereum-france.com/wp-content/uploads/2017/03/Lending-image00-5-300x293.jpg" alt="" width="300" height="293" />
<ul>
 	<li>Retournez sur “Session”. Donnez un nom dans “Saved sessions” puis cliquez sur “Save” (grâce à cela tout n’est pas à recommencer à chaque fois!)</li>
 	<li>Il ne vous reste plus qu’à cliquer sur “Open” (dites oui à l’avertissement qui s’ouvre) entrez votre mot de passe. (si vous voulez aller faire une pause c’est le moment !)</li>
</ul>
<h1>Etape 4 (la dernière promis !) : Configurer votre lendingbot</h1>
<em>(astuce : dans Putty un clic-droit = un copié-collé !)</em>

Validez chaque ligne avec la touche "entrée".
<ul>
 	<li>Ecrivez : “sudo apt-get install git tmux” (sans les guillemets !)<a href="https://www.ethereum-france.com/wp-content/uploads/2017/03/Lending-image00-11.jpg"><img class="aligncenter wp-image-2108 size-full" src="https://www.ethereum-france.com/wp-content/uploads/2017/03/Lending-image00-11.jpg" alt="" width="659" height="420" /></a></li>
 	<li>Puis “y” pour confirmer.</li>
 	<li>Ecrivez : “tmux”</li>
 	<li>Ecrivez : “git clone <a href="https://github.com/Mikadily/poloniexlendingbot">https://github.com/Mikadily/poloniexlendingbot</a>”<img class="aligncenter wp-image-2110 size-full" src="https://www.ethereum-france.com/wp-content/uploads/2017/03/Lending-image00-13.jpg" alt="" width="661" height="415" /></li>
 	<li>Puis : “cd poloniexlendingbot/”</li>
 	<li>Enfin : “python lendingbot.py"
Le petit fichier default.cfg vient d’être créé, il va vous permettre de configurer votre bot.</li>
</ul>
<img class="aligncenter wp-image-2098 size-full" src="https://www.ethereum-france.com/wp-content/uploads/2017/03/Lending-image00-1.png" alt="" width="655" height="397" />
<ul>
 	<li>Ecrivez : “nano default.cfg”Pour naviguer dans le fichier il vous suffit d’utiliser les flèches de votre clavier. attention Ctrl-C n’est pas un copié-collé dans ce cas, faites simplement un clic-droit.<a href="https://www.ethereum-france.com/wp-content/uploads/2017/03/Lending-image00-3.jpg"><img class="aligncenter wp-image-2100 size-large" src="https://www.ethereum-france.com/wp-content/uploads/2017/03/Lending-image00-3-1024x531.jpg" alt="" width="1024" height="531" /></a></li>
</ul>
&nbsp;
<ul>
 	<li>Remplacez “YourAPIKey” et “YourSecret” par les valeurs que vous avez noté à l’étape 1 (sans les guillemets !)</li>
 	<li>Remplacez “3” par “20”</li>
 	<li>Le “0.04” représente le pourcentage minimum auquel vous souhaitez “faire crédit” ceci est à votre discrétion, il est à noter que ce sont des taux journaliers si cette valeur est trop élevée vous risquez de voir les trader bouder vos offres.</li>
 	<li>Une fois que vous avez faits vos choix faites “Ctlr+O” puis “Entrée”
et enfin “Ctrl + x”</li>
 	<li>Dernière étape : écrivez “python lendingbot.py”<img class="aligncenter wp-image-2104 size-full" src="https://www.ethereum-france.com/wp-content/uploads/2017/03/Lending-image00-7.jpg" alt="" width="700" height="139" /></li>
</ul>
…et Voilà ! vous avez un serveur autonome qui fait crédit de vos sous à des traders contre rémunération.

Ca ne marche pas ? vous avez loupé une étape ! Relisez attentivement le guide.

<hr />

<h1>Et ensuite ?</h1>
<strong>Pour stopper vos crédits :</strong>
<ul>
 	<li>relancez putty, “load”, votre profil puis “open”</li>
 	<li>écrivez “tmux attach -t 0”
puis faites ctrl+C</li>
</ul>
Comme prévu vos fonds seront disponibles dans 48h maximum.

<strong>Pour relancer vos crédits :</strong>
<ul>
 	<li>encore putty, “load”, votre profil et “open”</li>
 	<li>écrivez “tmux attach -t 0”</li>
 	<li>puis faites “python lendingbot.py”</li>
</ul>