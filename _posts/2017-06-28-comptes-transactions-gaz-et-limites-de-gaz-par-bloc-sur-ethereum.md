---
ID: 2439
post_title: >
  Comptes, transactions, gaz et limites de
  gaz par bloc sur Ethereum
author: Simon Polrot
post_excerpt: ""
layout: post
permalink: >
  https://www.ethereum-france.com/comptes-transactions-gaz-et-limites-de-gaz-par-bloc-sur-ethereum/
published: true
post_date: 2017-06-28 17:05:39
---
<em>Cet article devrait permettre de mieux comprendre les mécanismes de base derrière les comptes, les transactions, le gaz et le rôle que les mineurs jouent dans la définition de la taille des blocs sur Ethereum.</em>

<em>Cet article est une traduction intégrale d'un article de <a href="https://twitter.com/hudsonjameson">Hudson Jameson</a> réalisée par <a href="https://twitter.com/simonpolrot">Simon Polrot</a> (original <a href="http://hudsonjameson.com/2017-06-27-accounts-transactions-gas-ethereum/">ici</a>). </em><em>Note : il a été choisi de traduire le mot original </em>gas<em> par gaz car il s'agit de la traduction généralement observée. Il faut cependant préciser sur le mot originel gas est plus couramment utilisé en anglais pour désigner l'essence ou un autre carburant, ce qui prends plus de sens dans le contexte de la blockchain Ethereum.</em>
<h1><strong>Que sont les <em>comptes </em>?</strong></h1>
<h2><strong>EOA <em>(ou CPE)</em> vs. comptes de contrats</strong></h2>
Il y a deux types de comptes sur Ethereum
<ul>
 	<li>Externally Owned Accounts (ou Compte à Propriétaire Externe)</li>
 	<li>Comptes de contrats</li>
</ul>
Cette distinction va être éliminée (ou <em>abstracted</em>) <a href="https://github.com/ethereum/EIPs/pull/208">dans la prochaine mise à jour du protocole (Metropolis)</a> (EN).
<h3><strong>Externally owned accounts (EOAs) / Compte à propriétaire externe (CPE)</strong></h3>
Un compte à propriétaire externe (CEP)
<ul>
 	<li>a un solde d'ether,</li>
 	<li>peut envoyer des transactions (transférer des ether ou déclencher l'exécution du code d'un <em>smart contract</em>),</li>
 	<li>est contrôlé par des clés privées,</li>
 	<li>n'a pas de code associé.</li>
</ul>
<h3><strong>Comptes de contrats</strong></h3>
Un contrat
<ul>
 	<li>a un solde d'ether,</li>
 	<li>a un code associé,</li>
 	<li>l'exécution du code est provoqué par l'envoi de transactions ou de messages (<em>calls</em>) reçus d'autres contrats.</li>
 	<li>lorsqu'il est exécuté, réalise des opérations d'une complexité arbitraire (code Turing-complet) - dispose d'un stockage persistant propre, c'est à dire peut avoir son propre état permanent - peut appeler d'autres contrats.</li>
</ul>
Toutes les actions sur la blockchain Ethereum sont mises en branle par les transactions envoyées depuis des comptes. A chaque fois qu'un compte de contrat reçoit une transaction, son code est exécuté comme défini par ses paramètres d'initialisation envoyées avec la transaction. Le code du contrat est exécuté par la Machine Virtuelle Ethereum (Ethereum Virtual Machine - EVM) sur chaque noeud participant au réseau ; c'est une partie de leur travail de vérification des nouveaux blocs.
<h1><strong>Que sont les transactions ou les messages ?</strong></h1>
<h2><strong>Transactions</strong></h2>
Le terme “transaction” est utilisé sur Ethereum en référence à un paquet de données signé qui contient un message devant être envoyé d'un compte à propriété externe à un autre compte sur la blockchain.

Les transactions contiennent
<ul>
 	<li>le destinataire du message,</li>
 	<li>une signature qui identifie l'envoyeur et démontre son intention d'envoyer le message via la blockchain au destinataire,</li>
 	<li>un champ <code>VALUE</code> - le montant en wei (subdivision d'ether) à transférer de l'envoyeur au destinataire,</li>
 	<li>un champ de données optionnel, qui peut contenir le message envoyé à un contrat,</li>
 	<li>une valeur <code>GASLIMIT</code>, représentant le nombre maximum d'étapes de calcul que la transaction est autorisée à réaliser,</li>
 	<li>une valeur <code>GASPRICE</code>, représentant la commission que l'envoyeur est prêt à dépenser pour chaque unité de gaz. Une unité de gaz correspond à l'exécution d'une instruction atomique, c'est à dire une étape de calcul.</li>
</ul>
<h2><strong>Messages</strong></h2>
Les Contrats peuvent envoyer des “messages” à d'autres contrats. Les messages sont des objets virtuels qui ne sont jamais sérialisés et qui n'existent que dans l'environnement d'exécution Ethereum. Ils peuvent être assimilés à des appels de fonctions.

Un message contient :
<ul>
 	<li>l'envoyeur du message (implicite).</li>
 	<li>le destinataire du message</li>
 	<li>un champ <code>VALUE</code> - le montant en wei à transférer avec le message à l'adresse du contrat,</li>
 	<li>un champ de données optionnel, qui corresponds à la donnée réellement envoyée au contrat</li>
 	<li>un champ <code>GASLIMIT</code>, qui limite le montant maximum de gaz que l'exécution du code provoquée par le message peut coûter.</li>
</ul>
En substance, un message est comme une transaction, sauf qu'elle est produit par un contrat et non un acteur extérieur. Un message est produit lorsque le contrat exécutant le code exécute les opcodes <code>CALL</code> ou <code>DELEGATECALL</code>, qui produisent et exécutent un message. Les messages sont aussi parfois appelés "transactions internes." Comme une transaction, un message conduit au compte destinataire exécutant le code. Donc, les contrats peuvent entrer en relation avec d'autres contrats de la même façon que des acteurs extérieurs peuvent le faire. Notons que le terme transaction est souvent, en pratique, utilisé pour faire référence à un message. Il est donc possible de cette distinction sémantique disparaisse à terme.
<h1><strong>Qu'est-ce que le gaz (ou carburant) ?</strong></h1>
Ethereum comprend un environnement d'exécution sur la blockchain appelé l'Ethereum Virtual Machine (EVM). Chaque noeud participant au réseau exécute l'EVM comme une partie du processus de vérification des nouveaux blocs. Ils parcourent les transactions listées dans le bloc qu'ils vérifient et exécutent dans l'EVM le code dont l'exécution est demandée par la transaction correspondante. Tous les noeuds exécutent les mêmes instructions et stockent les mêmes valeurs. Le fait que l'exécution du contrat est répliquée de façon redondante auprès de chaque noeud rend naturellement l'exécution coûteuse en terme de puissance de calcul, ce doit inciter à ne pas utiliser la blockchain pour des calculs qui pourraient être effectués hors de la chaîne. Pour chaque opération exécutée, un coût est identifié, qui est exprimé en un nombre d'unité de gaz. Chaque opération qu'un contrat contient a une valeur en gaz définie. <a href="https://docs.google.com/spreadsheets/d/1m89CVujrQe5LAFJ8-YAUCcNK950dUzMQPMJBxRtGCqs/edit#gid=0">Ce document référence le coût en gaz de chaque code d'opération (opcode) sur la blockchain Ethereum - attention, il n'est pas entièrement à jour</a> (EN).
<h2><strong>Gaz et coût de transaction</strong></h2>
Chaque transaction doit inclure une limite de gaz (<a href="https://media.consensys.net/ethereum-gas-fuel-and-fees-3333e17fe1dc">parfois appelée startGas</a>- EN) et un prix qu'elle est prête à payer par unité de gaz. Les mineurs ont le choix d'inclure la transaction et de collecter le prix ou non. En pratique, toutes les transactions finissent aujourd'hui par être sélectionnées, mais le prix du gaz qu'un utilisateur choisit de payer a une influence sur le délai qui va s'écouler entre l'envoi et la sélection et le minage de la transaction dans un bloc. Si le montant total du gaz utilisé par les étapes de calcul requises pour la transaction, y compris le message original et tout autre sous-message qui pourrait être envoyé dans le cadre de l'exécution de la transaction, est inférieur ou égal à la limite de gaz définie par l'envoyeur, alors la transaction est traitée par le mineur. Si le gaz total requis par la transaction dépasse la limite de gaz fixée par l'envoyeur, tous les changements sont annulés, mais la transaction est toujours valide et les frais sont tout de même collectés par le mineur, qui a de facto exécuté la transaction. La blockchain montre alors que l'exécution de la transaction commencé, mais qu'elle ne prévoyait pas assez de gaz et que les opérations ont été annulées. Il faut aussi noter que tout excès de gaz qui n'a pas été utilisé par l'exécution de la transaction est remboursé à l'envoyeur en Ether. Comme les estimations de coût en gaz sont précisément des estimations, la plupart des utilisateurs définissent une limite en gaz volontairement élevée pour garantir que leur transaction soit acceptée. Cela ne pose pas de problème dans la mesure ou l'excès de gaz est automatiquement remboursé.
<h2><strong>Estimer les coûts de transaction</strong></h2>
Le coût total en Ether d'une transaction est basé sur deux facteurs :
<ul>
 	<li><code>gasUsed</code>: le gaz total utilisé par la transaction</li>
 	<li><code>gasPrice</code>: le prix (en ether) d'une unité de gaz, tel que spécifié dans la transaction</li>
</ul>
<strong>Coût total = gasUsed * gasPrice</strong>
<h3><strong>gasUsed</strong></h3>
A chaque opération de l'EVM est associé un coût en gaz fixe. <code>gasUsed</code> est la somme du gaz correspondant à toutes les opérations effectuées par la transaction.

Pour estimer gasUsed, il existe une <a href="http://ethereum.stackexchange.com/q/266/42">API estimateGas, qui fonctionne globalement mais avec quelques imperfections</a> (EN).
<h3><strong>gasPrice</strong></h3>
Un utilisateur construit et signe une transaction, et chaque utilisateur peut définir le <code>gasPrice</code> qu'ils souhaitent payer, qui peut même être zéro. Cependant, les clients Ethereum qui ont été lancés au moment de Frontier (version actuelle d'Ethereum) ont un <code>gasPrice</code> par défaut de 0,05e12 wei. Puisque les mineurs optimisent leurs revenus, la plupart des transactions sont envoyées avec un <code>gasPrice</code> de 0.05e12 wei, et il serait difficile de convaincre un mineur d'accepter une transaction avec un <code>gasPrice</code> inférieur, voire égal à zéro
<h3><strong>Exemple de coût d'une transaction</strong></h3>
<em>Avec leur permission, j'emprunte cet exemple et cette analogie de l'excellent MyEtherWallet. Vous pouvez lire <a href="https://myetherwallet.groovehq.com/knowledge_base/topics/what-is-gas">leur excellent guide sur le gaz ici</a> (EN). Ils ont aussi une excellente page "Utilities" sur laquelle vous pouvez trouver <a href="https://www.myetherwallet.com/helpers.html">un convertisseur d'ethers en sous-unités</a> (EN).</em>

On peut comparer la limite en gaz à un une limite de litres de carburant pour une voiture. On peut comparer le prix du gaz au coût d'un litre de carburant.

Avec une voiture, il faut compter 1,5 € (prix) par litre (unité). Avec Ethereum, c'est 20 GWEI (prix) par gaz (unité). Pour remplir le "réservoir", il faut…
<ul>
 	<li>10 litres à 1,5 € = $15</li>
 	<li>21000 unités de gaz à 20 GWEI = 0.00042 ETH.</li>
</ul>
En conséquence, le coût total de la transaction sera de 0.00042 Ether.

Envoyer des tokens coûtera approximativement ~50000 à ~100000, donc le coût total de la transaction augmente de à 0.001 ETH - 0.002 ETH.
<h1><strong>Qu'est-ce que la “limite en gaz par bloc” ?</strong></h1>
La limite en gaz par bloc est le montant maximum de gaz accepté dans un bloc, pour déterminer combien de transactions peuvent entrer dans un bloc. Par exemple, disons que nous avons 5 transactions et les transactions ont une limite en gaz de 10, 20, 30, 40, et 50. Si la limite en gaz du bloc est de 100, alors les quatre premières transactions peuvent être contenues dans le bloc. Les mineurs décident quelles transactions ils incluent dans un bloc. Un mineur différent pourrait essayer d'inclure les deux dernières transactions dans le bloc (50+40), dans ce cas il ne resterait de la place que pour la première transaction (10). Si vous essayez d'inclure une transaction qui utilise plus de gaz que la limite actuelle de gaz par bloc, elle sera rejetée par le réseau, et votre client Ethereum vous enverra le message "Transaction exceeds block gas limit" (la transaction dépasse la limite en gaz par bloc). <a href="https://ethereum.stackexchange.com/questions/7359/are-gas-limit-in-transaction-and-block-gas-limit-different">Cet exemple provient d'un post sur l'Ethereum Slack Exchange par “ethers”</a> (EN).

La limite en gaz par bloc est de <a href="https://ethstats.net/">4 712 357 gaz au moment de la rédaction de cet article, selon les statistiques fournies par ethstats.net</a> (EN), ce qui signifie qu'environ 224 transactions qui ont chacune un <em>gas limit</em> de 21000 peuvent être contenues dans un bloc (qui est produit toutes les 15-20 secondes en moyenne). <a href="https://www.reddit.com/r/ethereum/comments/6g6tww/there_are_hundreds_or_even_thousands_of_pending/dinzrgq/">Le protocole permets au mineur d'un bloc d'ajuster la limite de gaz des blocs par un facteur de 1/1024 (0,0976 %) dans la direction qu'il souhaite (augmenter ou diminuer)</a> (EN).
<h2><strong>Qui décide de la limite en gaz par bloc ?</strong></h2>
Les mineurs du réseau décident ce qu'est la limite en gaz par bloc. En plus de cette limite en gaz par bloc ajustable par le protocole, une stratégie de minage <a href="https://github.com/search?q=org%3Aethereum+4712388&amp;type=Code">d'une limite par défaut de 4 712 388 est prévue par la plupart des clients</a> (EN). Les mineurs peuvent choisir de changer cette limite, mais la plupart ne le font pas et laissent le montant par défaut.
<h2><strong>Comment la limite en gaz par bloc est-elle changée ?</strong></h2>
Les mineurs sur Ethereum utilisent un programme de minage, comme <a href="https://github.com/ethereum-mining/ethminer">ethminer</a>, qui est lui-même connecté à un noeud <a href="https://geth.ethereum.org/">geth</a> ou <a href="https://parity.io/">Parity</a>. geth and Parity ont des options que les mineurs peuvent changer. Les options de <a href="https://github.com/ethereum/go-ethereum/wiki/Command-Line-Options">geth pour le minage sont détaillées ici</a> et <a href="https://github.com/paritytech/parity/wiki/Configuring-Parity#cli-options">les options de Parity ici</a>.
<h1><strong>Qu'est-ce qu'un “DoS” du réseau Ethereum ?</strong></h1>
Récemment, il y a eu beaucoup de discussions sur le fait que le réseau Ethereum était ralenti, devenait congestionnée voire inutilisable. Ces commentaires décrivent ces ralentissements comme "DoS" du réseau Ethereum. Un incident "DoS" ou déni de service sur le réseau Ethereum apparaît lorsque les blocs sont tous remplis et qu'il y a beaucoup de transactions en attente sur le réseau. Rappelez-vous que les mineurs peuvent choisir d'inclure les transactions sur la base du prix du gaz choisi. S'il y a des centaines de milliers de transactions en attente (on dit techniquement le "pool" de transactions), cela peut créer des retards inhabituels dans les transactions se chiffrant en heures. Les dénis de service peuvent être malintentionnés ou non.
<h2><strong>DoS malintentionnés</strong></h2>
En automne dernier, Ethereum a été attaqué par une personne ou un groupe de personnes dans ce qui fut appelé une attaque par spam. Cette attaque a été décrite <a href="https://www.ethereum-france.com/hard-fork-eip-150-mise-a-jour-de-recalibrage-et-carnet-de-voyage/">ici</a> (FR).

L’attaque DoS a consisté à inonder le réseau de transactions en faisant appel à diverses opérations dont le coût d’exécution ne correspondait pas à la charge réelle de traitement pour les nœuds du réseau.

Pendant cette attaque, il a été demandé aux mineurs de baisser la <a href="https://blog.ethereum.org/2016/09/22/transaction-spam-attack-next-steps/">limite de gaz des blocs à 1,5 million</a> (EN) puis à <a href="https://www.reddit.com/r/ethereum/comments/58aelh/attention_miners_recommending_miners_lower_the/">2 million à une autre occasion</a> (EN). Cette demande aux mineurs de baisser la limite de gaz par bloc pendant des attaques effectuées sur le réseau a été formulée à quelques autres reprises.
<h2><strong>DoS non-malintentionnés</strong></h2>
Les incidents de DoS non-malintentionnés sont simplement des événements au cours duquel le réseau a tellement de transactions en attente en même temps que cela prend un temps inhabituellement long pour les traiter. Récemment, la popularité et la prolifération des événements de distribution de tokens (appelés initial coin offerings (ICOs) ou token sales) ont provoqué une saturation du réseau avec des transactions. L'équipe d'INFURA a écrit <a href="https://blog.infura.io/when-there-are-too-many-pending-transactions-8ec1a88bc87e">un post de blog décrivant les détails techniques de ces événements</a> (EN).
<h2><strong>Pourquoi la limite en gaz des blocs ne change pas même lorsque les blocs sont pleins ?</strong></h2>
<strong>Raison principale : Les mineurs n'utilisent pas la fonction d'adaptation dynamique de la limite de gaz.</strong>

Le protocole Ethereum contient un mécanisme selon lequel les mineurs peuvent voter sur la limite en gaz des blocs, qui permets que la capacité augmente sans qu'il soit nécessaire de réaliser un hard fork. A l'origine, ce mécanisme était couplé avec une stratégie par défaut selon laquelle les mineurs votaient sur une limite en gaz au moins égale à 4.7 millions, mais qui aurait pour objectif 150 % du gaz moyen utilisé (calculé sur un intervalle moyen exponentiel de 1024 blocs) si ce montant est supérieur, ce qui permettait à la capacité d'augmenter organiquement avec la demande en incluant tout de même un plafond pour des raisons de lutte contre le spam.

Comme décrit dans la section “DoS malicieux” ci-dessus, il a été demandé de nombreuses fois aux mineurs de changer ce comportement par défaut pour lutter contre des attaques par spam. Le problème est que certaines pools de minage n'ont jamais remis le paramètre par défaut même après que les attaques aient cessé. Il y a à peu près un mois, il a été demandé aux mineurs <a href="https://www.reddit.com/r/ethereum/comments/6ehp60/recommendations_to_miners_to_change_gas_limit_and/">de changer la limite en gaz des blocs et le prix du gaz pour réintroduire cette fonction de limite en gaz évoluant organiquement</a> (EN) car les ventes de token récentes ont rapidement rempli les blocs et ont provoqué des congestions importantes sur la blockchain.

<a href="http://ethgasstation.info/index.php">ETH Gas Station</a> (EN) est une excellente ressource si vous recherchez des informations à jour sur <a href="http://ethgasstation.info/minerVotes.php">quelle limite en gaz par bloc les pools de minage votent</a> (EN).
<h3><strong>Qu'est-ce que les mineurs doivent faire pour régler ce problème ?</strong></h3>
Les mineurs peuvent modifier le paramétrage de leur noeud geth ou Parity pour réactiver les limites en gaz adaptive. Note : Les valeurs ci-dessous proviennent de ce <a href="https://www.reddit.com/r/ethereum/comments/6ehp60/recommendations_to_miners_to_change_gas_limit_and/">post Reddit</a> (EN) et peuvent en réalité être choisies beaucoup plus haut, comme il l'est expliqué dans cet autre <a href="https://www.reddit.com/r/ethereum/comments/6jn6lr/miners_increase_the_capacity_of_the_ethereum/">post Reddit</a> (EN).
<h4><strong>Geth</strong></h4>
<strong>Paramètre suggéré</strong>

<code>--gasprice 4000000000 --targetgaslimit 4712388</code>

<strong>Explication</strong>

<code>--targetgaslimit</code> fixe l'objectif de limite en gaz pour les blocs à miner (par défaut est : “4712388”)

<code>--gasprice</code> est le prix en gaz minimal pour accepter de miner une transaction (par défaut : “20000000000”). Note: gasprice est défini en <a href="https://www.myetherwallet.com/helpers.html">wei</a>.
<h4><strong>Parity</strong></h4>
<strong>Paramètre suggéré</strong>

<code>--gas-floor-target 4712388 --gas-cap 9000000 --gasprice 4000000000</code>

<strong>Explication</strong>

<code>--gas-floor-target</code> Montant de gaz par bloc à viser lors de la finalisation d'un bloc (par défaut : 4700000).

<code>--gas-cap</code> Une limite d'augmentation de limite en gaz par bloc en lien avec le volume de transaction (par défaut : 6283184).

<code>--gasprice</code> est le prix en gaz minimal pour accepter de miner une transaction .

Note: <code>gasprice</code> est défini en <a href="https://www.myetherwallet.com/helpers.html">wei</a>.

Note 2: <code>--gasprice</code> est une “option obligatoire”
<h4><strong>Autres options de minage</strong></h4>
Ces options sont disponibles sur les pages suivantes pour <a href="https://github.com/ethereum/go-ethereum/wiki/Command-Line-Options">geth</a> et <a href="https://github.com/paritytech/parity/wiki/Configuring-Parity#cli-options">Parity</a>.
<h1><strong>Autres ressources et documentation sur le sujet (EN)</strong></h1>
<ul>
 	<li><a href="http://ethgasstation.info/">Eth Gas Station website with Ethereum gas and miner stats.</a></li>
 	<li><a href="https://ethereum.stackexchange.com/">Ethereum StackExchange for technical questions of all kinds.</a></li>
 	<li><a href="http://ethdocs.org/en/latest/">EthDocs Ethereum Documentation (Much of it is outdated, but still good).</a></li>
 	<li><a href="https://media.consensys.net/ethereum-gas-fuel-and-fees-3333e17fe1dc">“Ethereum Gas, Fuel and Fees” by Joseph Chow.</a></li>
 	<li><a href="https://myetherwallet.groovehq.com/knowledge_base/topics/what-is-gas">“What is Gas?” by MyEtherWallet</a>.</li>
 	<li><a href="https://www.myetherwallet.com/helpers.html">MyEtherWallet Ether unit conversion tool.</a></li>
 	<li><a href="https://blog.infura.io/when-there-are-too-many-pending-transactions-8ec1a88bc87e">“When there are too many pending transactions” by Infura.</a></li>
</ul>