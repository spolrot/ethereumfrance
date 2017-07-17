---
ID: 1769
post_title: >
  Déconstruction du terme “Smart
  Contract”
author: Simon Polrot
post_excerpt: ""
layout: post
permalink: >
  https://www.ethereum-france.com/deconstruction-du-terme-smart-contract/
published: true
post_date: 2016-12-23 00:04:11
---
<em>Cet article est la traduction intégrale en français de l’article “‘<a href="https://medium.com/@ConsenSys/unpacking-the-term-smart-contract-dc8ac8afc0ef"><span style="text-decoration: underline;">Unpacking the term ‘Smart Contract</span></a>’” rédigé initialement par <a href="https://blog.stakeventures.com/pages/whoami"><span style="text-decoration: underline;">Pelle Braendgaard</span></a> et traduit par <a href="https://media.consensys.net/"><span style="text-decoration: underline;">ConsenSys Media</span></a> pour Ethereum France. Son objectif est de rendre compréhensible le terme "smart contract", dans la lignée de l'article "<a href="https://www.ethereum-france.com/smart-contract-ou-le-contrat-auto-executant/"><span style="text-decoration: underline;">Smart-Contract ou le contrat auto-exécutant</span></a>" .</em>

<strong>De contrat à <i>smart contract</i> sur Ethereum. </strong><span style="font-weight: 400;">J’ai toujours été fasciné par la définition que Nick Sazbo donne des </span><i><span style="font-weight: 400;">smarts contracts</span></i><span style="font-weight: 400;">. J’ai joué avec les premières versions expérimentales du concept, et puis </span><a href="http://www.ethereum.org/"><span style="font-weight: 400;">Ethereum</span></a><span style="font-weight: 400;"> a sorti sa première implémentation concrète. </span>
<h3><b>Que sont les </b><b><i>smart contracts</i></b><b> ?</b></h3>
<span style="font-weight: 400;">Les </span><i><span style="font-weight: 400;">smart contracts</span></i><span style="font-weight: 400;"> sont essentiellement des clauses qui sont programmés pour exécuter des actions spécifiques.</span>

<span style="font-weight: 400;">Sur Ethereum, ce qu'on appelle contrat est un morceau de code qui existe sur la blockchain. Le contrat est créé lors d’une transaction, qui est exécutée par toutes les noeuds connectées sur la blockchain. </span><span style="font-weight: 400;">Les parties et leurs droits spécifiques sont conservés sous forme de données et de code sur la blockchain elle-même. </span><span style="font-weight: 400;">Les parties peuvent accéder à leurs droits en utilisant les fonctions qui ont été prédéterminées par le </span><i><span style="font-weight: 400;">smart contract</span></i><span style="font-weight: 400;">. </span><span style="font-weight: 400;">Chaque appel aux fonctions est une transaction sur Ethereum. Le code de cette fonction est exécuté par chaque noeud présent sur le réseau Ethereum.</span>

<strong>Un <i>smart contract</i></strong><span style="font-weight: 400;"><strong> dans le contexte d’Ethereum n’est pas nécessairement un contrat légal</strong>, mais peut <em>a priori</em> l'être. </span><span style="font-weight: 400;">Cet article ne rentrera pas en détail sur l’architecture de la blockchain Ethereum mais se concentrera sur la notion de </span><i><span style="font-weight: 400;">smart contracts</span></i><span style="font-weight: 400;">.</span>
<h3><b>Un contrat de séquestre simplifié</b></h3>
<span style="font-weight: 400;">Une séquestre est traditionnellement un contrat légal dont un tiers de confiance détient le contrôle pour le compte d’un acheteur ou vendeur, par exemple.</span>

<span style="font-weight: 400;">Imaginons que je veuille acheter la voiture d'Alice. Alice n’habite pas dans la même ville que moi mais elle peut faire livrer la voiture en question. </span><span style="font-weight: 400;">Je ne veux pas lui envoyer la somme que je lui dois sans recevoir la voiture au préalable, car je risquerais de ne pas la recevoir.</span>

<span style="font-weight: 400;">Il nous manque un élément pour garantir le succès de la transaction. Ce qui nous manque est la tierce partie, le tiers de confiance. Un tiers de confiance est par exemple un avocat, une banque ou un service spécialisé.</span>

<span style="font-weight: 400;">Maintenant, je peux mettre en place un contrat entre Alice, le tiers de confiance Bob, et moi. . J’envoie le versement à Bob, le tiers de confiance, qui le garde jusqu'à ce que je confirme la réception de la voiture. Il ne donnera les fonds à Alice qu’avec cette confirmation.</span>

<i><span style="font-weight: 400;">Le contrat :</span></i>

<i><span style="font-weight: 400;">Je  (l’acheteur) verse une caution de $10,000 à Bob (le tiers de confiance) qui gardera cette somme en sécurité dans son compte de banque jusqu'à ce que l’acheteur confirme l'arrivée d’une 1996 Mazda Protegé (</span></i><i><span style="font-weight: 400;">la voiture) de la part d’Alice (la vendeuse). Une fois la transaction confirmée par l’acheteur,  le tiers de confiance peut verser les fonds à la vendeuse. Si la vendeuse ne livre pas la voiture à l’acheteur avant le 1er Avril, le tiers de confiance rendra la caution à l’acheteur.</span></i>
<h3><b>Ecriture d'un contrat de séquestre sous forme d'un s</b><b><i>mart contract</i></b></h3>
<span style="font-weight: 400;">Créons une implémentation simple d'un contrat de séquestre avec </span><span style="text-decoration: underline;"><a href="https://ethereum.github.io/solidity/"><span style="font-weight: 400;">Solidity</span></a></span><span style="font-weight: 400;">, qui est devenu le langage de référence pour développer des </span><i><span style="font-weight: 400;">smart contracts</span></i><span style="font-weight: 400;"> sur Ethereum. </span>

<span style="font-weight: 400;">Il n’y a rien </span><span style="font-weight: 400;">à</span><span style="font-weight: 400;"> craindre si vous n'êtes pas développeur. Vous n'êtes pas obligés de connaître le code pour pouvoir suivre :</span>

<span style="text-decoration: underline;"><a href="https://chriseth.github.io/browser-solidity/?gist=38cde143e314a91b8362">Code source pour un contrat de séquestre simple</a></span>

Ce contrat est créé par l’acheteur et comprends deux parties ; il donne la permission au tiers de confiance de verser les fonds au vendeur ou d'annuler la transaction et rendre les fonds à l’acheteur.

<span style="font-weight: 400;">L’acheteur crée le contrat à l’aide d’une application dédiée sur internet. Puis, il l’envoie au réseau Ethereum avec les données concernant le vendeur et l’agent (leurs adresses <em>ethereum</em>) et la valeur du bien (en <em>ether</em>). </span><span style="font-weight: 400;">Tout comme le bitcoin, la monnaie principale de la blockchain Bitcoin, ether est la monnaie du réseau d’Ethereum. </span><span style="font-weight: 400;">Il est tout à fait possible de créer d’autres formes de monnaies sur Ethereum mais gardons cet article simple pour l’instant.</span>
<h3><b>Cet exemple de cas d’usage d’un </b><b><i>smart contract</i></b><b> est-il pertinent ?</b></h3>
<span style="font-weight: 400;">En d’autres termes, est-ce que ce </span><i><span style="font-weight: 400;">smart contract</span></i><span style="font-weight: 400;"> est vraiment si ‘smart’ que ça ? </span>

<span style="font-weight: 400;">Puisque le <em>tiers de confiance</em> ne peut pas accéder aux fonds directement, il peut seulement les transmettre au vendeur ou les rendre à l’acheteur. Ceci est déjà une amélioration du procédé traditionnel.</span>

<span style="font-weight: 400;">Remarquons qu’ici, il n’est pas spécifié de clauses pour le transfert des fonds vers l’acheteur ou pour l’annulation.</span>

<span style="font-weight: 400;">Dans le système traditionnel, un tel contrat aurait une clause d’échéance. Ces propriétés peuvent êtres intégrés à Ethereum, mais sont plus complexes.</span>
<h3><strong>Avons nous besoin d’un tiers de confiance ?</strong></h3>
<span style="font-weight: 400;">Idéalement, nous voulons éliminer le besoin d’un tiers de confiance pour les </span><i><span style="font-weight: 400;">smart contracts</span></i><span style="font-weight: 400;">. Nous avons réussi à réduire notre dépendance au tiers de confiance en limitant son pouvoir d'intervention sur les fonds. Pourtant, ce serait encore mieux qu’il y ait une exécution automatique du contrat. Si l’autre partie du contrat (le transfert du bien) est effectuée sur le réseau Ethereum, il est possible de remplacer le tiers de confiance par un autre </span><i><span style="font-weight: 400;">smart contract </span></i><span style="font-weight: 400;">(<em>ndt : il est également possible de faire appel à des tiers de confiance spécialisés, dits "Oracles", concept <a href="https://www.ethereum-france.com/les-oracles-lien-entre-la-blockchain-et-le-monde/"><span style="text-decoration: underline;">exploré ici</span></a></em>).</span>
<h3><b>Un smart contract est-il vraiment un contrat?</b></h3>
<span style="font-weight: 400;">Premièrement, voyons ce qu’est un contrat. Selon Wikipédia…</span>

<i><span style="font-weight: 400;">Un </span></i><b><i>contrat</i></b><i><span style="font-weight: 400;"> est un accord de volonté en vue de créer une ou des obligations juridiques. C'est un engagement volontaire, formel ou informel, seul ou entre plusieurs parties et reconnu par le droit.</span></i>
<ul>
 	<li style="font-weight: 400;"><i><span style="font-weight: 400;">Engagement volontaire, le contrat naît d’un accord assumé et accepté. Selon la classification du </span><a href="https://fr.wikipedia.org/wiki/Code_civil_(France)"><span style="font-weight: 400;">code civil</span></a><span style="font-weight: 400;">, il diffère ainsi des autres obligations, comme celles issues des </span><a href="https://fr.wikipedia.org/wiki/D%C3%A9lit_civil"><span style="font-weight: 400;">délits civils</span></a><span style="font-weight: 400;">, des </span><a href="https://fr.wikipedia.org/wiki/Quasi-d%C3%A9lit_en_droit_civil_fran%C3%A7ais"><span style="font-weight: 400;">quasi-délits</span></a><span style="font-weight: 400;">, des </span><a href="https://fr.wikipedia.org/wiki/Quasi-contrat_en_droit_civil_fran%C3%A7ais"><span style="font-weight: 400;">quasi-contrats</span></a><span style="font-weight: 400;">, ou de la </span><a href="https://fr.wikipedia.org/wiki/Loi"><span style="font-weight: 400;">loi</span></a><span style="font-weight: 400;">.</span></i></li>
</ul>
<ul>
 	<li style="font-weight: 400;"><i><span style="font-weight: 400;">Formel ou informel, le contrat n’est pas soumis, sauf exceptions</span><span style="font-weight: 400;">, à des exigences de forme. Cette liberté est le corollaire de l’autonomie des volontés.</span></i></li>
</ul>
<ul>
 	<li style="font-weight: 400;"><em><span style="font-weight: 400;">Au moins deux </span><a href="https://fr.wikipedia.org/wiki/Partie_(droit)"><span style="font-weight: 400;">parties</span></a><span style="font-weight: 400;"> sont liées par le contrat, ce qui distingue le contrat d’un simple engagement individuel ou d’un </span><a href="https://fr.wikipedia.org/wiki/Droit_r%C3%A9el"><span style="font-weight: 400;">droit réel</span></a><span style="font-weight: 400;">, comme la </span><a href="https://fr.wikipedia.org/wiki/Propri%C3%A9t%C3%A9"><span style="font-weight: 400;">propriété</span></a><span style="font-weight: 400;">.</span></em></li>
</ul>
<ul>
 	<li style="font-weight: 400;"><em><span style="font-weight: 400;">Reconnu par le droit, le contrat diffère ainsi de la </span><a href="https://fr.wikipedia.org/wiki/Promesse"><span style="font-weight: 400;">promesse</span></a></em><span style="font-weight: 400;"><em> qui ne nécessite pas de consécration officielle</em>”</span></li>
</ul>
<span style="font-weight: 400;">Tout seul, un </span><i><span style="font-weight: 400;">smart contract</span></i><span style="font-weight: 400;">, ne satisfait pas aux critères requis pour répondre à la définition d’un contrat. La création du </span><i><span style="font-weight: 400;">smart contract</span></i><span style="font-weight: 400;"> pourrait être interprétée comme une offre de l’acheteur, mais ceci ne prend pas en compte le tiers de confiance ni le vendeur pour accepter la transaction.</span>

<span style="font-weight: 400;">Le contrat ne considère pas la logistique du vendeur ni de l’acheteur (la livraison de voiture) ni la logistique de l’agent (ses services et ses honoraires).</span>

<span style="font-weight: 400;">Ceci ne rend pas l’utilisation d’un </span><i><span style="font-weight: 400;">smart contrac</span></i><span style="font-weight: 400;">t impossible. En réalité, tant qu’une partie de la communication entre les acteurs de l'échange se fait hors du contrat, le contrat peut prendre place.</span>

<span style="font-weight: 400;">Le vrais contrat pourrait être implémentés comme application classique sur internet avec un intermédiaire comme tiers de confiance (comme c’est le cas pour eBay) ou dans une dApp (terme utilisé pour décrire un nouveau type d’application qui est décentralisé sur Ethereum).</span>

<strong>L'important est que toutes les acteurs de chaque transaction comprennent le contrat et le rôle du <i>smart contract</i>.</strong>