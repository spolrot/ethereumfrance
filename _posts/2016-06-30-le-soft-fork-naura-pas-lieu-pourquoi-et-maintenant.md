---
ID: 1141
post_title: 'Le (soft) fork n&rsquo;aura pas lieu. Pourquoi ? Et maintenant ?'
author: JdeTychey
post_excerpt: ""
layout: post
permalink: >
  https://www.ethereum-france.com/le-soft-fork-naura-pas-lieu-pourquoi-et-maintenant/
published: true
post_date: 2016-06-30 01:20:23
---
Décidément l’actualité sur Ethereum n’en finit plus de tourner autour du problème de l’attaque de The DAO. La proposition de <em>soft fork</em> que l’on vous décrivait précédemment <span style="text-decoration: underline"><a href="https://www.ethereum-france.com/to-fork-or-not-to-fork-telle-est-la-question/">ici</a></span> comme actée a finalement été écartée en urgence pour des raisons de sécurité.

Ce soft fork changeait le comportement des mineurs en créant une nouvelle classe de transaction: les transactions invalides. Étaient considérées comme invalides toutes les transactions invoquant le contrat de The DAO, ceci afin de bloquer l’accès aux éthers localisés sur les différents comptes utilisant le contrat de The DAO. Plus précisément les tentatives d’interaction avec la DAO initiale, avec celles utilisées par l’attaquant pour détourner les fonds, et même avec celle utilisée pour la “contre-attaque”, auraient été rejetées par les mineurs.

Mardi cette idée s’est révélée porteuse d’une importante faille de sécurité car elle ouvrait la possibilité d’une attaque sur Ethereum par déni de service. Vous pouvez en consulter les détails sur le site <span style="text-decoration: underline"><a href="http://hackingdistributed.com/2016/06/28/ethereum-soft-fork-dos-vector/">Hacking Distributed</a></span> et je vais vous en donner les grandes lignes ci-après. Le vecteur d’attaque part du principe que le rejet pour “transaction invalide” n’entraîne pas de consommation de gaz pour les mineurs… Explication.

<img class="size-medium wp-image-1142 aligncenter" src="https://www.ethereum-france.com/wp-content/uploads/2016/06/fork--300x169.gif" alt="fork" width="300" height="169" />

Pour commencer, un petit rappel sur le fonctionnement du gaz s'impose:

L’exécution d’une transaction, qu’elle soit un simple transfert d’éther ou plusieurs lignes du code d’un contrat, nécessite de rémunérer les mineurs pour la tâche exécutée. Cette rémunération se fait en éther sous la forme de gaz. Chaque opération sur Ethereum a un équivalent en nombre de gaz qui correspond à l’effort à fournir pour traiter cette opération. Ce gaz a un prix, chaque mineur peut fixer le sien qui correspond au nombre d’éther qu’il souhaite recevoir pour l’effort qu’il fournit. A la mi-juin le prix du moyen du gaz était de 0,0000000225 éther, une transaction basique de virement entre deux adresses nécessitant 21000 gaz, elle coûte donc en moyenne <span title="Gas Price * Gas Used By Transaction">0<b>,</b>00047 </span>éther en frais de traitement. Ce système a de nombreux avantages, il permet notamment:
<ul>
 	<li>Aux mineurs peu performants ou avares de refuser de traiter rapidement les opérations trop lourdes en exigeant un prix du gaz élevé;</li>
 	<li>D’éviter que certains contrats deviennent hors de prix lorsque le cours de l’éther s’apprécie; en effet le nombre de gaz nécessaire à l’exécution est défini par la complexité des opérations tandis que le prix du gaz peut être ajusté selon le cours de l’éther;</li>
 	<li>D’éviter qu’une boucle infinie dans un code ne tourne éternellement car au moment où la totalité du gaz fourni dans la transaction a été consommée, le mineur arrête de traiter l'opération et enregistre la transaction telle quelle.</li>
</ul>
Notez que sur Mist vous pouvez ajuster le gaz que vous êtes prêt à dépenser avec les "fees" en déplaçant le curseur vers "cheaper" :

<img class="aligncenter wp-image-1145 size-full" src="https://www.ethereum-france.com/wp-content/uploads/2016/06/cutmypic1.png" alt="cutmypic(1)" width="409" height="242" />

&nbsp;

Selon les frais que vous choisissez, Mist vous indique que votre transaction mettra plus ou moins de temps à être traitée ce qui représente le fait qu'il va vous falloir attendre avant qu'un mineur ne la traite. S'il n'y a aucun mineur qui accepte de traiter votre transaction compte tenu du gaz qu’elle nécessite et du prix par gaz qu’il demande… Mist renvoie le message d’erreur:

<img class="size-full wp-image-1146 aligncenter" src="https://www.ethereum-france.com/wp-content/uploads/2016/06/cutmypic.png" alt="cutmypic" width="248" height="78" />

&nbsp;

Le gaz est donc aussi un système interne pour éviter de saturer l’exécution sur la blockchain, toute opération entraînant paiement il n’y a pas d’attaque par déni de service possible.

Mais en définissant des transactions de type “invalide”, la soft fork faisait rejeter des transactions par les mineurs sans que ce rejet n’entraîne de paiement de gaz car:

<strong> Qui dit transaction rejetée dit transaction non inscrite dans la blockchain donc pas de paiement de gaz.</strong>

Cette faille permettait à un attaquant de demander l’exécution d’une transaction complexe et se finissant par une opération invalidant cette même transaction. Les nœuds du réseau se retrouvaient donc contraints d’exécuter ces opérations coûteuses avant de rejeter la transaction, sans être rémunérés pour leur effort. Une personne malintentionnée pouvait donc facilement saturer le réseau de transactions complexes sans devoir en payer le prix en gaz...

Que reste-t-il faire à présent ? Il reste le "hard fork", plus net, plus radical, mais plus difficile à développer et à faire accepter au réseau… A en juger par l’activité sur Reddit à ce sujet, il semble cependant que ces nouvelles difficultés commencent à faire pencher la communauté en sa faveur.

[caption id="attachment_1143" align="aligncenter" width="300"]<img class="wp-image-1143 size-medium" src="https://www.ethereum-france.com/wp-content/uploads/2016/06/Hector-et-Andromaque-Johann-Heinrich-Tischbein-XVIIIe-300x226.jpg" alt="Hector et Andromaque, Johann Heinrich Tischbein XVIIIe" width="300" height="226" /> <em> Johann Heinrich Tischbein - Hector et Andromaque (XVIIIe)</em>[/caption]