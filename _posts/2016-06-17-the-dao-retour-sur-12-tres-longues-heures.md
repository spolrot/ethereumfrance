---
ID: 1060
post_title: 'The DAO: retour sur 12 très longues heures'
author: JdeTychey
post_excerpt: ""
layout: post
permalink: >
  https://www.ethereum-france.com/the-dao-retour-sur-12-tres-longues-heures/
published: true
post_date: 2016-06-17 19:40:04
---
<img class="aligncenter wp-image-1061 size-large" src="https://www.ethereum-france.com/wp-content/uploads/2016/06/Le-Radeau-de-la-Méduse-1024x699.jpg" alt="Le-Radeau-de-la-Méduse" width="1024" height="699" />

<i>TheDAO est (<strong>était?</strong>) la première organisation autonome décentralisée sur la blockchain Ethereum. Ce matin cette organisation a été victime d'une attaque de grande ampleur visant à détourner ses fonds. Sur les 11 millions d'ethers (soit environ 143 millions d'euros) qui avait récoltés lors d'une opération de crowdfunding historique, plus de 3,6 millions ont d'ores et déjà été siphonnés sur cette</i><a href="https://live.ether.camp/account/304a554a310c7e546dfe434669c62820b7d83490"> <i>adresse</i></a><i>. Retour sur la journée où le premier fonds d'investissement décentralisé est mort sans avoir pu financer de projet. Illustration  :  <em>Le Radeau de La Méduse - Théodore Géricault 1819</em>.
</i>

Avant de commencer rappelons ce qu’est The DAO. C'est avant tout un code informatique qui réplique les différentes fonctionnalités d'un fonds d'investissement avec une approche décentralisée. Toute personne est libre de soumettre une proposition de financement à The DAO qui donne lieu à un vote, les membres se prononcent alors au prorata des Ethers qu'ils ont déposés dans The DAO. Parmi les fonctions du "logiciel" ou smartcontract de The DAO, il est possible aux membres de s'extraire de la DAO par un "split". Concrètement cette fonction déplace les fonds des membres qui en font usage vers une autre adresse sur la blockchain, elle permet ainsi à ces membres de sortir de la DAO avec les fonds qu'ils ont investis. Cette fonction bloque par construction les fonds dans la nouvelle adresse pendant 27 jours pour différentes raisons, cette précision est importante pour la suite.

Toute l'affaire qui s'est déroulée aujourd'hui a commencé hier par la diffusion d'un article sur ce<a href="http://hackingdistributed.com/2016/06/16/scanning-live-ethereum-contracts-for-bugs/"> blog</a> faisant état d'un bug important dans certains contrats. Ce dernier article faisait écho à un autre de la semaine dernière par<a href="http://vessenes.com/more-ethereum-attacks-race-to-empty-is-the-real-deal/"> Peter Vessenes</a>. De quoi s'agit il ? Ces articles décrivent la possibilité d'exploiter des failles dans les fonctions de retrait des fonds logés dans les contrats Ethereum. Grâce à un appel récursif à la fonction de retrait, un attaquant peut obtenir une multitude de fois la somme qu'il est en droit de retirer. Pour se figurer cette attaque, imaginez qu'appuyer de nombreuses fois sur le bouton "100 euros" d'un bancomate entraîne la sortie d'autant de billets sans générer de problème de débit sur votre compte... L'opération peut durer tant qu'il reste des billets dans la machine.

Cette attaque est précisément ce qui s'est passé aujourd'hui:
<ul>
 	<li>aux alentour de 9h30</li>
</ul>
L'agitation sur le slack de la DAO et de slock.it se manifeste par l'un des utilisateurs les plus actifs, Griff Green. Il signale qu'une attaque semble être en cours. Plusieurs splits se comportent de manière suspecte et Griff Green cherche à contacter le ou les auteurs de l'opération. Très rapidement il se confirme qu'il s'agit bien d'une attaque.

<img class="aligncenter wp-image-1063 size-large" src="https://www.ethereum-france.com/wp-content/uploads/2016/06/image-1024x511.png" alt="image" width="1024" height="511" />
<ul>
 	<li>aux alentour de 10h30</li>
</ul>
Slock.it et d'autres développeurs du code de la DAO organisent une contre-attaque consistant à spammer certaines fonctions de la DAO et à ralentir par divers moyens le déroulement des appels malveillants à la fonction de split. Les différentes places de marché coupent la cotation des token DAO et parfois même de l'Ether. Les sites qui permettent d'explorer la blockchain sont nombreux à être inaccessibles ou à ne plus mettre à jour les blocs. Pendant ce temps certains mineurs ont coupé leur machines, la puissance de calcul du réseau recule de plusieurs THash. Il devient très difficile de faire une opération sur Ethereum.
<ul>
 	<li>aux alentour de 11h30</li>
</ul>
La mobilisation de la communauté se poursuit pour ralentir l'opération et y apporter une solution. Plusieurs millions d'Ethers ont été transférés sur cette<a href="https://live.ether.camp/account/304a554a310c7e546dfe434669c62820b7d83490"> adresse</a>, ils y sont néanmoins bloqués pour 27 jours avant de pouvoir être déplacés par l'attaquant.
<ul>
 	<li>à la mi-journée</li>
</ul>
La fondation Ethereum s'exprime sur le sujet et propose une solution. Le retour des fonds dérobés nécessitera un <i>hard fork</i> (HF), c'est à dire faire recommencer tous les nœuds du réseau à partir de l'état de la blockchain précédant l'attaque. La fondation propose dans l'immédiat un <i>soft fork</i> (SF) consistant à "bannir" de la blockchain l'adresse sur laquelle les fonds de la DAO ont été déportés. Le SF nécessitera que la majorité des noeuds du réseau accepte une mise à jour, après quoi les fonds localisés dans l'adresse incriminée ne pourront être déplacés. Seul le HF permettra de rembourser les investisseurs lésés.

Ces deux forks seront soumis aux noeuds qui décideront donc à la majorité et successivement si oui ou non ils acceptent la SF puis si oui ou non ils acceptent le HF. Le code de la DAO serait changé vers un contrat simple remboursant chacun des investisseurs et mettant fin à la DAO.

Les<a href="https://blog.ethcore.io/attack-on-thedao-what-will-be-your-response/"> principaux développeurs</a> d'Ethereum ainsi que<a href="https://www.reddit.com/r/ethereum/comments/4oj7ql/personal_statement_regarding_the_fork/"> Vitalik Buterin</a> se sont exprimés à ce sujet.

Y aura-t-il <i>Soft Fork</i> puis <i>Hard Fork</i>, l'un mais pas l'autre, aucun des deux ? Le débat sur l'opportunité des options et des signaux envoyés fait déjà rage dans la communauté, soyez assuré que des articles de fond sont à venir.

En tout cas cette affaire ne remet pas en cause l'intégrité de la blockchain Ethereum. Quand à la DAO, le concept et son code seront sans doute amenés à être poursuivis et améliorés afin de garantir qu’un événement de ce type ne survienne plus.

<img class="aligncenter wp-image-1062 size-large" src="https://www.ethereum-france.com/wp-content/uploads/2016/06/liberté-peuple-1024x821.jpg" alt="liberté-peuple" width="1024" height="821" />
<p style="text-align: center;"><em>La Liberté guidant le peuple - Eugène Delacroix, 1830</em></p>
&nbsp;