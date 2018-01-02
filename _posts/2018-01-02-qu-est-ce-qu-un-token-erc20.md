---
ID: 3041
post_title: 'Qu&rsquo;est-ce qu&rsquo;un token ERC20 ?'
author: Simon Polrot
post_excerpt: ""
layout: post
permalink: >
  https://www.ethereum-france.com/qu-est-ce-qu-un-token-erc20/
published: true
post_date: 2018-01-02 12:48:16
---
<strong>Nous avons déjà exploré de façon générale les <em>tokens</em> ou jetons <a href="https://www.ethereum-france.com/qu-est-ce-qu-une-cryptomonnaie-token-bitcoin-ether-gnt-gno-dgd-plu-rep-rlc/">dans cet article dédié aux actifs numériques</a>. Penchons-nous maintenant sur une forme particulière de ces tokens : les ERC20. Ceux-ci pullulent sur Ethereum aujourd'hui, du fait de la simplicité de leur déploiement mais aussi, voire surtout, de la multiplication des ICOs, ces opérations de vente de tokens (bien décrites sur <a href="https://icomentor.net/2017/08/01/ico-definition-explication/">ICO Mentor</a> ou <a href="https://bitconseil.fr/ico-levees-de-fonds-cryptomonnaies/">BitConseil</a>). A tel point qu'il existe aujourd'hui plus <a href="https://etherscan.io/tokens">de 18 000 tokens ERC20</a> déployés ! Etat des lieux et aperçu du futur de ce qu'est aujourd'hui l'application d'Ethereum la plus utilisée.</strong>

<h1>Comportement d'un contrat de token sur Ethereum</h1>

Un contrat de token déployé sur Ethereum est <a href="https://www.ethereum-france.com/smart-contract-ou-le-contrat-auto-executant/">un smart-contract comme un autre</a>, contenant simplement un registre désignant les propriétaires de tokens du contrat et gérant l'ensemble des transferts de ces tokens en mettant à jour ledit registre.

[caption id="attachment_3076" align="aligncenter" width="300"]<a href="https://www.ethereum-france.com/qu-est-ce-qu-un-token-erc20/tokens1/" rel="attachment wp-att-3076"><img class="wp-image-3076 size-medium" src="https://www.ethereum-france.com/wp-content/uploads/2017/12/tokens1-300x157.png" alt="" width="300" height="157" /></a> L'état d'un contrat de tokens, représenté sous forme de tableau[/caption]

<em>Par exemple, si X envoie une transaction de transfert de 100 tokens à Y, le contrat modifie son registre pour réduire le nombre total de tokens de X de 100 et augmenter au même moment celui de Y.</em>

[caption id="attachment_3075" align="aligncenter" width="300"]<a href="https://www.ethereum-france.com/qu-est-ce-qu-un-token-erc20/tokens2/" rel="attachment wp-att-3075"><img class="wp-image-3075 size-medium" src="https://www.ethereum-france.com/wp-content/uploads/2017/12/tokens2-300x157.png" alt="" width="300" height="157" /></a> Dans cet exemple le compte 0x0148... a envoyé 1000 tokens au compte 0x9f7a...[/caption]

<h1>ERC20, document de travail devenu standard</h1>

Les tokens dits "<em>ERC20</em>" sont issus du processus de proposition / amélioration mis en oeuvre par la Fondation Ethereum sur <a href="https://github.com/ethereum/EIPs/issues">son compte Github</a>. ERC signifie littéralement Ethereum Request for Comments : un processus par lequel une personne demande à la communauté de revoir et de commenter une proposition pour Ethereum. En l'occurence, la 20ème proposition postée sur le Github le 19 novembre 2015 concernait une proposition de standards pour le développement de <em>tokens</em> sur Ethereum - elle s'appela donc ERC20. L'idée de token programmable était une des plus simples à implémenter sur la blockchain. Initiée par <a href="https://github.com/frozeman">frozeman</a> (Fabian Vogelsteller), la proposition a immédiatement donné lieu à <a href="https://github.com/ethereum/EIPs/issues/20">d'intenses discussions</a>.

Il est donc important de souligner qu'ERC20 est un standard : il définit des fonctions et des événements qu'un token doit gérer pour être qualifié d'ERC20. Il ne s'agit pas d'un code précis ou d'un produit. Chacun peut créer son propre code de token ERC20 tant que celui-ci respecte les fonctions standard et leur comportement. En l'occurence, il existe de nombreux contrats de tokens ERC20 : le <a href="https://www.ethereum.org/token">code fourni sur ethereum.org</a>, le <a href="https://github.com/OpenZeppelin/zeppelin-solidity/tree/master/contracts/token">code modulaire d'OpenZepplin</a>, le <a href="https://theethereum.wiki/w/index.php/ERC20_Token_Standard">code de ce wiki</a>, etc.

N'importe quel code mettant en application les spécifications ERC20 crée un token ERC20.

<h1>Intérêt, limites et évolutions futures du standard ERC20</h1>

Cette standardisation a permis le développement rapide d'un très large écosystème de tokens sur Ethereum. Avant sa création, chaque service, chaque projet devait réinventer la roue (le token), ce qui a d'ailleurs provoqué des erreurs et des incompatibilités. Avec un standard simple et ouvert, les tokens peuvent être déployés facilement. C'est aussi le cas des les services utilisant ces tokens.

De fait, l'essentiel des services développés sur Ethereum aujourd'hui gèrent ce standard et uniquement ce standard. Il est facile de créer un service gérant les tokens ERC20 car vous connaissez à l'avance les fonctions basique que ce token va accepter. Par exemple, <a href="https://www.myetherwallet.com/">MyEtherWallet</a> et <a href="https://etherscan.io/">Etherscan</a> sont capables d'afficher le solde de vos tokens ERC20 sur son interface, et <a href="https://etherdelta.com/">EtherDelta</a> gère nativement les échanges décentralisés entre tous les tokens ERC20 existants.

Cette standardisation a naturellement eu l'effet pervers de toutes les spécifications, en figeant d'une certaine façon les <em>tokens</em> dans leur forme actuelle pendant un certain temps. Lorsque le standard devient la norme, l'expérimentation ne peut se faire que dans le cadre restreint de ce standard. Il est heureux que les créateurs du standard avaient dès le départ en tête ces limitations et ont veillé à en faire un standard "minimum" avec des spécifications portant uniquement sur les fonctions essentielles d'un token.

Ce standard a cependant été critiqué pour de nombreuses raisons. D'abord, il n'est valable que pour un token fongible (tous les tokens d'un contrat ERC20 ont les mêmes caractéristiques, ils ne sont pas uniques et on peut échanger deux tokens du même contrat ERC20 sans effet) et il ne prévoit aucune fonction pour éviter les erreurs d'envoi, aucun standard de mise à jour de son code ou de bonnes pratiques quant à son émission, etc.

En réaction à ce caractère limité du standard, de nombreuses initiatives ont vu le jour, et notamment :

<ul>
    <li>La <a href="https://github.com/ethereum/EIPs/issues/223">proposition ERC223</a>, qui vise à intégrer des mécanismes de contrôle dans le contrat de token directement visant à éviter les transferts de tokens vers une adresse ne pouvant elle-même gérer les tokens (soit parce qu'il s'agit d'une adresse de contrat, soit parce qu'il s'agit de l'adresse du token ERC20 elle-même).</li>
    <li>La <a href="https://github.com/Giveth/minime">proposition Minime Token</a>, un token ERC20 avec des fonctions supplémentaires. Par exemple, il est facile de cloner le token et toutes ses balances, notamment pour mettre à jour ses fonctionnalités. Il est aussi possible de définir une personne qui contrôle les tokens (Token Controller) qui peut les déplacer, en créer de nouveaux, en détruire... Ou encore, l'historique des soldes de tokens par compte est enregistré et facilement consultable.</li>
</ul>

D'autres propositions sont visibles <a href="https://github.com/ethereum/EIPs/issues?utf8=%E2%9C%93&amp;q=is%3Aissue+is%3Aopen+token">sur le github officiel de la Fondation</a>.

<h1>Spécifications ERC20</h1>

Les fonctions et les événement qu'un token "ERC20" doit pouvoir gérer sont les suivants :

<ul>
    <li><code>name</code> est la fonction qui doit renvoyer le nom du token (par exemple <em>OmiseGo</em> ou <em>VariabL Contribution Token</em>)</li>
    <li><code>symbol</code> doit renvoyer le symbole du token (par exemple "OMG" est le symbole du token <em>OmiseGo</em>, "VCT" est le symbole de <em>VariabL Contribution Token</em>)</li>
    <li><code>decimals</code> renvoie le nombre de décimales qu'il faut prendre en compte pour le token. En effet, les balances de tokens sont gérés sans décimales par les contrats ERC20 - pour une personne possédant 1 token à 18 décimales, la fonction <code>balanceOf</code> définie ci-dessous renverra 1000000000000000000.</li>
    <li><code>totalSupply</code> doit renvoyer le nombre total de tokens existant</li>
    <li><code>balanceOf</code> doit permettre de consulter le nombre de tokens détenu par un compte</li>
    <li><code>allowance</code> renvoie le nombre de tokens qu'une adresse est autorisée à retirer du contrat de token</li>
    <li><code>transfer</code> est la fonction permettant à un compte possédant des tokens d'en envoyer à un autre compte</li>
    <li><code>transferFrom</code> permet de transférer des tokens d'une adresse à une autre, sans que l'adresse qui envoie la transaction soit celle qui détient les tokens</li>
    <li><code>approve</code> est une fonction permettant au détenteur d'un contrat de token d'approuver un retrait pour un montant déterminé par un compte précis (change l'"allowance" de ce compte)</li>
</ul>

Ces fonctions doivent également déclencher deux <a href="https://media.consensys.net/technical-introduction-to-events-and-logs-in-ethereum-a074d65dd61e">événements</a> :

<ul>
    <li><code>Transfer</code> se déclenche pour chaque appel à la fonction <code>transfer</code> ou <code>transferFrom</code></li>
    <li><code>Approval</code> se déclenche à chaque appel à la fonction <code>approve</code></li>
</ul>

Le détail de ces fonctions et des événements associés est consultable <a href="https://github.com/ethereum/EIPs/blob/master/EIPS/eip-20-token-standard.md">sur la page de l'Ethereum Improvement Proposal correspondant au standard ERC20</a>.

Pour aller plus loin, quelques articles (en anglais) sur les tokens ERC20 :

<ul>
    <li><a href="https://medium.com/@jgm.orinoco/understanding-erc-20-token-contracts-a809a7310aa5">Understanding ERC-20 token contracts par Jim McDonald</a></li>
    <li><a href="https://medium.com/@james_3093/ethereum-erc20-tokens-explained-9f7f304055df">Ethereum ERC20 Tokens Explained par James Seibel</a></li>
    <li><a href="https://www.coindesk.com/ethereums-erc-20-tokens-rage-anyway/">Ethereum 'Tokens' Are All the Rage. But What Are They Anyway? par Amy Castor</a></li>
</ul>