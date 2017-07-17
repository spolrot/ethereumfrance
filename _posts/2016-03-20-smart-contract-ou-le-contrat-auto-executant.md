---
ID: 371
post_title: >
  « Smart contract », où le contrat
  auto-exécutant
author: Simon Polrot
post_excerpt: ""
layout: post
permalink: >
  https://www.ethereum-france.com/smart-contract-ou-le-contrat-auto-executant/
published: true
post_date: 2016-03-20 23:20:19
---
L’apport essentiel d'Ethereum, lorsqu’on la compare aux autres <em>blockchain</em> existantes, se résume dans sa capacité à être <strong>programmée</strong> à l’aide d’un langage dédié (<span style="text-decoration: underline;"><a href="https://github.com/ethereum/wiki/wiki/The-Solidity-Programming-Language">Solidity</a></span>). Ce langage est dit « <em>turing-complete</em> », ce qui signifie qu’il permet d’exécuter l’ensemble des fonctions utilisés pour développer une application moderne : c'est un langage de programmation « complet »<span style="font-size: 10pt;"><sup><a href="#_ftn1" name="_ftnref1">[1]</a></sup></span>.
<h4><strong>La possibilité de programmer simplement des « contrats »…</strong></h4>
Cette caractéristique permet d’envisager la programmation d’engagements, simples ou complexes, sur la blockchain Ethereum. Ces engagements sont appelés par les créateurs d’Ethereum « <em>smart contracts</em> ». Ils sont dits « <em>smarts</em> », intelligents, car lorsque les conditions d’exécution de ces engagements sont réunies, ceux-ci s’exécutent automatiquement sur la blockchain, en prenant en compte l’ensemble des conditions et des limitations qui avaient été programmés dans le contrat à l’origine.

L'un des exemples le plus simple d'un "smart contract" est celui d'un contrat de prestation entre deux personnes. La première (A) souhaite rémunérer la seconde (B) pour l’exécution de cette prestation. Cet engagement est formalisé dans la blockchain Ethereum par la création d’un smart-contrat. Lors de la formalisation de ce smart-contract, A met en gage sur la blockchain le montant de la rémunération prévue pour B. Lorsque la prestation est réalisée, l'une des parties exécute le contrat. Celui-ci vérifie automatiquement que la prestation a bien été effectuée. Si tel est le cas, B reçoit la rémunération prévue. Dans le cas contraire, A récupère le montant de son gage.

Mais le langage Solidity permet d’envisager :
<ul>
 	<li>Des engagements entre deux ou plusieurs parties beaucoup plus complexes, à l’image des contrats existants à ce jour : des contrats-cadre, des contrats de distribution, des contrats de royalties, des contrats de société, des pactes d’actionnaire, des gages...</li>
</ul>
<p style="padding-left: 60px;">Dans ce contexte, l’intérêt de formaliser le contrat dans la blockchain Ethereum apparaît plus significatif dans le cadre des contrats dont l’exécution peut être source de difficulté : la mise en œuvre d’une caution, les contrats comprenant un droit de préemption d’une partie, etc.</p>

<ul>
 	<li>Des programmes qui vont bien au-delà de simples engagements contractuels. Le <span style="text-decoration: underline;"><a href="https://ethereum.org/" target="_blank">site officiel de la Fondation Ethereum</a></span> comprend plusieurs exemples d’applications simples et pratiques de Solidity, qui ne manquent pas d’ambition :
<ul>
 	<li><u><a href="https://ethereum.org/token" target="_blank">La création d’une monnaie (ou actif virtuel) spécifique à un projet</a></u>, qui peut s’échanger entre les participants au projet et dont la détention est susceptible de permettre l’obtention d’avantages.</li>
 	<li><u><a href="https://ethereum.org/crowdsale" target="_blank">La mise en place d’une plateforme de financement décentralisée</a></u> pour un projet en particulier.</li>
 	<li><u><a href="https://ethereum.org/dao" target="_blank">La création d’une organisation autonome décentralisée (DAO)</a></u>, dont le principe est décrit succinctement <u><a href="http://www.ethereum-france.com/decentralized-autonomous-organization-dao-blockchain/" target="_blank">dans l’article qui lui est dédié sur ce site</a></u>.</li>
</ul>
</li>
</ul>
La liste ne s’arrête pas là. De nombreuses applications décentralisées sont aujourd’hui développés sur la base de ces « <em>smart-contrats</em> » : <u><a href="https://augur.net/" target="_blank">Augur</a></u>, <span style="text-decoration: underline;"><a href="https://slock.it/" target="_blank">Slock.it</a></span>, <u><a href="https://makerdao.com/" target="_blank">Maker</a></u>, <u><a href="https://digix.io/" target="_blank">Digix</a></u>…
<h4><strong>…qui s’exécutent une fois leurs conditions d’exécution remplies…</strong></h4>
Comme il l’a été précisé, ces « contrats » (ou programmes) s’exécutent en examinant l’ensemble des conditions d’exécution qui ont été définies à l’avance dans le code du contrat. Par exemple, si un contrat comprend comme condition de s’exécuter après le 1<sup>er</sup> janvier 2017, il sera <em>impossible</em> de l’exécuter avant cette date.

Le problème se pose alors, naturellement, de la validation de ces conditions d’exécution. Deux cas de figure sont alors envisageables :
<ul>
 	<li>Les conditions d’exécution du contrat sont liées à d’autres écritures dans la blockchain ou sont de simples repères temporels. Dans ce cas, la vérification de ces conditions exécution est très facile : le contrat est programmé pour vérifier que ces écritures existent ou que le délai d’exécution est passé, et il s’exécute lorsque c’est le cas.</li>
</ul>
<ul>
 	<li>Les conditions d’exécution du contrat sont extérieures à la blockchain (réalisation d’une prestation, survenance d’un événement…). Dans ce cas, l’exécution du contrat nécessite le recours à un tiers de confiance, appelé dans le jargon Ethereum un « <em>oracle</em>». L’oracle est chargé d’entrer dans la blockchain l’information de façon fiable afin que le contrat puisse s’exécuter correctement. Cet oracle peut être constitué de plusieurs façons :
<ul>
 	<li>Désignation préalable d’un tiers de confiance connu des deux parties ;</li>
 	<li>Référence à une base de données considérée comme « de confiance » (par exemple dans le cas d’un paris sportif, possibilité de se référer au résultat enregistré sur le site d’un journal sportif) ;</li>
 	<li>Utilisation d’un service d’Oracle décentralisé. Il s’agit d’un service existant sur la blockchain faisant appel à de nombreux participants. Chacun des participants vote pour le résultat qu’il considère comme exact et c’est le consensus entre les participants qui détermine le résultat final envoyé au contrat. Des projets d’oracles décentralisés existent déjà, notamment <u><a href="http://www.oraclize.it/" target="_blank">le projet Oraclize</a></u>.</li>
</ul>
</li>
</ul>
<h4><strong>…de façon simple, fiable, peu onéreuse et sécurisée.</strong></h4>
Une fois les conditions du contrat validées, le contrat peut s’exécuter comme programmé. Cette exécution est en pratique réalisée en envoyant une commande à la blockchain qui provoque l’exécution du contrat.

L’exécution du contrat nécessite un paiement en « gaz », qui constitue le carburant des contrats. Celui-ci est peu onéreux : l’exécution d’un contrat simple nécessite quelques centimes tout au plus, celle d’un contrat complexe jusqu’à quelques euros.

Enfin, puisque le contrat est entré sur la blockchain, il bénéficie des avantages de celle-ci, à savoir :
<ul>
 	<li><span style="text-decoration: underline;">Publicité</span> : les transactions effectuées dans la blockchain sont <span style="text-decoration: underline;">publiques</span>. Il est possible de vérifier la bonne exécution du contrat. De plus, n'importe quelle partie qui dispose du code source du contrat peut vérifier que le contrat a bien été enregistré conformément au code prévu.</li>
 	<li><span style="text-decoration: underline;">Sécurité </span>: l’ensemble de la blockchain fonctionne avec un protocole chiffré puissant qui la rend également très difficile à altérer. Pour effectuer une modification dans la blockchain, il faut réussir une attaque simultanée sur plus de 50 % des participants.</li>
 	<li><span style="text-decoration: underline;">Immuabilité</span> : les données qui sont enregistrées dans la blockchain y sont enregistrées pour toujours : la blockchain garde l’historique de toutes les modifications qui y ont été apportées depuis l’origine. Le contrat est donc enregistré de façon irrémédiable dans la blockchain.</li>
 	<li><span style="text-decoration: underline;">Fiabilité</span> : Il est virtuellement impossible d’arrêter simultanément tous les ordinateurs participants à la blockchain. Par conséquent, cette base de données est toujours en ligne et son fonctionnement ne s’arrête jamais.</li>
</ul>
<strong>En synthèse</strong>, les « smart-contrats » offrent de nombreuses opportunités. Ils permettent d’exécuter automatiquement des accords préalablement formalisés entre deux parties, sans que l’une des parties ne puisse faire obstacle à son exécution. Ils permettent aussi d’envisager le développement d’applications complexes décentralisées. Ces contrats ou applications s'exécutent de façon sécurisée, publique et fiable, sans qu'il soit possible de les altérer.

Mais la grande force de ces « smart contrats » est aussi leur faiblesse : il est en pratique impossible, sauf à l’avoir prévu dès le départ, de modifier un contrat existant dans la blockchain après qu’il ait été enregistré dans celle-ci. La phase de conception de ces contrats nécessitera donc une particulière attention pour éviter toute déconvenue future…

&nbsp;

<span style="font-size: 8pt;"><a href="#_ftnref1" name="_ftn1">[1]</a> Théoriquement, il est donc possible de programmer des fonctions très complexes sur la blockchain Ethereum. Un programme comme un traitement de texte pourrait fonctionner exclusivement sur la blockchain. En pratique, les limitations inhérentes à la technologie (c’est-à-dire principalement sa lenteur et son coût d’exécution) rendent cette idée impraticable. Tel n’est d’ailleurs pas son objet, car on voit mal l'intérêt d'exécuter un traitement de texte de façon décentralisée...</span>