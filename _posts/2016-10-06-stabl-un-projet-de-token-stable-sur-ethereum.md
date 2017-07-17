---
ID: 1496
post_title: >
  Stabl, un projet de token stable sur
  Ethereum
author: Simon Polrot
post_excerpt: ""
layout: post
permalink: >
  https://www.ethereum-france.com/stabl-un-projet-de-token-stable-sur-ethereum/
published: true
post_date: 2016-10-06 23:23:05
---
[caption id="attachment_1503" align="alignright" width="200"]<img class="size-full wp-image-1503" src="https://www.ethereum-france.com/wp-content/uploads/2016/10/Hadrien-Charlanes.jpg" alt="Hadrien Charlanes, à l'initiative de Stabl" width="200" height="200" /> Hadrien Charlanes, à l'initiative de Stabl[/caption]

Hadrien Charlanes <span style="text-decoration: underline;"><a href="https://bitcoin.fr/entretien-avec-hadrien-charlanes/">présente, dans une interview réalisée par Julien Béranger et publiée sur Bitcoin.fr</a>,</span> son projet de token non-volatile <em><span style="text-decoration: underline;"><a href="https://github.com/ConsenSys/Stabl-API">Stabl</a></span></em>, qu'il développe au sein de la société <a href="https://consensys.net/"><span style="text-decoration: underline;">ConsenSys</span></a>. Les <em>stables tokens</em> sont des actifs virtuels qui ont pour ambition d'avoir un cours stable par rapport à un monnaie fiat ou à un panier de monnaies défini.

Il met notamment l'accent sur les avantages d'un stable token déployé sur une chaine publique comme Ethereum :
<blockquote>Le stable coin parfait sera celui qui sera totalement décentralisé, autrement dit les mécaniques qui font que ce token garde une valeur stable restent<em> on-chain</em>, on ne se repose pas sur quelque chose qui serait <em>off-chain</em>. Dans l’idéal, ce token serait 100% liquide, c’est-à- dire qu’on pourrait l’échanger facilement contre ce qu’on veut comme on veut. Il faudra aussi qu’il soit disponible sur une plateforme d’échange décentralisée. Le fait que cette plateforme d’échange soit elle-même décentralisée permet à la fois de proposer ce service aux traders mais aussi aux contrats déployés sur la blockchain d’Ethereum : tout ce qui est <em>on-chain</em> est accessible à la fois par de nombreux utilisateurs mais aussi par les contrats qui sont sur cette chaîne, celle d’Ethereum en l’occurence.</blockquote>
Il pointe les limites des modèles existants...
<blockquote>Le stable coin parfait serait une sorte de banque centrale autonome, un contrat qui agirait comme une banque centrale avec des share holders. [...] Dans ce « modèle parfait », la difficulté est de réussir à mettre en place les bonnes structures d’<em>incentive</em> pour que tout fonctionne bien, d’ailleurs c’est ce qu’essaie de faire <a href="https://makerdao.com/" target="_blank"><em>MakerDAO</em></a>. [...] Il est également possible d’adopter l’approche MVP (<em>Minimum Viable Product</em>) pour répondre aux besoins des traders (liquidité et disponibilité sur les plateformes d’échanges) : [...] pour chaque token émis, un vrai dollar est stocké <em>off-chain</em>. Ce système est acceptable pour les traders mais pas pour les dapps. Les développeurs de dapps recherchent plutôt un système dont le mécanisme de stabilité serait <em>on-chain</em> et décentralisé sinon la dapp elle-même perd son intérêt : on ne veut pas de tiers de confiance.</blockquote>
...et décrit son approche qui doit lui permettre de déployer un premier produit rapidement...
<blockquote>Si le prix de l’ether est à 10 dollars, tu vas pouvoir acheter 10 USD-token, elle va envoyer 1 ether sur un de nos contrats. Dans ce contrat, il y a ce qu’on appelle des <em>collaterals</em> (« fonds de garantie ») : c’est une quantité de token stockée dans le contrat. [...] Ce modèle est très simple mais il est assez robuste.</blockquote>
... et les limites de cette première approche :
<blockquote>Le système se veut très robuste mais comme il faut bloquer beaucoup d’ether pour chaque token, on ne peut pas émettre une quantité infinie de stable coin, c’est pour ça que j’assume le fait que ce stable token n’est pas « 100% liquide », c’est-à-dire qu’au lieu de créer un marché ouvert de stable coins (que n’importe qui pourrait acheter), je réserve ces stable coins aux développeurs de dApps qui vont par exemple dire « j’ai besoin d’un stable coin pour une campagne de 100 dollars donc je veux interagir avec un contrat qui contienne au moins 400 dollars qui vont me permettre de les échanger contre du dollar ». [...] le modèle n’est pas parfait, c’est un début. On veut expérimenter tout ça dans un premier temps. On passera à un modèle plus scalable au fur-et-à-mesure de l’adoption.</blockquote>
Plus de détails et la suite de l'interview <a href="https://bitcoin.fr/entretien-avec-hadrien-charlanes/"><span style="text-decoration: underline;">sur bitcoin.fr</span></a>.