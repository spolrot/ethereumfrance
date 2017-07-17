---
ID: 2379
post_title: >
  La sécurité des smart contracts
  Ethereum
author: vincentlg
post_excerpt: ""
layout: post
permalink: >
  https://www.ethereum-france.com/la-securite-des-smart-contracts-ethereum/
published: true
post_date: 2017-06-07 08:02:26
---
<p style="text-align: left"><span style="font-size: 12pt"><em>Traduction de <a class="markup--anchor markup--p-anchor" href="https://medium.com/zeppelin-blog/onward-with-ethereum-smart-contract-security-97a827e47702" target="_blank" rel="noopener noreferrer">Onward with Ethereum Smart Contract Security</a>&nbsp;de&nbsp;<a class="markup--user markup--p-user" href="https://medium.com/@maraoz" target="_blank" rel="noopener noreferrer">Manuel Aráoz</a>&nbsp;par <a href="https://medium.com/@vincentlg">Vincent Le Gallic</a></em></span></p>
<p style="text-align: left"><span style="font-size: 12pt"><em class="markup--em markup--p-em">Si vous débutez en développement sur Ethereum, je vous recommande </em><a class="markup--anchor markup--p-anchor" href="https://medium.com/zeppelin-blog/the-hitchhikers-guide-to-smart-contracts-in-ethereum-848f08001f05#.6dob381ks" target="_blank" rel="noopener noreferrer"><em class="markup--em markup--p-em">cette introduction aux Smart Contracts avec Ethereum</em></a><em class="markup--em markup--p-em"> avant de commencer.</em></span></p>
<p id="af3b" class="graf graf--p graf-after--p">Monter en compétence sur la sécurité des smart contracts n’est pas une chose facile. il existe quelques bons guides comme par exemple “<a class="markup--anchor markup--p-anchor" href="https://github.com/ConsenSys/smart-contract-best-practices" target="_blank" rel="nofollow noopener noreferrer">Consensys’ Smart Contracts Best Practices</a>” ou “<a class="markup--anchor markup--p-anchor" href="http://solidity.readthedocs.io/en/latest/security-considerations.html" target="_blank" rel="nofollow noopener noreferrer">the Solidity Documentation Security Considerations</a>” mais ces concepts restent très difficiles à appréhender sans écrire soi même du code.</p>
<p id="cfce" class="graf graf--p graf-after--p">Je vais donc tenter une approche légèrement différente. Je vais expliquer certaines recommandations qui améliorent la sécurité des Smart Contract. Je montrerai des extraits de codes qui ne suivent pas ces recommandations pour mettre en avant les failles. Je vais également vous donner des exemples de code que vous pouvez utiliser pour rendre vos Smart Contracts plus fiables en espérant que cela déclenche de bons réflexes lorsque vous coderez vos smart contracts “réels”.</p>
<p id="67e8" class="graf graf--p graf-after--p">Sans plus tarder, découvrons les bonnes pratiques:</p>

<h3 id="da88" class="graf graf--h3 graf-after--p">Échouez dès que possible et échouez franchement</h3>
<em class="markup--em markup--p-em">Fail as early and loudly as possible</em>

Un moyen simple et efficace d’améliorer vos programmes est de suivre la règle du “<a class="markup--anchor markup--p-anchor" href="https://oncodingstyle.blogspot.fr/2008/10/fail-early-fail-loudly.html" target="_blank" rel="nofollow noopener noreferrer">Fail Early, Fail Loudly</a>”. Voici un exemple de code qui ne “Fail” pas de façon assez évidente.
<pre id="9c16" class="graf graf--pre graf-after--p">// UNSAFE CODE, DO NOT USE!</pre>
<pre id="0fe6" class="graf graf--pre graf-after--pre"><strong class="markup--strong markup--pre-strong">contract</strong> BadFailEarly {
  <strong class="markup--strong markup--pre-strong">uint</strong> <strong class="markup--strong markup--pre-strong">constant</strong> DEFAULT_SALARY = 50000;
  <strong class="markup--strong markup--pre-strong">mapping(string =&gt; uint)</strong> nameToSalary;</pre>
<pre id="c5a4" class="graf graf--pre graf-after--pre"><strong class="markup--strong markup--pre-strong">function</strong> getSalary(string name) constant returns (uint) {
    if (bytes(name).length != 0 &amp;&amp; nameToSalary[name] != 0) {
      <strong class="markup--strong markup--pre-strong">return</strong> nameToSalary[name];
    } else {
      <strong class="markup--strong markup--pre-strong">return</strong> DEFAULT_SALARY;
    }
  }
}</pre>
Nous voulons éviter qu’un contrat échoue silencieusement ou qu’il continue à être exécuté dans un état instable ou incohérent. La fonction getSalary vérifie les conditions avant de retourner le salaire stocké, ce qui est une bonne chose. Le problème c’est que dans le cas où ces conditions ne sont pas remplies, une valeur par défaut est renvoyée. Cela pourrait cacher une erreur de l’appelant. Il s’agit d’un cas extrême, mais ce genre de code est très fréquent et s’explique par la crainte de déclencher des erreurs qui stoppent notre application. En réalité, plus tôt nous échouerons, plus il sera facile de trouver le problème. Si nous cachons des erreurs, elles peuvent se propager vers d’autres parties du code et provoquer des incohérences difficiles à tracer. Une meilleure approche serait:

<section class="section section--body section--first">
<div class="section-content">
<div class="section-inner sectionLayout--insetColumn">
<pre id="f4a8" class="graf graf--pre graf-after--p"><strong class="markup--strong markup--pre-strong">contract</strong> GoodFailEarly {
  <strong class="markup--strong markup--pre-strong">mapping(string =&gt; uint)</strong> nameToSalary;
  
  <strong class="markup--strong markup--pre-strong">function</strong> getSalary(string name) constant returns (uint) {
    if (bytes(name).length == 0) <strong class="markup--strong markup--pre-strong">throw</strong>;    
    if (nameToSalary[name] == 0) <strong class="markup--strong markup--pre-strong">throw</strong>;
    
    <strong class="markup--strong markup--pre-strong">return</strong> nameToSalary[name];
  }
}</pre>
<p id="4cfa" class="graf graf--p graf-after--pre">Cette version montre une autre manière de programmer plus adaptée qui sépare les conditions préalables et déclenche des exceptions séparément. Notez que certaines de ces vérifications (en particulier celles qui dépendent d’un état interne) peuvent être implémentées avec des <a class="markup--anchor markup--p-anchor" href="http://solidity.readthedocs.io/en/latest/contracts.html#function-modifiers" target="_blank" rel="nofollow noopener noreferrer">Fonctions “Modifiers</a>”.</p>

<h3 id="8e17" class="graf graf--h3 graf-after--p">Préférez les “pull paiements” au “push paiements”</h3>
<p id="6cdf" class="graf graf--p graf-after--h3">Chaque transfert d’ether implique une exécution potentielle de code. L’adresse de réception peut implémenter une “Fallback” fonction qui peut lancer une erreur. Ainsi, nous ne devrions jamais considérer qu’un appel à send s’exécute sans erreur. Une solution: nos contrats devraient favoriser les “<a class="markup--anchor markup--p-anchor" href="https://github.com/ethereum/wiki/wiki/Safety#favor-pull-over-push-for-external-calls" target="_blank" rel="nofollow noopener noreferrer">pull paiements</a>”. Regardez ce code naïf d’enchère:</p>

<pre id="8656" class="graf graf--pre graf-after--p">// UNSAFE CODE, DO NOT USE!</pre>
<pre id="77de" class="graf graf--pre graf-after--pre"><strong class="markup--strong markup--pre-strong">contract</strong> BadPushPayments {
  <strong class="markup--strong markup--pre-strong">address</strong> highestBidder;
  <strong class="markup--strong markup--pre-strong">uint</strong> highestBid;
 
  <strong class="markup--strong markup--pre-strong">function</strong> bid() {
    if (msg.value &lt; highestBid) <strong class="markup--strong markup--pre-strong">throw</strong>;
    if (highestBidder != 0) {
      // return bid to previous winner
      if (!highestBidder.send(highestBid)) {
        throw;
      }
    }
    highestBidder = msg.sender;
    highestBid = msg.value;
  }
}</pre>
<p id="b5c7" class="graf graf--p graf-after--pre">Notez que le contrat appelle la fonction send et vérifie la valeur de retour, ce qui semble correcte. Mais l’appel à send au milieu d’une fonction n’est pas sécurisé. Pourquoi? Rappelez-vous que, comme indiqué ci-dessus, send peut déclencher l’exécution de code dans un autre contrat.</p>
<p id="1311" class="graf graf--p graf-after--p">Imaginez que quelqu’un enchérisse avec une adresse qui déclenche une erreur à chaque fois que quelqu’un envoie de l’argent dessus. Que se passe-t-il lorsque quelqu’un d’autre tente d’enchérir? L’appel de send échouera toujours et remontera jusqu’à la function bid qui échouera à son tour. Un appel de fonction qui se termine par une erreur laisse l’état inchangé (toutes les modifications apportées sont annulées). Cela signifie que personne d’autre ne peut enchérir, le contrat est rompu.</p>
<p id="608b" class="graf graf--p graf-after--p">La solution la plus simple consiste à séparer les paiements dans une fonction différente qui permettra aux utilisateurs de demander (pull) des fonds indépendamment du reste de la logique du contrat:</p>

<pre id="859f" class="graf graf--pre graf-after--p"><strong class="markup--strong markup--pre-strong">contract</strong> GoodPullPayments {
  <strong class="markup--strong markup--pre-strong">address</strong> highestBidder;
  <strong class="markup--strong markup--pre-strong">uint</strong> highestBid;
  <strong class="markup--strong markup--pre-strong">mapping(address =&gt; uint)</strong> refunds;
  
  <strong class="markup--strong markup--pre-strong">function</strong> bid() <strong class="markup--strong markup--pre-strong">external</strong> {
    if (msg.value &lt; highestBid) <strong class="markup--strong markup--pre-strong">throw</strong>;
    
    if (highestBidder != 0) {
      refunds[highestBidder] += highestBid;
    }
    
    highestBidder = msg.sender;
    highestBid = msg.value;
  }
  
  <strong class="markup--strong markup--pre-strong">function</strong> withdrawBid() <strong class="markup--strong markup--pre-strong">external</strong> {
    uint refund = refunds[msg.sender];
    refunds[msg.sender] = 0;
    if (!msg.sender.send(refund)) {
      refunds[msg.sender] = refund;
    }
  }
}</pre>
<p id="7dbf" class="graf graf--p graf-after--pre">Cette fois, nous utilisons un mapping pour stocker les valeurs de remboursement pour les enchères dépassées et nous ajoutons une fonction permettant aux enchérisseurs de retirer leurs fonds.</p>
<p id="3f1e" class="graf graf--p graf-after--p">En cas de problème dans l’appel de send, seul l’enchérisseur appelant est affecté. Il s’agit d’un modèle simple qui résout beaucoup d’autres problèmes (Notamment la <a class="markup--anchor markup--p-anchor" href="http://hackingdistributed.com/2016/07/13/reentrancy-woes/" target="_blank" rel="nofollow noopener noreferrer">faille de réentrance</a>), alors n’oubliez pas: lors de l’envoi d’ether, favorisez les “pull” au “push” paiements.</p>
<p id="755b" class="graf graf--p graf-after--p">J’ai mis en place <a class="markup--anchor markup--p-anchor" href="https://github.com/OpenZeppelin/zeppelin-solidity/blob/master/contracts/payment/PullPayment.sol" target="_blank" rel="nofollow noopener noreferrer">un contrat</a> dont vous pouvez hériter pour utiliser facilement ce pattern.</p>

<h3 id="808b" class="graf graf--h3 graf-after--p">Organisez le code de vos fonctions: Conditions, actions, interactions</h3>
<p id="b72f" class="graf graf--p graf-after--h3">En complément du principe “Échouez dès que possible”, une bonne pratique consiste à structurer toutes vos fonctions comme suit: d’abord, vérifiez toutes les conditions préalables; ensuite, modifiez l’état de votre contrat; et enfin, interagissez avec d’autres contrats.</p>
<p id="c68a" class="graf graf--p graf-after--p">Conditions, actions, interactions. S’en tenir à cette structure de fonctions vous évitera beaucoup de problèmes. Voyons <a class="markup--anchor markup--p-anchor" href="http://solidity.readthedocs.io/en/latest/solidity-by-example.html" target="_blank" rel="nofollow noopener noreferrer">un exemple</a> d’une fonction utilisant ce pattern:</p>

<pre id="1d5c" class="graf graf--pre graf-after--p"><strong class="markup--strong markup--pre-strong">function</strong> auctionEnd() {
  <strong class="markup--strong markup--pre-strong"><em class="markup--em markup--pre-em">// 1. Conditions</em></strong>
  if (now &lt;= auctionStart + biddingTime)
    throw; <em class="markup--em markup--pre-em">// auction did not yet end</em>
  if (ended)
    throw; <em class="markup--em markup--pre-em">// this function has already been called</em>

  <strong class="markup--strong markup--pre-strong"><em class="markup--em markup--pre-em">// 2. Effects</em></strong>
  ended = true<strong class="markup--strong markup--pre-strong">;</strong>
  AuctionEnded(highestBidder, highestBid);

  <strong class="markup--strong markup--pre-strong"><em class="markup--em markup--pre-em">// 3. Interaction</em></strong>
  if (!beneficiary.send(highestBid))
    throw;
  }
}</pre>
<p id="77bc" class="graf graf--p graf-after--pre">Ce code est conforme au principe d’échouer vite&nbsp;, car les conditions sont vérifiées au début et les interactions potentiellement dangereuses avec d’autres contrats sont placées en dernière position.</p>

<h3 id="1f79" class="graf graf--h3 graf-after--p">Tenez compte des limites de la plateforme</h3>
<p id="6254" class="graf graf--p graf-after--h3">L’<a class="markup--anchor markup--p-anchor" href="http://solidity.readthedocs.io/en/latest/introduction-to-smart-contracts.html#index-6" target="_blank" rel="nofollow noopener noreferrer">EVM</a> a beaucoup de limites strictes sur ce que nos contrats peuvent faire. Ce sont des considérations de sécurité au niveau de la plateforme, mais elles peuvent menacer la sécurité de votre contrat si vous les ignorez. Jetons un coup d’oeil à ce code naïf de gestion des bonus des employés.</p>

<pre id="0eb3" class="graf graf--pre graf-after--p">// UNSAFE CODE, DO NOT USE!</pre>
<pre id="de85" class="graf graf--pre graf-after--pre"><strong class="markup--strong markup--pre-strong">contract</strong> BadArrayUse {
  
  <strong class="markup--strong markup--pre-strong">address</strong>[] employees;
  
  <strong class="markup--strong markup--pre-strong">function</strong> payBonus() {
    for (var i = 0; i &lt; employees.length; i++) {
      address employee = employees[i];
      uint bonus = calculateBonus(employee);
      employee.send(bonus);
    }     
  }
  
  <strong class="markup--strong markup--pre-strong">function</strong> calculateBonus(address employee) returns (uint) {
    // some expensive computation ...
  }
}</pre>
<p id="d888" class="graf graf--p graf-after--pre">Lisez ce code: c’est assez simple et ça semble correct… Ce code cache pourtant 3 problèmes potentiels liés aux limites de la plateforme.</p>
<p id="25b4" class="graf graf--p graf-after--p">Le premier problème est le type de i, uint8 sera appliqué car c’est le plus petit type qui supporte la valeur 0. Si le tableau a plus de 255 éléments, la boucle ne se terminera pas, ce qui entraînera une épuisement du <em class="markup--em markup--p-em">gas</em>. Utiliser le type uint explicitement est plus judicieux car cela évitera les surprises et augmentera la limite. Evitez de déclarer les variables en utilisant <em class="markup--em markup--p-em">var</em> quand cela est possible. Maintenant, réparons ça:</p>

<pre id="fee3" class="graf graf--pre graf-after--p">// STILL UNSAFE CODE, DO NOT USE!</pre>
<pre id="49f2" class="graf graf--pre graf-after--pre"><strong class="markup--strong markup--pre-strong">contract</strong> BadArrayUse {
  
  <strong class="markup--strong markup--pre-strong">address</strong>[] employees;
  
  <strong class="markup--strong markup--pre-strong">function</strong> payBonus() {
    for (<strong class="markup--strong markup--pre-strong">uint</strong> i = 0; i &lt; employees.length; i++) {
      address employee = employees[i];
      uint bonus = calculateBonus(employee);
      employee.send(bonus);
    }     
  }
  
  <strong class="markup--strong markup--pre-strong">function</strong> calculateBonus(address employee) returns (uint) {
    // some expensive computation ...
  }
}</pre>
<p id="3a7d" class="graf graf--p graf-after--pre">La deuxième aspect que vous devez considérer est la limite de <em class="markup--em markup--p-em">gas</em>. Le <em class="markup--em markup--p-em">gas</em> est le mécanisme d’Ethereum pour payer les ressources du réseau. Chaque appel de fonction qui modifie l’état a un coût en <em class="markup--em markup--p-em">gas</em>. Imaginez que CalculBonus détermine le bonus pour chaque employé en fonction d’un calcul complexe, comme le calcul du profit sur de nombreux projets par exemple. Cela dépenserait beaucoup de <em class="markup--em markup--p-em">gas</em>, ce qui pourrait facilement atteindre la limite de <em class="markup--em markup--p-em">gas</em> de la transaction ou du bloc. Si une transaction atteint la limite de <em class="markup--em markup--p-em">gas</em>, toutes les modifications sont annulées, mais les frais eux restent à payer. Tenez compte des coûts variables de <em class="markup--em markup--p-em">gas</em> lors de l’utilisation de boucles.</p>
<p id="4249" class="graf graf--p graf-after--p">Optimisons le contrat en séparant le calcul du bonus de la boucle for. Notez que cela ne résout pas le problème: à mesure que le nombre de salariés augmente, le coût du gas augmente.</p>

<pre id="f8e1" class="graf graf--pre graf-after--p">// UNSAFE CODE, DO NOT USE!</pre>
<pre id="5628" class="graf graf--pre graf-after--pre"><strong class="markup--strong markup--pre-strong">contract</strong> BadArrayUse {
  
  <strong class="markup--strong markup--pre-strong">address</strong>[] employees;
  <strong class="markup--strong markup--pre-strong">mapping(address =&gt; uint)</strong> bonuses;  
  
  <strong class="markup--strong markup--pre-strong">function</strong> payBonus() {
    for (uint i = 0; i &lt; employees.length; i++) {
      address employee = employees[i];
      uint bonus = <strong class="markup--strong markup--pre-strong">bonuses[employee];</strong>
      employee.send(bonus);
    }     
  }
  
  <strong class="markup--strong markup--pre-strong">function</strong> calculateBonus(address employee) returns (uint) {
    uint bonus = 0;
    // some expensive computation modifying the bonus...
    <strong class="markup--strong markup--pre-strong">bonuses[employee] = bonus;</strong>
  }
}</pre>
<p id="b453" class="graf graf--p graf-after--pre">Enfin, la profondeur de la pile d’appels est limitée. La pile d’appels de l’EVM a une limite stricte de 1024. Cela signifie que si le nombre d’appels récursifs atteint 1024, le contrat échoue. Un attaquant peut appeler un contrat récursivement 1023 fois puis appeler une fonction de notre contrat, cela provoquera une erreur silencieuse en raison de cette limite. PullPaymentCapable.sol présenté plus haut permet d’implémenter facilement des “pull paiements”. Hériter de PullPaymentCapable et utiliser asyncSend vous protègent.</p>
<p id="b98a" class="graf graf--p graf-after--p">Voici une version modifiée du code qui corrige tous ces problèmes:</p>

<pre id="c31a" class="graf graf--pre graf-after--p"><strong class="markup--strong markup--pre-strong">import</strong> './PullPaymentCapable.sol';</pre>
<pre id="cfb4" class="graf graf--pre graf-after--pre"><strong class="markup--strong markup--pre-strong">contract</strong> GoodArrayUse is PullPaymentCapable {
  address[] employees;
  mapping(address =&gt; uint) bonuses;
  
  <strong class="markup--strong markup--pre-strong">function</strong> payBonus() {
    for (uint i = 0; i &lt; employees.length; i++) {
      address employee = employees[i];
      uint bonus = bonuses[employee];
      <strong class="markup--strong markup--pre-strong">asyncSend(employee, bonus);</strong>
    }
  }</pre>
<pre id="400e" class="graf graf--pre graf-after--pre"><strong class="markup--strong markup--pre-strong">function</strong> calculateBonus(address employee) returns (uint) {
    uint bonus = 0;
    // some expensive computation...
    bonuses[employee] = bonus;
  }
}</pre>
<p id="3785" class="graf graf--p graf-after--pre">En résumé, tenez compte (1) des limites dans les types de variables que vous utilisez, (2) des limites de coûts de gas de votre contrat et (3) de la limite de profondeur de la pile d’appels (stack depth limit).</p>

<h3 id="aa13" class="graf graf--h3 graf-after--p">Écrivez des&nbsp;tests</h3>
<p id="23fa" class="graf graf--p graf-after--h3">Ecrire des tests représente beaucoup de travail, mais cela vous évitera des problèmes de régression. Un bug de régression apparaît lorsqu’un composant stable devient instable à cause d’une modification récente. J’écrirai prochainement un guide sur ce sujet, mais si vous êtes intéressés, consultez le “<a class="markup--anchor markup--p-anchor" href="http://truffleframework.com/docs/getting_started/testing" target="_blank" rel="nofollow noopener noreferrer">Truffle’s testing guide</a>”.</p>

<h3 id="9872" class="graf graf--h3 graf-after--p">Tolérance aux pannes et bug bounties automatiques</h3>
<p id="4558" class="graf graf--p graf-after--h3"><em class="markup--em markup--p-em">(Un bug bounty est un programme qui permet à des personnes de recevoir une compensation après avoir reporté des bugs ou des vulnérabilités)</em></p>
<p id="9f55" class="graf graf--p graf-after--p">Merci à <a class="markup--anchor markup--p-anchor" href="https://medium.com/@peterborah/we-need-fault-tolerant-smart-contracts-ec1b56596dbc" target="_blank" rel="noopener noreferrer">Peter Borah pour l’inspiration de ces deux idées</a>. Les relectures de code et les audits de sécurité ne suffisent pas rendre les <em class="markup--em markup--p-em">smart contracts</em> infaillibles. Notre code doit être paré au pire. Dans le cas d’une vulnérabilité dans notre Smart contract, il devrait y avoir un moyen sûr de le réparer. En plus de cela, nous devrions essayer de découvrir ces vulnérabilités le plus tôt possible. C’est là que les <em class="markup--em markup--p-em">bug bounties</em> automatiquement intégrés dans notre contrat peuvent aider.</p>
<p id="3eff" class="graf graf--p graf-after--p">Examinons une implémentation de bug bounty automatique dans un exemple (simplifié) de contrat Token</p>

<pre id="59f2" class="graf graf--pre graf-after--p"><strong class="markup--strong markup--pre-strong">import</strong> './PullPaymentCapable.sol';
<strong class="markup--strong markup--pre-strong">import</strong> './Token.sol';</pre>
<pre id="513f" class="graf graf--pre graf-after--pre"><strong class="markup--strong markup--pre-strong">contract</strong> Bounty is PullPaymentCapable {
  <strong class="markup--strong markup--pre-strong">bool</strong> public claimed;
  <strong class="markup--strong markup--pre-strong">mapping(address =&gt; address)</strong> public researchers;
  
  <strong class="markup--strong markup--pre-strong">function</strong>() {
    if (claimed) <strong class="markup--strong markup--pre-strong">throw</strong>;
  }
  
  <strong class="markup--strong markup--pre-strong">function</strong> createTarget() <strong class="markup--strong markup--pre-strong">returns</strong>(Token) {
    Token target = new Token(0);
    researchers[target] = msg.sender;
    <strong class="markup--strong markup--pre-strong">return</strong> target;
  }
  
  <strong class="markup--strong markup--pre-strong">function</strong> claim(Token target) {
    address researcher = researchers[target];
    if (researcher == 0) <strong class="markup--strong markup--pre-strong">throw</strong>;
    
    // check Token contract invariants
    if (target.totalSupply() == target.balance) {
      <strong class="markup--strong markup--pre-strong">throw</strong>;
    }
    asyncSend(researcher, this.balance);
    claimed = true;
  }
}</pre>
<p id="b586" class="graf graf--p graf-after--pre">Comme précédemment, nous utilisons PullPaymentCapable pour sécuriser nos paiements sortants. Ce contrat Bounty permet aux chercheurs de créer des copies du contrat Token que nous souhaitons auditer. Tout le monde peut contribuer en envoyant des transactions à l’adresse du contrat Bounty. Si un chercheur parvient à corrompre sa copie du contrat Token, en faisant une faille immuable (par exemple en rendant le nombre de Token distribués différent de la balance), il obtiendra la totalité des compensations. Une fois la faille revendiquée, le contrat n’acceptera plus de fonds (cette fonction sans nom est appelée “fallback function”, elle est exécutée à chaque fois que de l’argent est envoyé directement au contrat).</p>
<p id="7ce2" class="graf graf--p graf-after--p">Comme vous pouvez le voir, il s’agit d’un contrat distinct et cela ne nécessite aucune modification de notre contrat Token d’origine. <a class="markup--anchor markup--p-anchor" href="https://github.com/OpenZeppelin/zeppelin-solidity/blob/master/contracts/Bounty.sol" target="_blank" rel="nofollow noopener noreferrer">Voici une implémentation complète disponible sur GitHub que tout le monde peut utiliser.</a></p>
<p id="12d4" class="graf graf--p graf-after--p">En ce qui concerne la tolérance aux pannes, nous allons devoir modifier notre contrat d’origine pour ajouter des mécanismes de sécurité supplémentaires. Une idée simple est de permettre au gardien d’un contrat de geler le contrat en cas d’urgence. Voyons une façon de mettre en œuvre ce comportement avec de l’héritage:</p>

<pre id="2556" class="graf graf--pre graf-after--p"><strong class="markup--strong markup--pre-strong">contract</strong> Stoppable {
  <strong class="markup--strong markup--pre-strong">address</strong> <strong class="markup--strong markup--pre-strong">public</strong> curator;
  <strong class="markup--strong markup--pre-strong">bool public </strong>stopped;</pre>
<pre id="5529" class="graf graf--pre graf-after--pre"><strong class="markup--strong markup--pre-strong">modifier</strong> stopInEmergency { if (!stopped) _ }
  <strong class="markup--strong markup--pre-strong">modifier</strong> onlyInEmergency { if (stopped) _ }
  
  <strong class="markup--strong markup--pre-strong">function</strong> Stoppable(address _curator) {
    if (_curator == 0) <strong class="markup--strong markup--pre-strong">throw</strong>;
    curator = _curator;
  }
  
  <strong class="markup--strong markup--pre-strong">function</strong> emergencyStop() external {
    if (msg.sender != curator) <strong class="markup--strong markup--pre-strong">throw</strong>;
    stopped = true;
  }
}</pre>
<p id="b151" class="graf graf--p graf-after--pre">Stoppable permet de spécifier l’adresse d’un gardien (curator) qui pourra arrêter le contrat. Que signifie «arrêter le contrat»? Cela doit être défini par le contrat enfant qui hérite de Stoppable en utilisant les fonctions modifiers stopInEmergency et onlyInEmergency. Voyons un exemple:</p>

<pre id="d11d" class="graf graf--pre graf-after--p"><strong class="markup--strong markup--pre-strong">import</strong> './PullPaymentCapable.sol';
<strong class="markup--strong markup--pre-strong">import</strong> './Stoppable.sol';</pre>
<pre id="98ec" class="graf graf--pre graf-after--pre"><strong class="markup--strong markup--pre-strong">contract</strong> StoppableBid is Stoppable, PullPaymentCapable {
  <strong class="markup--strong markup--pre-strong">address public</strong> highestBidder;
  <strong class="markup--strong markup--pre-strong">uint public</strong> highestBid;
  
  <strong class="markup--strong markup--pre-strong">function</strong> StoppableBid(address _curator)
    Stoppable(_curator)
    PullPaymentCapable() {}
  
  <strong class="markup--strong markup--pre-strong">function</strong> bid() external <strong class="markup--strong markup--pre-strong">stopInEmergency</strong> {
    if (msg.value &lt;= highestBid) <strong class="markup--strong markup--pre-strong">throw</strong>;
    
    if (highestBidder != 0) {
      asyncSend(highestBidder, highestBid);
    }
    highestBidder = msg.sender;
    highestBid = msg.value;
  }
  
  <strong class="markup--strong markup--pre-strong">function</strong> withdraw() <strong class="markup--strong markup--pre-strong">onlyInEmergency</strong> {
    suicide(curator);
  }
}</pre>
<p id="3d8b" class="graf graf--p graf-after--pre">Dans cet exemple d’enchères, le système peut maintenant être interrompu par un gardien (curator), défini lors de la création du contrat. Tant que StoppableBid est en mode normal, seule la fonction bid peut être appelée. Si quelque chose d’étrange se produit et que le contrat est dans un état incohérent, le gardien peut intervenir et activer l’état d’urgence (emergency mode). Cela désactive la fonction dib et permet à la fonction withdraw de fonctionner.</p>
<p id="3538" class="graf graf--p graf-after--p">Dans cet exemple, l’état d’urgence (emergency mode) ne permet qu’au conservateur de détruire le contrat et de récupérer les fonds, mais en réalité, la logique de récupération pourrait être plus complexe (par exemple, renvoyer des fonds à leurs propriétaires).</p>

<h3 id="b2a7" class="graf graf--h3 graf-after--p">Limitez le montant des fonds&nbsp;déposés</h3>
<p id="d12e" class="graf graf--p graf-after--h3">Une autre façon de protéger nos <em class="markup--em markup--p-em">smart contracts</em> contre les attaques est de limiter leur portée. Les attaquants vont probablement cibler des contrats importants qui gèrent des millions de dollars. Tous les smart contracts ne doivent pas avoir des enjeux aussi importants, surtout si nous effectuons des tests. Dans ce contexte, il pourrait être utile de limiter le montant des fonds que notre contrat accepte. C’est aussi simple qu’une limite en dur sur la balance (le solde) de l’adresse du contrat.</p>
<p id="d1a9" class="graf graf--p graf-after--p">Voici un exemple simplifié sur la façon de procéder:</p>

<pre id="d38c" class="graf graf--pre graf-after--p"><strong class="markup--strong markup--pre-strong">contract</strong> LimitFunds {
  
  <strong class="markup--strong markup--pre-strong">uint</strong> LIMIT = 5000;
  
  <strong class="markup--strong markup--pre-strong">function</strong>() { throw; }
  
  <strong class="markup--strong markup--pre-strong">function</strong> deposit() {
    if (this.balance &gt; LIMIT) throw;
    ...
  }
}</pre>
<p id="f925" class="graf graf--p graf-after--pre">La fallback function rejettera tout paiement direct au contrat. La fonction deposit vérifiera d’abord si la limite souhaitée n’est pas déjà dépassée avant d’autoriser un nouveau dépôt. Des choses plus intéressantes comme des limites dynamiques ou paramétrées sont faciles à mettre en œuvre.</p>

<h3 id="6243" class="graf graf--h3 graf-after--p">Ecrivez un code simple et modulaire</h3>
<p id="2da3" class="graf graf--p graf-after--h3">Un code est fiable (au sens sécurisé) lorsque correspondent notre intention et ce que notre code permet réellement de faire. C’est très difficile à vérifier, surtout si le code est énorme et désordonné. C’est pourquoi il est important d’écrire un code simple et modulaire.</p>
<p id="9fca" class="graf graf--p graf-after--p">Cela signifie que les fonctions devraient être aussi courtes que possible, les dépendances de code devraient être réduites au minimum, et les fichiers devraient être aussi courts que possible, séparant la logique indépendante en modules, chacun avec une seule responsabilité.</p>
<p id="5e76" class="graf graf--p graf-after--p">Le nommage est également l’un des meilleurs moyens d’exprimer notre intention lors de l’écriture du code. Réfléchissez bien aux noms que vous choisissez, afin de rendre votre code aussi clair que possible.</p>
<p id="b1d4" class="graf graf--p graf-after--p">Etudions un exemple de mauvais nommage <a class="markup--anchor markup--p-anchor" href="https://solidity.readthedocs.io/en/latest/contracts.html#events" target="_blank" rel="nofollow noopener noreferrer">d’événements</a>. Regardez cette fonction à partir de<a class="markup--anchor markup--p-anchor" href="https://github.com/slockit/DAO/blob/develop/DAO.sol#L618-L691" target="_blank" rel="nofollow noopener noreferrer"> The DAO</a>. Je ne vais pas copier le code de la fonction ici car il est très long.</p>
<p id="1ef4" class="graf graf--p graf-after--p">Le problème le plus important est que c’est trop long et trop complexe. Essayez de garder vos fonctions beaucoup plus courtes, disons 30 ou 40 lignes de code max. Idéalement, vous devriez pouvoir lire les fonctions et comprendre ce qu’elles font en moins d’une minute. Un autre problème est le mauvais nom pour l’événement Transfer. Le nom diffère d’une fonction appelée transfer par seulement 1 caractère! Cela apporte beaucoup de confusion. En général, le nommage recommandé pour les événements est de préfixer la variable par “Log”. Dans ce cas, un meilleur nom serait LogTransfer.</p>
<p id="3786" class="graf graf--p graf-after--p">N’oubliez pas, écrivez des contrats simples, modulaires et aussi bien nommés que possible. Cela facilitera grandement les autres et vous-même pour auditer votre code.</p>

<h3 id="45ab" class="graf graf--h3 graf-after--p">N’écrivez pas tout votre code à partir de&nbsp;zéro</h3>
<p id="c656" class="graf graf--p graf-after--h3">Enfin, comme le dit l’adage: “Don’t roll your own crypto”. Je pense que cela s’applique également au code des Smart Contracts. Vous manipulez de l’argent, votre code et vos données sont publics, et vous utilisez une plateforme récente et expérimentale. Les enjeux sont élevés et les occasions de tout gâcher sont partout.</p>
<p id="b9ba" class="graf graf--p graf-after--p">Ces pratiques aident à sécuriser nos <em class="markup--em markup--p-em">smart contracts</em>. Mais, finalement, nous devrions créer de meilleurs outils de développement pour construire des <em class="markup--em markup--p-em">smart contracts</em>. Il existe des initiatives intéressantes comme ce meilleur <a class="markup--anchor markup--p-anchor" href="https://www.youtube.com/watch?v=H2uwUdzVD9I&amp;feature=youtu.be" target="_blank" rel="nofollow noopener noreferrer">système de type</a>, <a class="markup--anchor markup--p-anchor" href="https://blog.ethereum.org/2015/12/24/understanding-serenity-part-i-abstraction/" target="_blank" rel="nofollow noopener noreferrer">Serenity Abstractions</a>, et <a class="markup--anchor markup--p-anchor" href="http://www.rsk.co/" target="_blank" rel="nofollow noopener noreferrer">the Rootstock platform</a>.</p>
<p id="6267" class="graf graf--p graf-after--p">Il y a beaucoup de code sûr et de qualité déjà écrit et les frameworks commencent à apparaître. Nous avons commencé à compiler certaines des meilleures pratiques dans<a class="markup--anchor markup--p-anchor" href="http://com/OpenZeppelin/zeppelin-solidity" target="_blank" rel="nofollow noopener noreferrer"> ce repo GitHub que nous avons appelé OpenZeppelin</a>. N’hésitez pas à regarder et à contribuer avec du nouveau code ou des audits de sécurité.</p>

<h3 id="e548" class="graf graf--h3 graf-after--p">Récapitulons&nbsp;!</h3>
<ol class="postList">
	<li id="00ee" class="graf graf--li graf-after--h3">Échouez dès que possible et échouez franchement.</li>
	<li id="768d" class="graf graf--li graf-after--li">Préférez les “pull paiements” au “push paiements”</li>
	<li id="4086" class="graf graf--li graf-after--li">Organisez le code de vos fonctions: Conditions, actions, interactions</li>
	<li id="6ed5" class="graf graf--li graf-after--li">Tenez compte des limites de la plate-forme</li>
	<li id="c911" class="graf graf--li graf-after--li">Écrivez des tests</li>
	<li id="504f" class="graf graf--li graf-after--li">Tolérance aux pannes et bug bounties automatiques</li>
	<li id="a605" class="graf graf--li graf-after--li">Limitez le montant des fonds déposés</li>
	<li id="109e" class="graf graf--li graf-after--li">Ecrivez un code simple et modulaire</li>
	<li id="6d66" class="graf graf--li graf-after--li">N’écrivez pas tout votre code à partir de zéro</li>
</ol>
<p id="99fc" class="graf graf--p graf-after--li">Si vous souhaitez vous joindre à la discussion à propos des patterns de sécurité des smart contract, <a class="markup--anchor markup--p-anchor" href="https://zeppelin-slackin.herokuapp.com/" target="_blank" rel="nofollow noopener noreferrer">rejoignez-nous sur Slack</a>. Améliorons ensemble les standards de développement des smart contracts&nbsp;!</p>
<p class="graf graf--p graf-after--li">Pour suivre le travail d’OpenZeppelin sur la sécurité des smart contracts, suivez-les sur <a class="markup--anchor markup--p-anchor" href="https://medium.com/zeppelin-blog" target="_blank" rel="noopener noreferrer">Medium</a> et <a class="markup--anchor markup--p-anchor" href="https://twitter.com/maraoz" target="_blank" rel="nofollow noopener noreferrer">Twitter</a>.</p>
<p class="graf graf--p graf-after--li"><em class="markup--em markup--p-em">Publié avec l’accord préalable de </em><a class="markup--user markup--p-user" href="https://medium.com/@maraoz" target="_blank" rel="noopener noreferrer"><em class="markup--em markup--p-em">Manuel Aráoz</em></a><em class="markup--em markup--p-em">. Merci </em><a class="markup--user markup--p-user" href="https://medium.com/@romemore" target="_blank" rel="noopener noreferrer"><em class="markup--em markup--p-em">Romain Menetrier</em></a><em class="markup--em markup--p-em"> pour la relecture.</em></p>

</div>
</div>
</section>