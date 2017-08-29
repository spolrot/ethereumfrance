---
ID: 2575
post_title: >
  Miner de l’ether (ETH) sous Windows 10
  avec une carte Nvidia et des drivers à
  jour
author: Ben
post_excerpt: ""
layout: post
permalink: >
  https://www.ethereum-france.com/miner-de-lether-eth-sous-windows-10-avec-une-carte-nvidia-et-des-drivers-a-jour/
published: true
post_date: 2017-08-29 09:30:09
---
<div>

Je voulais partager avec vous mon expérience sur comment miner efficacement de l'ether sous Windows 10 avec un GPU nvidia et des drivers à jour. J'ai passé pas mal de temps sur différents sites pour atteindre un hashrate décent.

Je vous recommande grandement de commencer par lire les 2 articles suivants :
<ul>
 	<li><a href="https://www.ethereum-france.com/comment-miner-de-lether-eth-windows/">Comment miner de l ether (ETH) sous Windows (introduction pour débutant)</a></li>
 	<li><a href="https://www.ethereum-france.com/tutoriel-complet-pour-miner-sur-la-blockchain-ethereum-mai-2017/">Tutoriel complet pour miner sur la blockchain Ethereum ; mai 2017</a></li>
</ul>
</div>
Notamment concernant la rentabilité et la difficulté grandissante de miner, ainsi que le futur passage annoncé en <a href="https://www.ethereum-france.com/quest-ce-que-la-preuve-denjeu-proof-of-stake-faq-par-v-buterin-traduction-francaise/">POW </a>de la blockchain ethereum.

Ceci étant dit, passons aux explications.

-----
<div>
<div>

Ma config est très simple : un PC orienté "gamer" avec une carte NVIDIA KFA2 GTX 970 (Black OC edition)

</div>
<div>

J'atteins un hashrate de 20 MHs après optimisation (versus les 3 MHs initiaux :))

J'utilise Claymore miner et ethermine pool, mais vous pouvez en choisir d'autres si vous préférez.

</div>
<div>
<div>
<div>

Ci-dessous quelques liens de téléchargement que vous aurez besoin si vous voulez suivre ce tuto :

</div>
</div>
</div>
<div>
<div>
<ul type="disc">
 	<li><a href="http://www.nvidia.fr/download/driverResults.aspx/123550/fr">Les derniers drivers nvidia</a> - 385.41 à ce jour</li>
 	<li><a href="https://bitcointalk.org/index.php?topic=1433925.0">Claymore 9.8 Miner</a></li>
 	<li><a href="http://download.msi.com/uti_exe/vga/MSIAfterburnerSetup.zip">MSI afterburner</a></li>
</ul>
</div>
</div>
</div>
&nbsp;
<h2><span style="text-decoration: underline;"><strong>Pour les architecture Pascal (10xx)</strong></span></h2>
Si vous avez une carte NVidia 10xx (Pascal), vous n'aurez pas grand chose à faire pour avoir un hashrate correct. Assurez vous juste d'avoir à minimum la version Anniversary Update de Windows 10, la version Créator Update étant recommandée.

Si vous n'etes pas sur de votre version, vous pouvez tapez "ver" dans une invite de commande (cmd) :
<ul>
 	<li>Microsoft Windows [version 10.0.15063] : Windows 10 Creator Update</li>
 	<li>Microsoft Windows [version 10.0.14393] : Windows 10 Anniversary Update</li>
</ul>
<div>
<div>
<div>

Vous n'aurez ensuite qu'a trouver vos réglages d'overclocking les plus adaptés dans MSI Afterburner.

&nbsp;
<h2><span style="text-decoration: underline;"><strong>Pour les architecture Maxwell (9xx)</strong></span></h2>
</div>
</div>
</div>
<h3><em><strong>Installation et configuration du drivers Nvidia</strong></em></h3>
Installer le drivers ne devrait pas être trop compliqué, mais du fine tuning est nécessaire.

Une fois le drivers installé, ouvrez le panneau de configuration Nvidia (click droit sur le Bureau)

Vous devriez voir cet écran avec en rouge, les modifications à passer à la config :

&nbsp;

Allez dans "Paramètres 3D" =&gt; "Gérer les paramètres 3D"
<ul type="disc">
 	<li>Vérifiez que "CUDA - Processeurs graphiques" est à "Tous"</li>
 	<li>Changer "DSR - Facteurs" à"2x"</li>
 	<li>(et le plus important) Mettez "Optimiser pour les performances de calcul" à "Activé"</li>
</ul>
<img class="aligncenter" src="https://image.ibb.co/f185vQ/NVIDIA_Control_Panel_2.jpg" alt="Nvidia Control Panel" width="646" height="525" />

Vous avez maintenant un driver nvidia optimisé pour le minage.

&nbsp;
<h3><em><strong>Installer Claymore</strong></em></h3>
Installer Claymore est plutôt simple, dézipper juste l'archive la ou vous voulez.

Créer un nouveau fichier dans le répertoire de Claymore (mining_ether.bat par exemple) avec  :
<pre>setx GPU_FORCE_64BIT_PTR 0
setx GPU_MAX_HEAP_SIZE 100
setx GPU_USE_SYNC_OBJECTS 1
setx GPU_MAX_ALLOC_PERCENT 100
setx GPU_SINGLE_ALLOC_PERCENT 100
EthDcrMiner64.exe -epool eu2.ethermine.org:14444 -ewal 0xdc7eFDbBE4aFD15c3385d1156b371333550FdDcF -epsw x -eworker benether.2 -mode 1 -allpools 1</pre>
<ul type="disc">
 	<li>setx : pour des paramètres de configuration du GPU</li>
 	<li>-epool eu2.ethermine.org:14444 : pour utiliser ethermine pool (vous pouvez en choisir un autre si vous voulez)</li>
 	<li>-ewal 0xdc7eFDbBE4aFD15c3385d1156b371333550FdDcF : l'adresse de votre wallet. METTEZ LE VOTRE !</li>
 	<li>-epsw x : mot de passe du pool si nécessaire</li>
 	<li>-eworker benether.2 : un nom arbitraire que vous voulez donner à votre worker</li>
 	<li> -mode 1 : ne miner que l'ether (ne pas faire de dual mining - les "devfee" sont à 1% dans ce mode - 2% si vous faite du dual mining)</li>
 	<li>-allpools 1 : nécessaire pour le devfee</li>
 	<li>Voir la doc de claymore pour le détail de toutes les options et le devfee</li>
</ul>
&nbsp;
<h3><em><strong>Fréquence GPU/Mémoire (Pstate) et overclocking</strong></em></h3>
Avant d'attaquer ce paragraphe, commencer à miner que votre GPU soit solicité.

Les cartes nvidia maxwell ont un mécanismes particulier permettant d'auto ajuster les fréquences GPU/Mémoire en fonction de la charge sur le GPU. Ca s'apelle les pstate (Performance State)

P0 est la performance maximale et est généralement utilisée quand vous jouez.

&nbsp;

Le hic, c'est que quand vous minez de l'ether, le drivers nvidia ne détecte pas cette activité comme intensive et laisse la carte en P2. Du coup en forceant manuellement à passer en P0 vous gagnerez quelques MHs (vous demanderez à votre carte de délivrer le maximum qu'elle peux) Changer de pstate n'est pas de l'overcloocking. Ca permet juste de dire à votre carte de tourner aux maximum de ces capacités d'usine.

Vous pouvez changer le pstate en utilisant l'utilistaire nvidia-smi (installé en meme temps que les drivers dans C:\Program Files\NVIDIA Corporation\NVSMI).

Les examples ci-dessous sont pour ma GTX 970, vous pouvez avoir des fréquences différentes en fonction de votre carte. Vous devez etre administrateur pour changer les pstate. Pour cela lancer une invite de commande en tant qu'admin (tapez 'cmd' dans la bare de recherche cortana et click droit =&gt; lancer en tant qu'admin)

La première commande est pour vérifier sur quel pstate votre carte est :
<pre>nvidia-smi.exe -q -d PERFORMANCE</pre>
Le pstate est indiqué dans la ligne "Performance State". Ca devrait etre P2 si vous n'avez rien fait de particulier.

Moi je suis en P0, mais ca devrait ressembler à ca :

<img class="aligncenter" src="https://image.ibb.co/gmie5Q/cmd_pstate.jpg" alt="" width="695" height="403" />

L seconde commande est pour récupérer les fréquences que votre carte graphique supporte (toujours sans overclocker)
<pre>nvidia-smi.exe -q -d SUPPORTED_CLOCKS|more</pre>
Nottez juste les 2 premières fréquences (Memory and Graphics). Sur ma carte c'est 3505 Mhz / 1506 Mhz

<img class="aligncenter" src="https://image.ibb.co/b9hHs5/cmd_supported.jpg" alt="" width="702" height="218" />

Vous pouvez ensuite forcer le mode P0 avec la commande suivante :
<pre>nvidia-smi.exe -ac 3505,1506</pre>
Vous pouvez maintenant vérifier avec 'nvidia-smi.exe -q -d PERFORMANCE'  que vous êtes bien en pstate P0.

&nbsp;

Mais… (et la c'est un peu étrange). Lancer MSI afterburner. Vous allez voir que la fréquence GPU de votre carte n'est pas celle que vous avez fixé avec nvidia-smi. Dans mon cas, c'est 1404/3505. Vous pouvez bougez manuellement le slider "Core Clock" jusqu’à la fréquence désirée (+102 pour moi)

Vous etes maintenant aux fréquences maximale (et hashrate) que votre carte permet nativement (sans overclocking donc)

Si vous continuer à augmenter le slider "Core Clock" (par exemple +123), vous constaterez que la fréquence ne monte pas mais que le voltage de la carte baisse ! (dans mon cas, je passe de 1212mv - config stock - à 1187 mv). Undervolter la carte peut-etre cool pour le mining du fait que vous consommerez moins d'électricité. Par contre la carte peux devenir instable si elle tourne à des hautes fréquences sans assez de courant.

Mais … (je comprend toujours pas plus ce qu'il se passe)

Si vous avez sauvegardés des setting dans des profils (par exemple +131Mhz GPU / +50 Mhz Memory) et que vous appliquez ce profil, dans ce cas vous allez réellement overcloocker votre carte. Le voltage utilisé sera celui natif de la carte (1212mv dans mon cas) mais et le GPU et la mémoire seront overcloockés. Dans mon cas ca sera 1535/3556 à 1212 mv.

C'est ma config que j'utilise pour miner, qui me permet d'atteindre 20 MHs sans errors d'overclocking dans claymore. A vous de trouver vos réglages les plus adaptés/stable à votre carte.

<img class="aligncenter" src="https://image.ibb.co/mBLgKk/mining.jpg" alt="" width="749" height="232" />

&nbsp;
<p style="text-align: center;"><em>J'espère que cet article vous aura permis de gagner quelques précieux MHs.</em></p>
<p style="text-align: center;"><em>Si vous vous sentez d'humeur généreuse, n'hésitez pas à m'envoyer quelques Ether sur mon wallet :  0xdc7eFDbBE4aFD15c3385d1156b371333550FdDcF</em></p>