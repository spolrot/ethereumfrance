---
ID: 517
post_title: 'CUDA Miner 1.0.7 et bonus [MàJ]'
author: Okkoh
post_excerpt: ""
layout: post
permalink: >
  https://www.ethereum-france.com/cuda-miner-1-0-7-et-bonus/
published: true
post_date: 2016-04-19 09:56:51
---
L'excellent Genoil a publié une nouvelle version de son fork d'Ethermine, le logiciel de référence pour <a href="http://www.ethereum-france.com/comment-miner-de-lether-eth-sous-windows-version-complete/"><span style="text-decoration: underline">le minage d'ethers</span></a>. Nous en sommes donc à la version 1.0.7. Il y a maintenant une fonction de failover, ce qui signifie qu'il est maintenant possible en complément des arguments StratumProxy <code><span class="c6 c1">-S </span><span class="c1 c2 c18">URL_POOL</span><span class="c6 c1">:</span><span class="c1 c2 c18">PORT_POOL</span><span class="c7 c1"> </span><span class="c6 c1">-O</span><span class="c7 c1"> </span><span class="c1 c2 c18">VOTRE</span><span class="c1 c2 c18">_WALLET</span><span class="c6 c1">.</span><span class="c1 c2 c18">NOM_DU_WORKER</span></code> de mettre <code><span class="c6 c1">-FS </span><span class="c1 c2 c18">URL_POOL</span><span class="c6 c1">:</span><span class="c1 c2 c18">PORT_POOL</span><span class="c7 c1"> </span><span class="c6 c1">-FO</span><span class="c7 c1"> </span><span class="c1 c2 c18">VOTRE</span><span class="c1 c2 c18">_WALLET</span><span class="c6 c1">.</span></code><span class="c1 c2 c18"><code>NOM_DU_WORKER</code> pour spécifier un autre serveur de pool si jamais le premier est down. Il paraîtrait aussi que le hashrate est légèrement meilleur (sans garantie aucune).</span>

Dans la 1.0.8, Genoil souhaite travailler sur les points suivants :
<ul>
 	<li>implémenter un stratum work timeout (si aucun nouveau travail n'envoyé par le serveur dans les X secondes, reconnecter ou basculer sur un autre serveur)</li>
 	<li>rendre l'utilisation d'OpenCL avec CUDA aussi rapide qu'avec le CUDA natif</li>
 	<li>améliorer l'affichage de la console pour afficher plus d'informations pertinentes</li>
 	<li>corriger ce qui se passe lorsque le DAG switch crashe</li>
 	<li>améliorer le temps de démarrage (en attendant, si vous ne voulez pas attendre derrière votre PC, vous pouvez toujours utiliser mon batch qui redémarre périodiquement ethermine)</li>
</ul>
Le lien pour récupérer CUDA Miner :
<p style="text-align: center"><a href="https://github.com/Genoil/cpp-ethereum/tree/master/releases">https://github.com/Genoil/cpp-ethereum/tree/master/releases</a></p>
[Edit]: autre lien (contenant un help.txt):
<p style="text-align: center"><a href="http://cryptomining-blog.com/wp-content/download/ethminer-0.9.41-genoil-1.0.7.zip">http://cryptomining-blog.com/wp-content/download/ethminer-0.9.41-genoil-1.0.7.zip</a></p>
Le bonus, enfin, concerne les workers sous Windows 10 et travaillant avec des cartes Nvidia, puisque Genoil a mis en ligne la version 1.0.5 recompilée avec les CUDA 6.5. Cela permet d'utiliser l'argument -U avec les pilotes 347.52.
<p style="text-align: center"><a href="https://github.com/Genoil/cpp-ethereum/tree/master/releases/cuda-6.5">https://github.com/Genoil/cpp-ethereum/tree/master/releases/cuda-6.5</a></p>
[Edit]: une version CUDA 6.5 de la 1.0.7 a été également réalisée, elle est incluse dans la version 1.0.7 distribuée sur cryptomining-blog :
<p style="text-align: center"><a href="http://cryptomining-blog.com/wp-content/download/ethminer-0.9.41-genoil-1.0.7.zip">http://cryptomining-blog.com/wp-content/download/ethminer-0.9.41-genoil-1.0.7.zip</a></p>
&nbsp;

Pour remercier Genoil : 0xeb9310b185455f863f526dab3d245809f6854b4d