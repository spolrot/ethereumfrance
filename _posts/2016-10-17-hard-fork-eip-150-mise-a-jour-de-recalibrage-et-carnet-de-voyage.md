---
ID: 1565
post_title: 'Hard-fork EIP-150 : mise à jour de recalibrage et carnet de voyage'
author: JdeTychey
post_excerpt: ""
layout: post
permalink: >
  https://www.ethereum-france.com/hard-fork-eip-150-mise-a-jour-de-recalibrage-et-carnet-de-voyage/
published: true
post_date: 2016-10-17 22:41:54
---
<em>Décompte avant la mise à jour :<strong><a href="https://fork.codetract.io/"> https://fork.codetract.io/</a></strong></em>

<em>Pour mettre à jour <strong><a href="https://github.com/ethereum/mist/releases">Mist ou Ethereum Wallet cliquez ici!</a></strong></em>

Ethereum subit depuis 1 mois une attaque par déni de service (DoS) qui a commencé le premier jour de la DEVCON2. Cette attaque a tenté de saturer et faire crasher les nœuds du réseau qui a montré sa résistance. Une EIP (Ethereum Improvement Proposal) a été finalisée en milieu de semaine dernière et sera déployée dans un hard fork au bloc 2 463 000 (soit demain mardi un peu avant 15h) pour corriger les failles exploitées.

Retour sur un mois agité sur Ethereum, sur le contenu et sur les conséquences de cette mise à jour.

<strong>Un mois de gros temps où la résilience du réseau a fait ses preuves</strong>

[caption id="attachment_1571" align="aligncenter" width="1024"]<img class="wp-image-1571 size-large" src="https://www.ethereum-france.com/wp-content/uploads/2016/10/Joseph-Mallord-William-Turner-Snow-Storm-Steam-Boat-off-a-Harbours-Mouth-WGA23178-1024x766.jpg" alt="J.M.W. Turner - Tempête de neige en mer (1842)" width="1024" height="766" /> J.M.W. Turner - Tempête de neige en mer (1842)[/caption]

&nbsp;

Au bloc 2,283,249, c’est-à-dire le 18 septembre aux alentours de 4h du matin à Shanghai, un contrat malicieux a été déployé par la transaction<a href="https://etherchain.org/tx/0x21090b64f0a5e7645c81fa60f80e809c61e3a1809cc95d2191fe95ec63ca05bc"> 0x21090b64(…)</a>. Le langage machine (en OPCODE) de ce contrat est consultable à cette adresse<strong><a href="https://etherchain.org/account/0xd6a64d7e8c8a94fa5068ca33229d88436a743b14#codeDisasm"> 0xd6a64d7e(…)</a></strong>. Il contient l’opération PUSH20 qui met sur la pile des opérations l’écriture d’une chaîne de caractères de 20 bytes « fromshanghaiwithlove » faisant sans doute référence à DEVCON2 qui devait commencer dans les heures suivantes. On trouve dans ce contrat l’opération EXTCODESIZE qui demande la lecture de la taille du code contenu dans un compte Ethereum. Cette opération s’est avérée sous-estimée dans le calibrage des coûts en gaz initialement réalisé dans le<strong><a href="http://gavwood.com/paper.pdf"> yellow paper d’Ethereum</a> </strong>(cf. Gextcode dans l’appendice G) pour les opérations sur Ethereum.

Pour rappel, le système de gaz permet entre autre de résoudre le<strong><a href="https://fr.wikipedia.org/wiki/Probl%C3%A8me_de_l%27arr%C3%AAt"> problème de l’arrêt</a></strong> dans la machine virtuelle Ethereum. A chaque opération correspond un coût en gaz et l’exécution d’une transaction s’interrompt lorsque le gaz fourni pour la transaction est épuisé. L’exécution d’une transaction, qu’elle soit un simple transfert d’ether ou plusieurs lignes du code d’un contrat, nécessite de rémunérer le premier mineur qui valide initialement l’opération en l’incluant dans un bloc. Tous les nœuds complets (full nodes) vérifient à leur tour l’état de la blockchain inscrit dans chaque bloc que les mineurs diffusent en exécutant eux aussi les opérations demandées par les transactions. Les mineurs sont libres de fixer le prix en ether pour une unité de gaz mais pas la quantité de gaz à attribuer aux différentes opérations. Avec le jeu de la concurrence entre les mineurs, ils sont incités à ne pas trop augmenter le prix au risque que les transactions soient inscrites dans le prochain bloc par un autre mineur moins cher.

Pour illustrer ce mécanisme, à la mi-juin le prix du moyen du gaz était de 0,0000000225 ether en moyenne. Une transaction basique de virement entre deux adresses nécessitant 21000 gaz, elle coûte donc en moyenne 0,00047 ether en frais de traitement. La flexibilité du prix du gaz permet de garantir une certaine stabilité du coût d’exécution : si le prix en euros de l’éther venait à doubler les mineurs pourraient diviser par deux le prix du gaz pour que les frais de traitement restent stables en euros. Le gaz est donc un système interne pour éviter de saturer l’exécution sur la blockchain et, toute opération entraînant paiement, il n’y a pas d’attaque par déni de service possible sauf en cas d’écart entre le coût calibré de l’opération et son coût réel.

L’attaque DoS a consisté à innonder le réseau de transactions en faisant appel à diverses opérations dont le coût d’exécution ne correspondait pas à la charge réelle de traitement pour les nœuds du réseau. Cette attaque a d’abord affecté sévèrement les nœuds utilisant Geth, la version plus populaire du client Ethereum (écrit en Go) qui ont rapidement crashé. Il faut avoir à l’esprit que contrairement à Bitcoin où plus de <a href="https://coin.dance/nodes/share">96% des clients sont dérivés de Core</a> (écrit en C++), la blockchain Ethereum est implémentée dans plusieurs clients qui ne traitent pas l’exécution des opérations avec les mêmes contraintes. La seconde version la plus populaire (Parity, écrite en Rust) a rapidement pris le relais sur le réseau. La plupart des clients ci-dessous ont mis en ligne des versions intégrant EIP 150 :
<table>
<tbody>
<tr>
<td><b>Client</b></td>
<td><b>Langage</b></td>
<td><b>Développeurs</b></td>
</tr>
<tr>
<td><a href="http://ethdocs.org/en/latest/ethereum-clients/go-ethereum/index.html#go-ethereum">go-ethereum</a></td>
<td>Go</td>
<td><a href="https://ethereum.org/foundation">Ethereum Foundation</a></td>
</tr>
<tr>
<td><a href="http://ethdocs.org/en/latest/ethereum-clients/parity/index.html#parity">Parity</a></td>
<td>Rust</td>
<td><a href="https://ethcore.io/">Ethcore</a></td>
</tr>
<tr>
<td><a href="http://ethdocs.org/en/latest/ethereum-clients/cpp-ethereum/index.html#cpp-ethereum">cpp-ethereum</a></td>
<td>C++</td>
<td><a href="https://ethereum.org/foundation">Ethereum Foundation</a></td>
</tr>
<tr>
<td><a href="http://ethdocs.org/en/latest/ethereum-clients/pyethapp/index.html#pyethapp">pyethapp</a></td>
<td>Python</td>
<td><a href="https://ethereum.org/foundation">Ethereum Foundation</a></td>
</tr>
<tr>
<td><a href="http://ethdocs.org/en/latest/ethereum-clients/ethereumjs-lib/index.html#ethereumjs-lib">ethereumjs-lib</a></td>
<td>Javascript</td>
<td><a href="https://ethereum.org/foundation">Ethereum Foundation</a></td>
</tr>
<tr>
<td><a href="http://ethdocs.org/en/latest/ethereum-clients/ethereumj/index.html#ethereum-j">Ethereum(J)</a></td>
<td>Java</td>
<td><a href="http://www.ether.camp/">&lt;ether.camp&gt;</a></td>
</tr>
<tr>
<td><a href="http://ethdocs.org/en/latest/ethereum-clients/ruby-ethereum/index.html#ruby-ethereum">ruby-ethereum</a></td>
<td>Ruby</td>
<td><a href="https://github.com/janx/">Jan Xie</a></td>
</tr>
<tr>
<td><a href="http://ethdocs.org/en/latest/ethereum-clients/ethereumh/index.html#ethereumh">ethereumH</a></td>
<td>Haskell</td>
<td><a href="http://www.blockapps.net/">BlockApps</a></td>
</tr>
</tbody>
</table>
&nbsp;

<strong>Branle-bas de combat du milieu de la nuit au petit matin à Shanghai</strong>

Comme écrit plus haut l’attaque est survenue dans la nuit précédant le début de DEVCON2 qui rassemblait la très grosse majorité des développeurs de l’écosystème et de la Fondation. Cette attaque aurait pu ruiner l’événement mais force est de constater que les développeurs ont réagi promptement et efficacement à cette attaque. L’ensemble de la presse spécialisée a d’ailleurs salué cette réactivité. Dès les premières heures qui ont suivi l’attaque, les membres de l’équipe responsable de go-ethereum s’affairaient à préparer un correctif tandis que les coopératives (les pools) de mineurs s’appliquaient à adapter le prix du gaz et le traitement des transactions pour maintenir le réseau à flot.

[caption id="attachment_1570" align="aligncenter" width="1024"]<img class="size-large wp-image-1570" src="https://www.ethereum-france.com/wp-content/uploads/2016/10/fixinf-ethbug-at-5am-devcon2-credit-Alex-van-de-Sande-1024x772.jpg" alt="Bon baiser de (Russie/) Shanghai) - l'équipe de Go ethereum réagit à l'attaque" width="1024" height="772" /> Bons baisers de <del>Russie</del> Shanghai - l'équipe de Go Ethereum contre-attaque dans la war room improvisée de l'Hyatt on the Bund à 5h heure locale - crédit Alex van de Sande[/caption]

Une des grosses difficultés de l’opération contre cette première vague de l’attaque semble avoir été de parvenir à mettre en ligne la nouvelle version à travers le<strong><a href="https://fr.wikipedia.org/wiki/Grand_Firewall_de_Chine"> Grand Firewall de Chine</a></strong>. Au final le lancement de DEVCON2 a été retardé de 30 minutes après la mise en ligne de la version 1.4.12 de go-ethereum nommée « From Shanghai, with love ». L’effervescence autour de l’attaque et les contributions de la communauté ont produit une analyse constante de la situation et des mouvements suspects dans la blockchain. On a pu par exemple remarquer, quelques blocs après le déploiement du contrat de l’attaque, la transaction suspecte<strong><a href="https://etherscan.io/tx/0x5c19695f50a30abbadfeef201d695d9c95c254534019e2f6a7a590e9ef246e82"> 0x5c19695f(…)</a></strong> qui contenait le message en allemand « Rentrez à la maison » (Fahrt nach Hause) menant rapidement à l’explication de l’auteur de cette<strong><a href="https://www.reddit.com/r/ethereum/comments/53jm1n/fahrt_nach_hause_pm/"> transaction</a></strong>.

L’attaque ne s’est pas arrêtée pour autant et plusieurs autres abus du calibrage des opérations ont eu lieu régulièrement depuis « From Shanghai, with love ». Ces attaques ont aussi affecté le client Parity et également la chaîne minoritaire Ethereum Classic (ETC). Plutôt que de passer dans les<strong><a href="https://github.com/ethereum/go-ethereum/releases"> détails techniques</a></strong> des opérations concernées par les étapes successives de l’attaque et des corrections apportées, je me contenterai de donner les noms des nombreuses versions qui se sont suivies jusqu’à la dernière qui implémente le hard fork à venir :

-          From Shanghai, with love (1.4.12)
-          Into the Woods (1.4.13)
-          What else should we rewrite? (1.4.14)
-          Come at me Bro (1.4.15)
-          Dear Diary (v1.4.16)
-          Poolaid (v1.4.17)
-          Note 7 (v1.4.18)

<strong>Un mois de réseau ralenti mais jamais entravé</strong>

[caption id="attachment_1572" align="aligncenter" width="1024"]<img class="size-large wp-image-1572" src="https://www.ethereum-france.com/wp-content/uploads/2016/10/Ulysse-se-moquant-de-Polyphème-1829.-1024x640.jpg" alt="J.M.W. Turner - Ulysse se moquant de-polypheme (1829)" width="1024" height="640" /> J.M.W. Turner - Ulysse se moquant de-polypheme (1829)[/caption]

&nbsp;
<ul>
 	<li><strong>L’état du réseau</strong></li>
</ul>
Une des réactions pour contenir l’attaque a été d’augmenter le prix de gaz et celui-ci a doublé puis triplé en moyenne depuis la mi-septembre :
<img class="aligncenter size-large wp-image-1588" src="https://www.ethereum-france.com/wp-content/uploads/2016/10/gaz-price-1-1024x385.png" alt="gaz-price" width="1024" height="385" />
La taille moyenne des blocs exprimée en gaz a également été changée par les mineurs vers le plafond de 500K gaz pour faire face aux dernières attaques :

<img class="aligncenter size-large wp-image-1586" src="https://www.ethereum-france.com/wp-content/uploads/2016/10/blocksize-1-1024x382.png" alt="blocksize" width="1024" height="382" />

Du fait des disparités dans la diffusion des stratégies de contre-attaque,  les uncles (qui sont des blocs valides mais diffusés trop tardivement aux noeuds du réseau) ont été très nombreux sur la période tandis que le blocktime (le temps entre les blocs) est resté constant à 14 secondes.

<img class="aligncenter size-large wp-image-1587" src="https://www.ethereum-france.com/wp-content/uploads/2016/10/uncle-1-1024x403.png" alt="uncle" width="1024" height="403" />

Ce tumulte sur le réseau a eu pour conséquence de reporter le déploiement ou de perturber la vente des tokens de quelques gros contrats. L’EIP 150 règlera les problèmes de calibrage des coûts en gaz des opérations impliquées dans l’attaque. On retrouve parmi elles majoritairement des opérations liées à l’utilisation de la mémoire de la machine virtuelle Ethereum (EVM).

[caption id="attachment_1573" align="aligncenter" width="1024"]<img class="size-large wp-image-1573" src="https://www.ethereum-france.com/wp-content/uploads/2016/10/Rain-Steam-and-Speed-–-The-Great-Western-Railway-1024x765.jpg" alt="J.M.W. Turner - Pluie, Vapeur et Vitesse (1844)" width="1024" height="765" /> J.M.W. Turner - Pluie, Vapeur et Vitesse (1844)[/caption]

Ces changements vont affecter à la marge le fonctionnement de contrats déjà déployés,<strong><a href="https://np.reddit.com/r/ethereum/comments/57ork1/ive_made_a_list_of_contracts_which_will_be_100/"> l’analyse de la blockchain</a></strong> ayant pu mettre en évidence environ 111 ethers répartis sur quelques 570 contrats qui pourraient être inutilisables après le hard fork.
<ul>
 	<li><strong>Une mise à jour par hard fork et après ?</strong></li>
</ul>
Ce mois d’attaque a donné lieu à des réflexions diverses comme la possibilité d’organiser « <strong><a href="https://www.reddit.com/r/ethereum/comments/572n4q/on_gas_price_markets/">un gas price market </a></strong>» ou d’autres plus philosophiques sur<strong><a href="https://www.reddit.com/r/ethereum/comments/57hqyg/thoughts_on_our_values_as_a_community/"> les valeurs de la communauté</a></strong>, ce dont nous aurons peut-être l’occasion de parler ultérieurement. La notion d’anti-fragilité théorisée par<strong><a href="https://fr.wikipedia.org/wiki/Nassim_Nicholas_Taleb"> Nassim Nicholas Taleb</a></strong> revient régulièrement dans les discussions sur les réseaux sociaux pour qualifier Ethereum et sa communauté. Ethereum apparaît comme un projet jeune et dynamique qui croît et s’améliore au gré des attaques, des aléas, de son exposition à la volatilité et des passions que le projet suscite. Cette caractéristique est d’être anti-fragile, c’est-à-dire à l’opposé du fragile.  Un projet résilient résiste aux chocs et reste le même, un anti-fragile survit et s’améliore.

Dès les premiers jours de l’attaque il a été mis en évidence que<strong><a href="https://www.reddit.com/r/ethereum/comments/544y1p/some_blockchain_analysis_of_the_current_dos/"> cette opération était très coûteuse</a></strong> pour son ou ses auteurs. Plusieurs milliers d’euros par jour ont été dépensés sans que le cours de l’ether ne s’effondre alors que la Fondation Ethereum dispose d’un programme de<strong><a href="https://bounty.ethereum.org/"> bug bounty</a></strong> pour rémunérer les développeurs trouvant un bug. On peut dès lors questionner les motivations d’une telle attaque : s’agissait-il d’un test grandeur nature de la robustesse du réseau ou simplement de l’expression de la volonté de voir Ethereum échouer?

Si l’on retrace l’origine des fonds utilisés par les adresses de l’attaque, on débouche sur des conversions depuis la plateforme<strong><a href="https://shapeshift.io/"> Shapeshift</a></strong>. Pour les amateurs d’enquête, j’ai pu remonter les opérations sur Shapeshift jusqu’à ces deux transactions sur Bitcoin <strong><a href="http://btc.blockr.io/tx/info/64793d565a20564731671d3ec454fac227f9a709ac278816664a518d3efdcf98">64793d56(…)</a></strong> et <strong><a href="http://btc.blockr.io/tx/info/8553e73063d695162866557b773b5fbc4f325a5dd2157543e88691f534997c10">8553e730(…)</a></strong>. Il demeure cependant peu probable que l’on découvre un jour le ou les auteurs de cette attaque.

Il apparaît clairement que l’ambition du projet Ethereum s’accompagne d’une surface d’attaque très importante. Et pour conclure, en reprenant le titre d’un article de Genesis mining après le hard fork de juillet :

-         <strong><a href="http://blog.genesis-mining.com/quo-vadis-ethereum"> Quo vadis Ethereum ?</a></strong>

<strong>-          Curro de furca in furcam et melior factus sum</strong>

<i>(Où vas-tu Ethereum ? Je cours de fourche en fourche et je m’améliore)</i>

[caption id="attachment_1574" align="aligncenter" width="656"]<img class="size-full wp-image-1574" src="https://www.ethereum-france.com/wp-content/uploads/2016/10/J.M.W.-Turners-unfinished-painting-Sun-Setting-Over-a-Lake.jpg" alt="J.M.W. Turner - Coucher de soleil sur un lac (vers 1840 - inachevé)" width="656" height="480" /> J.M.W. Turner - Coucher de soleil sur un lac (vers 1840 - inachevé)[/caption]

<span style="color: #ff0000;"><strong>Bonus </strong></span>: la première intervention de DEVCON2, Ethereum en 25 minutes !

[embed]https://www.youtube.com/watch?v=66SaEDzlmP4[/embed]

&nbsp;