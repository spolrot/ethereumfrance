---
ID: 1309
post_title: >
  Sécuriser vos ethers (ETH) ou autres
  cryptomonnaies
author: Simon Polrot
post_excerpt: ""
layout: post
permalink: >
  https://www.ethereum-france.com/securiser-vos-ethers-eth-ou-autres-cryptomonnaies/
published: true
post_date: 2016-08-22 11:32:37
---
<strong>Après le <span style="text-decoration: underline;"><a href="http://www.nextinpact.com/news/100914-bitfinex-apres-vol-119-756-bitcoins-clients-en-seront-leur-poche.htm">piratage retentissant de la plateforme d'échange Bitfinex</a></span>, qui a récemment perdu 119 756 bitcoins (plus de 60 millions d’euros), un point s’impose sur la façon de sécuriser vos cryptomonnaies. Le vol ou la perte d'actifs virtuels n'est pas un événement hypothétique... Aperçu des moyens les plus simples de limiter vos risques.</strong>

Il existe aujourd’hui plusieurs degrés de sécurité, chaque degré entraînant davantage de contraintes à l’utilisation :

[caption id="attachment_1313" align="alignright" width="300"]<img class="wp-image-1313 size-medium" src="https://www.ethereum-france.com/wp-content/uploads/2016/08/Sécuriser-crypto-300x141.png" alt="Quelle méthode utiliser pour sécuriser vos ethers ?" width="300" height="141" /> Il existe plusieurs méthodes pour sécuriser vos ethers.[/caption]
<ul>
 	<li>Sécurité 0 : Une plateforme d’échange.</li>
 	<li>Sécurité 1 : Un portefeuille dont la clé privée est conservée sur support numérique</li>
 	<li>Sécurité 2a : Un "paper wallet".</li>
 	<li>Sécurité 2b : Un "hardware wallet".</li>
</ul>
<strong>Sécurité</strong><strong> 0 : </strong><strong>Une</strong> <strong>plateforme</strong> <strong>d</strong><strong>’</strong><strong>échange</strong>

Si vous stockez aujourd’hui vos ethers sur une plateforme d’échange et que vous n’avez pas une activité de trading, il vous est fortement conseillé de les en retirer. C’est sur les échanges que vos ethers sont les plus exposés.

L’un des intérêts principaux de la blockchain est de bénéficier d’un registre sécurisé par des méthodes cryptographiques. Si vos ethers sont sur la blockchain, il est en théorie impossible de les pirater, sauf à voler votre clé privée. En laissant vos ethers chez Kraken par exemple, vous abandonnez cet avantage et faites confiance à Kraken pour conserver vos ethers et la clé privée du compte sur lequel ils sont stockés, de la même façon que vous faites confiance à une banque lorsque vous lui confiez votre argent. Mais les échanges offrent beaucoup moins de garanties que les banques : ils ne sont pas soumis aux mêmes règlementations bancaires strictes et ils peuvent plus facilement faire l’objet d’un piratage. En pratique, de nombreuses plateformes d’échange ont été piratées ces dernières années, par exemple Mt.Gox, Cryptsy, Poloniex, BTer, ShapeShift, GateCoin et très récemment Bitfinex... Le dépôt d’ethers sur ces plateformes d’échange comporte donc un fort risque qui s’est matérialisé de nombreuses fois. Et au-delà du piratage de la plateforme entière, vous pouvez aussi simplement vous faire pirater votre compte sur la plateforme.

En contrepartie, il est plus simple de gérer ses ethers directement sur un échange que sur un compte dont vous détenez la clé privée. Si vous perdez votre mot de passe, il suffit d'en demander un nouveau à l'échange. Et si vous faites du trading, il est compliqué de retirer et déposer en permanence vos cryptomonnaies sur la plateforme.

Si, malgré ces avertissements, vous souhaitez laisser vos ethers sur un échange, une étape de sécurisation reste essentielle : <strong>l</strong><strong>'</strong><strong>activation</strong> <strong>de</strong> <strong>l</strong><strong>'</strong><strong>authentification</strong> <strong>à</strong> <strong>deux</strong> <strong>facteurs</strong> (ou 2FA pour Two-Factor Authentication). Tous les échanges sérieux proposent cette fonction (Kraken et Poloniex notamment) qui consiste à ajouter une sécurité supplémentaire au mot de passe habituel, en passant par exemple par l'application Google Authenticator.  Une fois cette option activée, le site vous demandera un mot de passe temporaire généré par l'application toutes les X secondes en plus de votre de mot de passe habituel. Vous pouvez l'activer pour toutes les opérations (connexion, retrait, achat/vente d'ethers) ou seulement pour certaines. Si vous avez un comptez chez Kraken, l'activation du 2FA se fait dans l'onglet <em>Security</em> puis <em>Two</em><em>-</em><em>Factor</em> <em>Authentication</em><em>. </em>Si vous utilisez l'application Google Authenticator, sélectionnez le protocole <em>Google</em> <em>Authenticator</em><em>, </em><em>TOTP</em> <em>Mode</em>. Plus d'informations <span style="text-decoration: underline;"><a href="https://support.kraken.com/hc/en-us/articles/203395513-How-do-I-set-up-two-factor-authentication-">sur ce lien</a></span>. Veillez aussi à sauvegarder la clé fournie en cas de perte de votre téléphone.

Ce double degré ne suffira pas à vous protéger en cas de piratage de la plateforme mais devrait rendre la tâche d’un pirate s’attaquant à votre compte plus complexe.

Passons maintenant à une étape de sécurité supplémentaire : le dépôt de vos ethers dans un compte dont vous détenez la clé privée au format numérique.

<strong>Sécurité</strong><strong> 1 : </strong><strong>Un</strong> <strong>portefeuille </strong><strong>dont</strong> <strong>la</strong> <strong>clé</strong> <strong>privée</strong> <strong>est</strong> <strong>conservée sur support numérique</strong>

C’est la solution recommandée sur ce site pour conserver la maîtrise de vos ethers. Il s’agit de créer un compte personnel à l’aide de <a href="https://github.com/ethereum/mist/releases">Mist</a> ou de <a href="https://www.myetherwallet.com/">MyEtherWallet</a> en choisissant un mot de passe pour chiffrer le compte et y envoyer ensuite vos ethers. Après de la création du compte, vous sauvegardez le fichier contenant la clé privée de votre compte sur votre disque dur et en faites une sauvegarde sur une clé USB / un autre moyen, afin de pouvoir le récupérer en cas de panne de votre ordinateur.

En procédant ainsi, le risque lié au piratage de l’échange disparaît naturellement. Vous détenez vous-même vos possessions virtuelles. Vous en devenez cependant l’unique responsable et introduisez donc d’autres problématiques :
<ul>
 	<li>le vol de votre clé privée par une personne malintentionnée, qui connaîtrait votre mot de passe ou qui l’aurait obtenu par un logiciel espion installé sur votre ordinateur (keylogger, etc.).</li>
 	<li>la perte du fichier contenant votre clé privée qui permet d’accéder au compte ou l’oubli du mot de passe que vous avez choisi pour la chiffrer. Si vous perdez la clé privée, vous n’avez <strong>aucun</strong> moyen de la récupérer. Si vous perdez votre mot de passe, il vous reste l’espoir de vous en souvenir plus tard (ou de faire appel à un service de craquage de mot de passe, long et sans garantie).</li>
</ul>
<strong>Sécurité</strong><strong> 2a : </strong><strong>Un</strong> <strong>«</strong><strong> </strong><strong>paper</strong> <strong>wallet</strong><strong> </strong><strong>»</strong>

[caption id="attachment_1319" align="alignright" width="300"]<img class="size-medium wp-image-1319" src="https://www.ethereum-france.com/wp-content/uploads/2016/08/Paper-Wallet-300x124.png" alt="Un exemple de Paper Wallet (n'utilisez pas cette adresse !)" width="300" height="124" /> Un exemple de Paper Wallet (n'utilisez pas cette adresse !)[/caption]

Il s’agit de la même logique que précédemment, mais vous ne gardez pas la clé privée stockée sur votre ordinateur, vous l’imprimez et vous conservez le papier dans un endroit sécurisé comme un coffre de banque, comme vous pourriez conserver de l’or.

Ce mode de fonctionnement est uniquement adapté si vous souhaitez acheter des ethers et les stocker pour une longue durée sans y toucher. Il est en effet très contraignant : il faudra obligatoirement récupérer le « paper wallet » et recopier la clé privée manuellement pour accéder aux ethers : ce n’est pas adapté à une utilisation régulière.

En fonctionnant de cette façon, vous pouvez raisonnablement penser que vos ethers sont en sécurité, sauf si votre ordinateur était vérolé au moment où vous avez généré votre clé privée. Celle-ci n’est pas sauvegardée sur votre disque dur ce qui limite fortement le risque de vol. Le risque de perte subsiste dans le cas où la copie papier de votre clé privée est perdue ou détruite.

Il est très facile de générer un <em>paper wallet</em> avec le site <a href="https://www.myetherwallet.com/"><span style="text-decoration: underline;">MyEtherWallet.com</span></a> : générez un nouveau compte (<em>Generate Wallet) </em>avec un mot de passe sécurisé puis choisissez la méthode 3, <em>Print your paper wallet, or store a QR code version</em>. Pour le détail de l'utilisation de MyEtherWallet, <a href="https://www.ethereum-france.com/creer-et-gerer-son-portefeuille-dether-en-2-minutes-avec-myetherwallet-com/"><span style="text-decoration: underline;">suivez le guide</span></a>. Et comme d'habitude, faites des tests de réception ET d'envoi de petites sommes avec l'adresse avant d'y déposer de grosses sommes.

<strong>Sécurité</strong><strong> 2b : </strong><strong>Un</strong> <strong>«</strong><strong> </strong><strong><em>hardware</em></strong> <strong><em>wallet</em></strong><strong> </strong><strong>»</strong>

[caption id="attachment_1321" align="alignright" width="300"]<a href="https://www.ledgerwallet.com/r/eeb1?path=/products/12-ledger-nano-s"><img class="size-medium wp-image-1321" src="https://www.ethereum-france.com/wp-content/uploads/2016/08/ledger-wallet-300x185.png" alt="Le Ledger Nano S" width="300" height="185" /></a> Le Ledger Nano S[/caption]

Le <em>hardware wallet</em> est un mini-ordinateur qui se présente sous forme de clé, comme le <span style="text-decoration: underline;"><a href="https://www.ledgerwallet.com/r/eeb1?path=/products/12-ledger-nano-s">Ledger Nano S</a></span> (70 € environ), l’un des premiers <em>hardware wallets</em> compatibles Ethereum.

C’est cette clé qui sera chargé de générer votre clé privée, qui n’est jamais communiquée à l’ordinateur que vous utilisez et à laquelle vous même n’avez jamais accès. En effet, lorsque vous utilisez le hardware wallet, seule la clé publique vous permettant de recevoir des ethers vous est communiquée. La clé privée est générée par le matériel au premier lancement et vous pouvez la sauvegarder en recopiant une série de 24 mots aléatoires sur un papier, que vous mettez ensuite en sécurité. Si vous perdez la clé ou qu'elle tombe en panne, vous pouvez récupérer votre compte à l'aide de ces mots.

Lorsque vous souhaitez accéder à vos ethers, vous n'utilisez pas directement la clé privée : c’est le <em>hardware wallet</em> qui se charge de signer la transaction. Vous accédez aux détails de votre compte par l'intermédiaire d'une application sécurisée et vous la validez avec un code PIN que vous avez choisi au premier lancement, directement sur le <em>hardware wallet</em>. Après trois erreurs, il est automatiquement réinitialisé.

Cette méthode de sécurisation est beaucoup plus facile à utiliser que celle du <em>paper wallet</em> puisqu'elle vous permet d’envoyer de recevoir des ethers sans avoir à récupérer un document à la banque. Elle est à la fois plus et moins sécurisée que celle-ci. Elle est plus sécurisée car la clé privée n’est jamais accessible et même si votre ordinateur est piraté, il est impossible de vous voler vos ethers. Elle est moins sécurisée car l’utilisation de la clé repose uniquement sur un code PIN. Si quelqu’un vous observe utiliser la clé et mémorise ce code, il aura accès à vos ethers s’il prend possession de votre clé, que vous avez vocation à utiliser relativement souvent. Si vous veillez à choisir un code PIN unique et à le composer à l’abri des regards, le risque est cependant limité.

Si vous êtes intéressés par une hardware wallet, <a href="https://www.ethereum-france.com/comment-securiser-vos-ethers-avec-un-hardware-wallet/"><span style="text-decoration: underline;">un tutoriel détaillé est aussi disponible sur le site</span></a>.

Notez que <a href="https://www.ethereum-france.com/creer-et-utiliser-un-portefeuille-dether-eth-sur-smartphone-avec-jaxx-ios-android/"><span style="text-decoration: underline;">le wallet Jaxx</span></a> fonctionne un peu sur le même principe que le Ledger Nano S mais sous la forme d'une application iOS ou Android gratuite qui génère votre clé privée sans vous la communiquer. Attention cependant si vous utilisez un téléphone rooté ou jailbreaké : vous n'êtes pas à l'abri d'un vol de données. De même si une faille de sécurité récente est exploitée par un hacker.

<strong>En résumé :</strong>
<ul>
 	<li>Évitez de laisser vos ethers sur une plateforme d'échange, sauf si vous revendez et rachetez régulièrement des ethers ou faites du <em>margin trade</em>.</li>
 	<li>Si vous laissez vos ethers sur une plateforme d'échange, activez <em>a minima</em> l'authentification à deux facteurs.</li>
 	<li>Si vous achetez des ethers comme placement à long terme / réserve de valeur, vous pouvez utiliser un <em>paper wallet</em> pour les mettre en sûreté.</li>
 	<li>Si vous utilisez vos ethers régulièrement, vous avez le choix entre la méthode de la clé privée stockée sur votre ordinateur (et <span style="text-decoration: underline;">dont vous avez gardé une copie de sauvegarde</span>) ou la version plus sécurisée du <em>hardware wallet</em>.</li>
</ul>