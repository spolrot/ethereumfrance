---
ID: 1480
post_title: >
  uPort ou la gestion de l’identité par
  la blockchain
author: JdeTychey
post_excerpt: ""
layout: post
permalink: >
  https://www.ethereum-france.com/uport-ou-la-gestion-de-lidentite-par-la-blockchain/
published: true
post_date: 2016-09-27 22:19:29
---
Après avoir présenté son avancement à la DEVCon2, <strong><a href="https://uport.me/#home">uPort </a></strong>a gagné le prix de la meilleure application blockchain à l’International Blockchain Week. C’est l’occasion de détailler un peu plus le fonctionnement de ce qui pourrait bien devenir une interface privilégiée pour se servir des applications décentralisées sur Ethereum.

[caption id="attachment_1481" align="aligncenter" width="600"]<img class="wp-image-1481" src="https://www.ethereum-france.com/wp-content/uploads/2016/09/uport-wins-demo-day-2-1024x683.jpg" alt="photographie par les organisateur de l'événement" width="600" height="400" /> photographie par les organisateur de l'événement[/caption]
<ul style="list-style-type: circle;">
 	<li><strong>L’identité numérique , des contrôles contraignants qui ont amené la centralisation</strong></li>
</ul>
Dans un<strong><a href="https://www.ethereum-france.com/le-phenomene-pokemon-go-un-two-way-forward-avec-ethereum/"> article précédent</a></strong>, j’avais rappelé le modèle actuel de gestion de l’identité numérique, avec ses jetons d’identification donnés par différents fournisseurs en silo. Cette situation empêche toute approche holiste et détériore l’expérience utilisateur par la répétition des demandes de login et mot de passe. La sécurité pâtit doublement de ces répétitions. D’une part, lorsque les utilisateurs refusent l’authentification centralisée, ils sont tentés de se servir du même mot de passe pour de nombreux comptes différents. D’autre part, les fournisseurs d’identité centralisés comme Facebook ou Google permettent certes de diminuer la charge de login et mot de passe, mais ils deviennent des cibles d’autant plus intéressantes (« <i>honeypots of data</i> ») pour les hackers. Les attaques sont fréquentes, on peut citer pêle-mêle<a href="https://www.theguardian.com/technology/2016/aug/31/dropbox-hack-passwords-68m-data-breach"> dropbox</a>,<a href="http://www.wired.co.uk/article/linkedin-data-breach-find-out-included"> linkedin</a>,<a href="http://www.recode.net/2016/9/22/13012836/yahoo-is-expected-to-confirm-massive-data-breach-impacting-hundreds-of-millions-of-users"> yahoo</a>… Je vous recommande de faire un tour sur le site<strong><a href="https://haveibeenpwned.com/"> haveibeenpwned</a></strong> pour vérifier si votre email n’a pas été compromis. En outre, l’avènement de l’internet des objets va amplifier les conséquences de ces failles sécuritaires dans l’espace physique. Par exemple, la prise de contrôle à distance d’une voiture autonome est d’ores et déjà largement<strong><a href="http://www.theverge.com/2016/9/19/12985120/tesla-model-s-hack-vulnerability-keen-labs"> documentée</a></strong>.

Le fonctionnement de la blockchain est à l’inverse de la centralisation des mots de passe ; les utilisateurs sont entièrement responsables de la sécurité de leur compte par la préservation et la protection de leur clé privée. L’avantage de cette approche est que la mise en oeuvre d’une attaque visant à récupérer cette clé privée est potentiellement beaucoup moins intéressante économiquement que de s’en prendre à un serveur contenant des millions de mots de passe. Encore faut que les utilisateurs observent des mesures de précaution pour leur clé privée.
<ul style="list-style-type: circle;">
 	<li><strong>La gestion des clés privées, un problème inhérent à la Blockchain</strong></li>
</ul>
La blockchain utilise la cryptographie asymétrique pour gérer les identités avec un couple de clés publique et privée Ce n’est pas une technologie nouvelle mais les cryptomonnaies peuvent se targuer d’en avoir diffusé largement l’utilisation. Toute adresse utilisateur Ethereum est une clé publique exposée sur le réseau, elle est associée à une clé privée que l’utilisateur doit conserver et ne pas révéler. Toute transaction émise par une adresse sur Ethereum est authentifiée par une signature générée à partir de la clé privée de cette adresse. Il s’agit du principe même de fonctionnement de la blockchain décrit dans l’article original de Satoshi Nakamoto.

La responsabilité de la clé privée peut être difficile à gérer pour monsieur tout-le-monde. En effet, il faut prendre soin que cette clé privée ne soit pas dérobée ou égarée. Les utilisateurs avertis recommandent d’utiliser des dispositifs hardware dédiés sécurisés tel que le<strong><a href="https://www.ledgerwallet.com/products/12-ledger-nano-s"> Ledger Nano S</a></strong> (seul disponible actuellement pour Ethereum) pour la gestion des clés. L’idée derrière uPort est que ce problème critique de la conservation des clés peut être contourné par la blockchain. Pour se faire, uPort se sert de la blockchain comme une autorité de certification des identités où un smartcontract représente l’identité numérique d’un utilisateur tout en permettant la révocation et le remplacement des clés de cet utilisateur.

[caption id="attachment_1486" align="aligncenter" width="432"]<img class="size-full wp-image-1486" src="https://www.ethereum-france.com/wp-content/uploads/2016/09/janus.jpg" alt="Janus- Détail d'une peinture de L'église de Waltham Abbey (RU-Essex)" width="432" height="234" /> Janus - détail du plafond de l'église de Waltham Abbey (RU-Essex)[/caption]
<ul style="list-style-type: circle;">
 	<li><strong>uPort déploie un contrat d’identité numérique tolérant la perte des clés privées</strong></li>
</ul>
L’architecture uPort comprend trois éléments principaux : un smartcontract attestant l’identité de l’utilisateur, une application mobile pour que l’utilisateur communique avec le smartcontract, et des librairies pour les développeurs.

L’application mobile utilise la clé privée de l’utilisateur qui est stockée dans l’enclave sécurisée (TrustZone) du téléphone. Un smartcontract individualisé associe la clé publique de l’utilisateur à son identité. Si l’utilisateur perd son téléphone et n’a aucun moyen de récupérer sa clé privée, alors uPort permet à l’utilisateur d’associer une nouvelle clé publique grâce à l’intervention d’un quorum de personnes de confiance. Ces personnes de confiance sont définies par l’utilisateur et peuvent être des amis, membres de la famille, institutions…

<img class="aligncenter wp-image-1485 size-full" src="https://www.ethereum-france.com/wp-content/uploads/2016/09/pasted-image-0.png" alt="pasted-image-0" width="605" height="308" />

Lorsque l’utilisateur a besoin de s’identifier auprès d’un smartcontrat, l’application mobile relaie sa requête via un « Controller contract » qui se charge du contrôle d'accès. La requête est ensuite transmise au « Proxy contract » qui communique avec le smartcontract. L’identité de l’utilisateur est alors représentée par le Proxy contract qui permet d’ajouter une couche entre la clé privée et le smartcontract qui a besoin d’une authentification.

Que se passe-t-il si le téléphone est perdu ou cassé ?

<img class="aligncenter size-full wp-image-1484" src="https://www.ethereum-france.com/wp-content/uploads/2016/09/pasted-image-01.png" alt="pasted-image-01" width="604" height="450" />

L’utilisateur prévient ses personnes de confiance qui informent le « Controller contract » que l’utilisateur a changé d’adresse. Lorsque suffisamment de personnes de confiance ont confirmé la nouvelle adresse, le « Controller contract » se met à jour et l’authentification par uPort est à nouveau accessible sur l’application mobile.

Outre ce système de mise à jour des clés, le « Proxy contract » de uPort permet d’ajouter d’autres fonctionnalités comme une limite de dépense, ou encore de se servir de l’immutabilité de ce « Proxy contract » comme une référence dans un système de réputation.

uPort s’insèrera très bien dans les processus de vérification par les entreprises de l'identité de leurs clients (Know Your Customer – KYC ).  Ces processus sont issus d’obligations de mise en conformité avec les lois anti-corruption et anti-blanchiment des États. L’authentification par uPort permet donc d’inscrire les applications Ethereum dans les exigences légales du monde réel. D’autres acteurs entendent bien faire concurrence à uPort sur ce thème comme « BlockOne ID » chez Thomson Reuters.
<ul style="list-style-type: circle;">
 	<li><strong>          Un mécanisme d’authentification qui veut pouvoir s'appliquer partout où l’utilisateur en a besoin</strong></li>
</ul>
<img class="aligncenter size-large wp-image-1483" src="https://www.ethereum-france.com/wp-content/uploads/2016/09/pasted-image3-0-1024x541.png" alt="pasted-image3-0" width="1024" height="541" />

Une fois associé à une solution de stockage des données personnelles, uPort permettra à ses utilisateurs de choisir quel service accède à quelles données et éventuellement de révoquer cet accès à tout moment. Enfin, l’interaction dans la blockchain ouvre la possibilité pour les utilisateurs de monnayer leurs données et ainsi a minima de couvrir les coûts de transaction.

<img class="aligncenter size-large wp-image-1482" src="https://www.ethereum-france.com/wp-content/uploads/2016/09/pasted-image-4-0-1024x394.png" alt="pasted-image-4-0" width="1024" height="394" />

Si vous souhaitez en savoir plus, vous pouvez consulter la <strong><a href="https://uport.me/library/pdf/whitepaper.pdf">documentation technique</a></strong> d'où sont tirés les schémas ci-dessus.