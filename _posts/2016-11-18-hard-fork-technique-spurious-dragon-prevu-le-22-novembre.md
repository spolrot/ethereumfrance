---
ID: 1682
post_title: >
  Hard Fork technique – Spurious Dragon
  – prévu le 22 novembre
author: JdeTychey
post_excerpt: ""
layout: post
permalink: >
  https://www.ethereum-france.com/hard-fork-technique-spurious-dragon-prevu-le-22-novembre/
published: true
post_date: 2016-11-18 16:05:46
---
<em>Annoncée en complément du Hard Fork EIP-150 (<span style="text-decoration: underline;"><a href="https://www.ethereum-france.com/hard-fork-eip-150-mise-a-jour-de-recalibrage-et-carnet-de-voyage/">mise à jour de recalibrage</a></span>)  ce nouveau Hard Fork est annoncé et prévu pour le bloc 2 675 000 soit mardi 22 novembre vers 16h30. Son objectif est de corriger un certain nombre de stigmates <a href="https://www.ethereum-france.com/hard-fork-eip-150-mise-a-jour-de-recalibrage-et-carnet-de-voyage/">des attaques DoS de septembre-octobre</a> et d'empêcher par le futur les attaques de réplication entre les chaines ETH et ETC. En pratique, il implémentera quatre EIP (Ethereum Improvement Proposal) qui sont des propositions publiques d'amélioration d'Ethereum dont la liste complète <a href="https://github.com/ethereum/EIPs/issues"><span style="text-decoration: underline;">est disponible ici</span></a>. Suivez son arrivée ici : <strong><a href="https://fork.codetract.io/">https://fork.codetract.io/</a></strong>.</em>
<h3>Épilogue de l'attaque par déni de service...</h3>
Les EIP implémentées sont les suivantes :
<ul>
 	<li><strong><strong>EIP 155 - Protection contre l’attaque de réplication (Simple replay attack protection)</strong></strong>Une transaction issue de la chaîne minoritaire ETC (Ethereum classique) est potentiellement valide sur la chaîne principale ETH et vice et versa. Pour mémoire cette attaque avait été notamment exploitée contre des places de marché comme <span style="text-decoration: underline;"><strong><a href="http://bitcoinist.net/brian-armstrong-coinbase-ethereum/">Coinbase</a></strong></span> et plusieurs options permettent aujourd’hui de s’en protéger facilement comme le contrat de split de MyEtherWallet. La proposition EIP 155 règle ce problème en modifiant le <em>hash</em> de la transaction qui est signé par la clé privée d’un l’utilisateur (<span style="text-decoration: underline;"><strong><a href="https://github.com/ethereum/EIPs/issues/155">détails techniques ici</a></strong></span>).</li>
 	<li><strong><strong>EIP 160 - augmentation du coût de l’OPcode EXP</strong></strong> L’OPcode (langage machine) EXP est l’opération d’exponentiation dans la machine virtuelle Ethereum. Il consomme actuellement 10 gaz plus 10 gaz par byte dans l’exposant alors que les étalonnages suggèrent un prix de 4 à 8 fois supérieur. L’EIP 160 passe son coût à 10 gaz plus 50 par byte dans l’exposant (<span style="text-decoration: underline;"><strong><a href="https://github.com/ethereum/EIPs/issues/160">détails techniques ici</a></strong></span>).</li>
 	<li><strong><strong>EIP 161 - effacement du trie d'état (State trie clearing - invariant-preserving alternative)</strong></strong>Ce changement supprime un grand nombre de comptes vides qui ont été ajoutés dans la blockchain à un coût très faible en exploitant des failles dans le protocole aujourd’hui corrigées. La Hard Fork permettra ainsi de réduire la taille de la blockchain et la durée de synchronisation (<span style="text-decoration: underline;"><strong><a href="https://github.com/ethereum/EIPs/issues/161">détails techniques ici</a></strong></span>).</li>
</ul>
<ul>
 	<li><strong><strong>EIP 170 - Limite à la taille du code d’un contrat  (Contract code size limit)</strong></strong>Cette proposition corrige une vulnérabilité du protocole dans l’appel d’un contrat. Alors que l’appel a un coût fixe en gaz, il est possible que cet appel engendre un coût plus important par des lectures de la blockchain. Aujourd’hui cette vulnérabilité n’est pas vraiment exploitable du fait de la limite de gaz par bloc (<span style="text-decoration: underline;"><strong><a href="https://github.com/ethereum/EIPs/issues/170">détails techniques ici</a></strong></span>).</li>
</ul>
[caption id="attachment_1684" align="aligncenter" width="1024"]<img class="wp-image-1684 size-large" src="https://www.ethereum-france.com/wp-content/uploads/2016/11/tumblr_o9ntj0jVcS1ugyavxo1_1280-1024x723.jpg" alt="Jan de Bray - Les dirigeants de la Guilde de Saint-Luc (1675)" width="1024" height="723" /> Jan de Bray - Les dirigeants de la Guilde de Saint-Luc (1675)[/caption]
<h3><strong>Les clients Ethereum mis à jour pour l'occasion intègrent de nouvelles fonctionnalités remarquables</strong></h3>
Notez au passage le nom de ce hard fork « Spurious Dragon » que l’on pourrait traduire par « dragon parasite » ; les développeurs ayant probablement l’impression de refermer le roman de l’attaque par déni de service.

Cela se retrouve dans les versions mises à jour des clients <strong>Geth</strong> (Go-ethereum) :
<ul>
 	<li><strong><span style="text-decoration: underline;"><a href="https://github.com/ethereum/go-ethereum/releases/tag/v1.5.0">Let There be Light v1.5.0</a></span> </strong>récemment amendée en <span style="text-decoration: underline;"><strong><a href="https://github.com/ethereum/go-ethereum/releases/tag/v1.5.2">1.5.2</a></strong></span></li>
 	<li><span style="text-decoration: underline;"><strong><a href="https://github.com/ethereum/go-ethereum/releases/tag/v1.4.19">Garbage Man v1.4.19</a></strong></span></li>
</ul>
La version 1.5.0 de Geth  est un jeu de mots faisant référence une annonce très attendue. « <em>Let there be Light</em> » apporte (<span style="text-decoration: underline;"><strong><a href="https://blog.ethereum.org/2016/11/17/whoa-geth-1-5/">entre autres</a></strong></span>) une librairie Android et iOS ainsi qu’une version alpha d’un client léger (« <em>light </em>») qui permet de se synchroniser en quelques minutes en ne téléchargeant que quelques mégabytes. Ceci permettra à des appareils très léger dans l’IoT ou dans la téléphonie de devenir des nœuds du réseau.

Enfin, Geth 1.5 implémente une preuve de concept du protocole de stockage décentralisé Swarm dont nous aurons l’occasion de reparler notamment avec une interview à venir de Viktor Tròn.

Pour les utilisateurs de <strong>Parity</strong>, le client s'offre un lifting complet et propose de <strong><span style="text-decoration: underline;"><a href="https://blog.ethcore.io/announcing-parity-1-4/">nouvelles fonctionnalités</a></span></strong> de même qu'un client précompilé sur Mac OS X (v1.4.3) :
<ul>
 	<li><span style="text-decoration: underline;"><strong><a href="https://github.com/ethcore/parity/releases/tag/v1.3.12">Stable release v1.3.12</a></strong></span></li>
 	<li><span style="text-decoration: underline;"><strong><a href="https://github.com/ethcore/parity/releases/tag/v1.4.3">Beta v1.4.3</a></strong></span></li>
</ul>