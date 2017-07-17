---
ID: 1225
post_title: 'Le Hard Fork « The DAO » aura bien lieu, mode d&#8217;emploi'
author: Simon Polrot
post_excerpt: ""
layout: post
permalink: >
  https://www.ethereum-france.com/le-hard-fork-the-dao-aura-bien-lieu-mode-demploi/
published: true
post_date: 2016-07-19 02:28:09
---
<em>C'est aujourd'hui acté : <a href="https://www.ethereum-france.com/to-fork-or-not-to-fork-telle-est-la-question/"><span style="text-decoration: underline;">un hard fork de la blockchain</span></a> est programmé pour le <strong>20 juillet 2016 (ce mercredi) vers</strong> <strong>15 heures.</strong> Les spécifications de ce fork ont été finalisées pendant le week-end et les principaux clients Ethereum ont été mis à jour dans la foulée (dont Mist et Ethereum Wallet). A compter du bloc 1 920 000, une nouvelle chaîne sera donc formée par les mineurs qui auront décidé de suivre le hard fork, tandis que les autres continueront à miner l'ancienne chaîne, inaltérée. Cette opération est loin d'être insignifiante, et elle nécessite une action de votre part si vous souhaitez suivre la nouvelle chaîne. Mode d'emploi sous forme de questions / réponses.</em>

<strong>Que va-t-il se passer exactement ? </strong>Un hard fork de la blockchain Ethereum va se déclencher au bloc 1 920 000 (<span style="text-decoration: underline;"><a href="https://etherscan.io/">compte à rebours ici</a></span>). Ce comportement a été codé par défaut dans les dernières versions des logiciels les plus utilisés de l'écosystème Ethereum (Mist et Ethereum Wallet 0.8.1 - qui offrent un choix à l'utilisateur au lancement - mais aussi geth 1.4.10 et parity 1.2.2b).

A partir de ce moment, une nouvelle chaine de blocs va être créé, parfaitement identique à l'ancienne à une exception près : dans la nouvelle, l'ensemble des ethers détenus par The DAO et les DAO-filles créées par split vont être réunis dans un contrat spécifique comprenant une seule fonction. Cette fonction permet aux détenteurs de tokens DAO d'échanger 100 de ces tokens contre 1 ether.

Ce hard fork permettra donc aux personnes ayant participé à la création de The DAO de récupérer leurs ethers investis, dont une partie avaient été dérobés par un hacker le 17 juin. Pour ceux qui auraient participé après l'augmentation du prix des tokens, pas de panique : les développeurs ont également prévu de rembourser les comptes ayant surpayé les tokens, dans un second temps. <em>In fine</em>, personne ne devrait être lésé.

Le mode d'emploi pour récupérer l'ether de ces contrats sera fourni sur ce site le cas échéant.

<strong>Que dois-je faire pour utiliser cette nouvelle blockchain ?</strong>

Si vous utilisez Mist, Ethereum Wallet, geth ou parity, il faut mettre à jour votre logiciel. <a href="https://github.com/ethereum/mist/releases/tag/0.8.1"><span style="text-decoration: underline;">Pour Mist et Ethereum Wallet, suivez le lien</span></a>.

Si vous utilisez MyEtherWallet pour accéder à votre compte, vous n'avez rien à faire. Le site a indiqué qu'il suivrait la chaine majoritaire <a href="https://www.reddit.com/r/ethereum/comments/4tjrqs/myetherwalletcom_hf_dao_withdrawal_questions/"><span style="text-decoration: underline;">sur ce fil reddit</span></a>.

Si vous utilisez Jaxx, le créateur du logiciel a également précisé sur reddit, de façon un peu lapidaire, <a href="https://www.reddit.com/r/ethereum/comments/4sv7qv/sayonara_jaxx/d5eslag"><span style="text-decoration: underline;">qu'il suivrait également la chaine majoritaire</span></a>. Rien à faire non plus de votre côté à priori.

<strong>Je suis mineur, que dois-je faire ?</strong>

Si vous minez sur un pool, c'est lui qui va décider la chaine qui va être minée au moment du hard fork (habituellement selon le résultat d'un vote, voir ci-dessous), vous n'avez donc rien à faire de particulier. Si vous minez en solo, vous devez mettre à jour votre node (geth, parity, EthereumJS...) et choisir la chaine que vous souhaitez miner selon les instructions disponibles sur les github de chacun des logiciels.

<strong>Je suis opposé au Hard Fork, suis-je obligé de le suivre ?</strong>

Non. Un hard fork repose sur un consensus des participants à la blockchain et elle consiste à créer une blockchain entièrement nouvelle. L'ancienne blockchain Ethereum, non-modifiée, continuera à exister et vous pouvez décider de l'utiliser si vous le souhaitez. C'est la raison pour laquelle la mise à jour de Mist 0.8.1 affiche à son premier lancement une boite de dialogue vous invitant à choisir la chaine que vous souhaitez suivre.

[caption id="" align="alignnone" width="1504"]<img class="" src="https://cloud.githubusercontent.com/assets/232662/16900179/a7705a00-4c1d-11e6-8027-dfb072f89810.png" width="1504" height="1384" /> "Yes" pour suivre le hard fork, "No" pour rester sur la blockchain d'origine.[/caption]

Cependant, comme l'indique cette boite de dialogue, ce choix n'est pas anodin et suivre la chaine minoritaire peut s'avérer très contreproductif. Par exemple, les échanges Kraken, Poloniex et Bitfinex ont annoncé qu'ils ne suivraient que la chaine majoritaire : il sera donc impossible de vendre vos ethers si vous suivez la chaine perdante. De même, la Fondation se concentrera uniquement sur la chaine gagnante.

<span style="text-decoration: underline;">D'un point de vue purement pratique</span>, pour éviter d'envoyer vos transactions sur une chaine qui a toute les chances d'être très minoritaire, je vous recommande de choisir aujourd'hui "Yes" pour suivre la nouvelle chaine, qui semble faire consensus (cf. ci-dessous). Dans le cas où la nouvelle chaine ne serait finalement pas la chaine majoritaire, vous pourrez toujours modifier votre choix après-coup. Dans ce cas, un article vous expliquant comment changer de chaine sera publié sur le site.

<strong>Comment est déterminée la chaine majoritaire ou "gagnante" ?</strong> Le succès d'une chaine ou d'une autre dépend de son adoption, qui est évaluée selon plusieurs facteurs : échanges, utilisateurs (nodes), mineurs, développeurs.

La Fondation Ethereum est officiellement agnostique : ils suivront  l'avis de la majorité. Cela n'empêche pas certains développeurs d'avoir un avis tranché, mais Vitalik Buterin s'est explicitement tenu à l'écart des débats.

Mais <a href="https://www.ethereum-france.com/hard-fork-ou-non-faites-entendre-votre-voix/"><span style="text-decoration: underline;">le vote effectué sur carbonvote.com</span></a> a été pris en considération par les développeurs de geth et parity : faute d'option prise par l'utilisateur, les deux optent par défaut pour la chaine avec hard fork, conformément au résultat dudit vote.

Quant aux autres développeurs, ils ont naturellement chacun leur avis. Si la position de ceux de slock.it ne fait pas grand mystère, les responsables des projets Maker (MKR) et Digix <a href="https://np.reddit.com/r/digix/comments/4th5px/digix_and_maker_announcement_regarding_ethereum/"><span style="text-decoration: underline;">ont indiqué qu'ils suivraient aussi l'avis de la majorité mais qu'ils soutiennent le principe d'un hard fork</span></a>.

Les principaux échanges, quant à eux, ont indiqués qu'ils suivraient la chaine adoptée par la majorité des mineurs au moment du fork.

Les utilisateurs choisissent la chaine qu'ils veulent utiliser au moment du lancement de Mist 0.8.1, comme indiqué plus haut.

Reste donc les mineurs, dont le poids sera a priori déterminant. Tout comme au moment du soft fork, un vote a été organisé sur les principaux pools de minage. Les résultats sont <a href="https://www.reddit.com/r/ethereum/comments/4tffta/hard_fork_voting_and_node_adoption_results/"><span style="text-decoration: underline;">synthétisés en temps réel ici</span></a>, et ils sont les suivants au moment de la rédaction de cet article (moins de 36h avant le fork) :

<img class="aligncenter wp-image-1229 size-full" src="https://www.ethereum-france.com/wp-content/uploads/2016/07/Hard-Fork-votes-pool.png" alt="Hard Fork votes pool" width="822" height="448" />

La quasi-totalité des pools devraient donc, sauf changement de dernière minute, suivre la voie du hard fork, d'autant que, d'une part, les pools f2pool et ethpool ont annoncé qu'ils suivraient en définitive la chaine minée par la majorité (quel que soit le résultat du vote pour ethpool) et, d'autre part, le pool le plus important (DwarfPool) a clôturé son vote et supportera donc le hard fork.

Si vous êtes déçus, sachez que la blockchain Ethereum "d'origine" sera en tout état de cause soutenue par une minorité qui souhaite garantir à tout prix l'immutabilité de la blockchain. Il s'agit du projet "Ethereum Classic", que vous pouvez suivre <span style="text-decoration: underline;"><a href="https://ethereumclassic.github.io/">sur ce github</a></span> ou <span style="text-decoration: underline;"><a href="https://www.reddit.com/r/EthereumClassic/">ce subreddit</a></span>.

<strong>Comment savoir quelle chaine sera "gagnante" ? </strong>Au moment du hard fork proprement dit, il y aura forcément une période de flottement, le temps de déterminer la chaine ayant le plus de puissance de calcul.

Pendant cette période, les principaux échanges ont annoncé que les retraits et dépôts d'ether seront impossibles. Une fois la chaine "gagnante" déterminée, les échanges suivront cette chaine et rouvrirons les vannes.

La blockchain "gagnante" sera alors définie par le consensus de la communauté. Elle devrait être annoncée d'abord sur <a href="https://www.reddit.com/r/ethereum/"><span style="text-decoration: underline;">reddit</span></a> ou twitter, mais une annonce sera naturellement faite ici.

<strong> Puis-je envoyer / recevoir des ethers au moment du fork ? </strong>Il est déconseillé d'envoyer des transactions sur la blockchain Ethereum au moment du hard fork. Attendez quelques heures.

&nbsp;

N'hésitez pas à poster vos questions additionnelles en commentaires. Ce post sera mis à jour pour intégrer les réponses à ces questions.

<em>A titre informatif, l'auteur de cet article détient aujourd'hui 15 000 DAO Tokens.</em>