---
ID: 73
post_title: >
  Créer et gérer un portefeuille /
  wallet d’ether (ETH) en 2 minutes
author: Simon Polrot
post_excerpt: ""
layout: post
permalink: >
  https://www.ethereum-france.com/creer-et-gerer-son-portefeuille-dether-en-2-minutes-avec-myetherwallet-com/
published: true
post_date: 2016-02-13 14:56:03
---
Pour stocker, recevoir, envoyer les <em>ether</em> que vous allez vous procurer (<span style="text-decoration: underline;"><a href="http://www.ethereum-france.com/comment-acheter-des-ethers-eth/">selon les instructions ici</a></span> ou <span style="text-decoration: underline;"><a href="http://www.ethereum-france.com/obtenir-des-ether-eth/">ici</a></span>), il vous faut <em>a minima</em> un <strong>compte</strong> (« <em>account</em> »). Il existe de multiple façons de créer et gérer un compte d’ether, mais la plus simple et la plus rapide est de passer par le service en ligne <a href="https://www.myetherwallet.com/"><span style="text-decoration: underline;">myetherwallet.com</span></a>.

<strong>Ce service est très utilisé et permet de créer un compte rapidement, mais il nécessite de faire confiance à un service tiers. Le client officiel (<a href="https://github.com/ethereum/mist/releases"><span style="text-decoration: underline;"><em>ethereum mist wallet</em></span></a>) a été conçu par la Fondation Ethereum, mais il est beaucoup plus complexe à utiliser.</strong>

<strong>Dans tous les cas, il est fortement recommandé de lire les <a href="https://www.ethereum-france.com/avertissements-de-securite/"><span style="text-decoration: underline;">recommandations de sécurité</span></a> avant de générer votre compte.</strong>

<!--more-->
<h4>1. Créer un portefeuille (« <em>wallet </em>»)</h4>
La création d’une adresse de portefeuille par le site myetherwallet.com se fait comme suit :
<ul>
 	<li>Se rendre sur le site à l’adresse <span style="text-decoration: underline;"><a href="http://www.myetherwallet.com">myetherwallet.com</a>.</span></li>
</ul>
<ul>
 	<li>Choisir un mot de passe qui permettra de protéger l’accès à votre compte et l'entrer dans la case précédée de <em>Entrez un mot de passe fort (au moins 9 caractères)</em>. Il est recommandé de choisir un mot de passe contenant au moins un caractère minuscule, un caractère majuscule et un nombre. N'hésitez pas à utiliser des caractères spéciaux (@&amp;$%...).</li>
</ul>
<p style="padding-left: 30px;"><strong><code></code>Le mot de passe ne peut pas être changé ni retrouvé en cas de perte, choisissez un mot de passe sécurisé mais ne l’oubliez pas !</strong></p>

<ul>
 	<li>Cliquer sur <em>Générer un portefeuille</em>.</li>
</ul>
<ul>
 	<li>Le message <em>Succès ! Votre portefeuille a été généré.</em> devrait s’afficher, sur la suite de la page :</li>
</ul>
&nbsp;

<a href="https://www.myetherwallet.com/"><img class="aligncenter size-large wp-image-1379" src="https://www.ethereum-france.com/wp-content/uploads/2016/02/MyEtherWallet-FR-Succès-1024x544.png" alt="myetherwallet-fr-succes" width="1024" height="544" /></a>

C’est tout ! Votre adresse, qui correspond à un « numéro de compte » sur lequel envoyer les ethers, est indiquée dans la case <em>Sauvegarder votre portefeuille</em>.

<strong>Il  faut absolument sauvegarder votre clé privée (« <em>Clé privée</em> »), au moins en version encryptée. Pour cela, cliquez sur Fichier Keystore/JSON<em> (Recommandé - Chiffré - Format Mist/Geth</em>).</strong>

Vous pouvez aussi copier la chaine de caractère qui apparaît dans la case <i>Clé privée (non-chiffrée)</i>, ou cliquer sur <em>Fichier JSON (non-chiffré)</em>, mais cette deuxième clé permet d'accéder <span style="text-decoration: underline;">sans mot de passe</span> à votre compte d'ether. Si vous copiez cette chaine de caractère, mettez-là en lieu sûr ! (coffre de banque, service de sauvegarde chiffré...).

La dernière option (<em>Imprimer votre portefeuille papier</em>) permet de conserver sa clé… sur du papier ! Cela vous permet de la mettre <span style="text-decoration: underline;">physiquement</span> en lieu sur, et vous ne pouvez y accéder qu’en tapant le texte écrit dessus ou en scannant le QR code avec un téléphone.

<strong>Attention </strong>:
<ul>
 	<li><strong>Si 1) vous perdez vos clés, ou 2) que nous n’avez sauvegardé que la version <em>encrypted</em> et que vous perdez votre mot de passe, vous avez définitivement perdu l'accès à ce compte. Il n’existe AUCUN moyen de récupérer l’accès ou de retrouver facilement le mot de passe. Il est donc CAPITAL de conserver les clés dans un endroit sûr ET sécurisé et de MEMORISER votre mot de passe. Les personnes qui possèdent beaucoup d’« actifs » virtuels comme le bitcoin ou l’ether ont souvent un « portefeuille papier » à la banque, dans un coffre.</strong><strong> </strong></li>
</ul>
<ul>
 	<li><strong>La version <em>non-chiffrée</em> de la clé permet d’accéder à vos <em>ether </em><span style="text-decoration: underline;">sans mot de passe</span> : ne la diffusez à personne et n'en conservez aucune copie accessible facilement.
</strong></li>
</ul>
<h4>2. Utiliser un portefeuille pour envoyer des <em>ether</em></h4>
Une fois le portefeuille créé <u>et la clé sauvegardée</u>, vous pouvez accéder à votre portefeuille avec le lien « <em>Envoyer des ether</em> ».
<img class="aligncenter size-large wp-image-1381" src="https://www.ethereum-france.com/wp-content/uploads/2016/02/MyEtherWallet-Envoyer-des-ether.jpg" alt="myetherwallet-envoyer-des-ether" width="605" height="302" />

Ensuite, vous pouvez :
<ul>
 	<li>Utiliser un fichier JSON téléchargé dans l’étape 1 (<em>Fichier Keystore/JSON</em>)</li>
</ul>
<p style="padding-left: 30px;">Il faut alors cliquer sur <em>Choisissez le fichier de portefeuille</em> choisir le fichier avant de valider.</p>

<ul>
 	<li>Écrire manuellement la clé (<em>Clé privée</em>) dans la case qui s’affiche avant de valider.</li>
</ul>
Dans les deux cas, le site vous demandera le mot de passe en cas de clé chiffrée avant de vous permettre d’accéder au compte. Entrez le mot de passe et cliquez sur Déchiffrer<em>.</em>

L’état de votre compte s’affiche alors en dessous de la page :

<img class="aligncenter size-large wp-image-1382" src="https://www.ethereum-france.com/wp-content/uploads/2016/02/MyEtherWallet-Envoyer-des-ethers-Transaction-1024x423.jpg" alt="myetherwallet-envoyer-des-ethers-transaction" width="1024" height="423" />

A partir de cet état, vous pouvez envoyer des ether vers une autre adresse. Il suffit pour cela de copier-coller l’adresse à laquelle vous souhaitez envoyer de l’<em>ether</em> dans le champ <em>Adresse de destination</em> et d’indiquer le montant dans le champ <em>Montant à envoyer</em>.

Vous pouvez envoyer des ether (ETH) uniquement ou des ether classic (ETC) uniquement, ou faire une transaction standard. Si vous ne comprenez pas la distinction, utilisez toujours ETH (transaction standard).

Une fois le montant indiqué, cliquez sur <em>Générer la transaction</em>. Le système vous indique alors dans la section <em>Transaction signée </em>le code de la transaction (si vous souhaitez le conserver) que vous pouvez valider avec <em>Envoyer la transaction</em>. Après une fenêtre de confirmation, vous pouvez confirmer une dernière fois avec le bouton <em>Oui, j'en suis sûr ! Effectuer la transaction</em>.

<strong>Attention : Le montant est à indiquer au format américain : la virgule est remplacée par un point. Pour envoyer <em>2,5</em> ether, indiquez <em>2.5</em>. Le site n’accepte pas la virgule.</strong>