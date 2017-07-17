---
ID: 1052
post_title: >
  Mise à jour de stabilité pour Ethereum
  Wallet (0.7.5)
author: Simon Polrot
post_excerpt: ""
layout: post
permalink: >
  https://www.ethereum-france.com/mise-a-jour-de-stabilite-pour-ethereum-wallet-0-7-5/
published: true
post_date: 2016-06-16 09:48:30
---
[caption id="attachment_1053" align="alignright" width="300"]<img class="size-medium wp-image-1053" src="https://www.ethereum-france.com/wp-content/uploads/2016/06/Ethereum-Wallet-Sync-300x173.png" alt="Ethereum Wallet - Sync" width="300" height="173" /> Synchronisation rapide au 1er démarrage[/caption]

Alex Van de Sande, développeur à la Fondation, <span style="text-decoration: underline;"><a href="https://github.com/ethereum/mist/releases/tag/0.7.5">annonce aujourd'hui la sortie de la très attendue version 0.7.5 de l'Ethereum Wallet</a></span>.

Pour rappel, Ethereum Wallet permet d’utiliser les fonctions avancées de la blockchain Ethereum : déploiement d’un contrat, appel à un contrat existant, surveillance d’un contrat. Le Wallet permet aussi plus simplement de créer et gérer un portefeuille d’ether. Il est développé par l’équipe de développement du logiciel Mist, qui servira à terme de point d’entrée grand public aux dApps développées sur Ethereum. Son fonctionnement est plus complexe que l’utilisation d’un site comme <span style="text-decoration: underline;"><a href="http://www.myetherwallet.com/">myetherwallet.com</a></span>, mais son ergonomie s’est améliorée au fil des versions. Pour fonctionner, le logiciel télécharge sur votre ordinateur l’intégralité de la blockchain Ethereum (comptez au mieux quelques heures et quelques Go d’espace disque libre).

La version 0.7.4 était largement critiquée par la communauté pour ses lenteurs et ses problèmes de synchronisation. D'après le billet publié sur Github, cette version corrige l'essentiel des problèmes de stabilité, permet une synchronisation rapide au premier lancement et un certain nombre d'autres nouveautés, dont une amélioration de la traduction en français (<span style="text-decoration: underline;"><a href="https://github.com/ethereum/mist/releases/tag/0.7.5">la liste complète est présente sur le billet, en anglais</a></span>).

Si nous n'avez pas lancé Ethereum Wallet depuis longtemps, il est conseillé de supprimer la blockchain téléchargée sur votre disque dur avant de lancer cette nouvelle version pour permettre l'activation de la synchronisation rapide. Sous Windows 7, 8 ou 10, celle-ci est localisée dans le répertoire suivant : C:\Users\[Nom d'utilisateur]\AppData\Roaming\Ethereum\chaindata. <strong>Attention : ne supprimez pas le dossier keystore qui contient vos portefeuilles ! (même si vous en avez normalement déjà fait une sauvegarde)</strong>

Pour télécharger la version 0.7.5 du Wallet, <span style="text-decoration: underline;"><a href="https://github.com/ethereum/mist/releases">cliquez ici</a></span> puis choisissez la version adaptée à votre système d’exploitation :
<ul>
 	<li>Linux 32 bits : Ethereum-Wallet-linux32-0-7-5.zip</li>
 	<li>Linux 64 bits : Ethereum-Wallet-linux64-0-7-5.zip</li>
 	<li>Mac OS X : Ethereum-Wallet-macosx-0-7-5.zip</li>
 	<li>Windows 32 bits : Ethereum-Wallet-win64-0-7-5.zip</li>
 	<li>Windows 64 bits : Ethereum-Wallet-win64-0-7-5.zip</li>
</ul>
Il vous suffit ensuite d'extraire l'archive puis d'exécuter le fichier Ethereum-Wallet.