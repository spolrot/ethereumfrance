---
ID: 1946
post_title: 'Tutoriel : rejoindre Kovan le testnet de Parity technologies'
author: JdeTychey
post_excerpt: ""
layout: post
permalink: >
  https://www.ethereum-france.com/tutoriel-rejoindre-kovan-le-testnet-de-parity-technologies/
published: true
post_date: 2017-03-10 20:09:55
---
Kovan est une blockchain mise en place par Parity Technologies (aussi connu sous le nom de <a href="http://ethcore.io/">Ethcore</a>). Cette blockchain est dédié aux tests et au développement d'applications sur Ethereum. A la différence de la chaîne principale d'Ethereum il n'y a pas de mineurs, les blocs sont créés par certains noeuds qui ont autorité sur la chaîne selon un algorithme mis au point par Parity Technologies: "<a href="https://github.com/ethcore/parity/wiki/Proof-of-Authority-Chains">Proof of Authority</a>".

Ce réseau dispose d'un explorateur web fourni par etherscan: <a href="https://kovan.etherscan.io/">https://kovan.etherscan.io/</a>

Des ethers sur cette blockchain sont distribués gratuitement via ce <a href="https://github.com/kovan-testnet/faucet">guide</a>.
<h1>Se connecter au réseau Kovan</h1>
Kovan n'est pour l'instant compatible qu'avec Parity et à partir de la version 1.5.7. Pour mettre à jour le client Parity rendez-vous <a href="https://ethcore.io/parity.html">ici</a>.
En cas de besoin d'aide à l'installation, vous pouvez vous rendre sur le <a href="https://gitter.im/ethcore/parity">chan gitter de Parity</a> (en anglais) ou bien sur le <a href="https://asseth.slack.com/messages/general/">slack de l'Asseth</a> ou de CryptoFR.
<h2>OSX / Linux</h2>
Après l'installation ou la mise à jour, assurez vous que le ficher <a href="https://raw.githubusercontent.com/kovan-testnet/config/master/kovan-config.json">kovan-config.json </a>est présent dans le dossier de Parity.

Ouvrez le terminal et entrez:
<blockquote>parity --chain=kovan</blockquote>
<h2>Windows</h2>
Suivez ce guide vidéo en anglais:

<iframe src="https://www.youtube.com/embed/dTjstkfOT8E" width="560" height="315" frameborder="0" allowfullscreen="allowfullscreen"></iframe>

&nbsp;
<h2>Aller plus loin en référençant publiquement son noeud</h2>
&nbsp;

Il existe un serveur permettant de surveiller l'état du réseau comme sur la chaîne principale: <a href="https://stats.kovan.network">https://stats.kovan.network</a>

Pour référencer votre noeud voici la marche à suivre:
<ul>
 	<li>Installez l'application l'API:</li>
</ul>
<blockquote><code>git clone https://github.com/cubedro/eth-net-intelligence-api; cd eth-net-intelligence-api;
npm install;
npm install -g pm2;</code></blockquote>
<ul>
 	<li>Editez le fichier app.json dans le répertoire nouvellement créé, attention il vous faudra demander le mot de passe sur slack ou gitter</li>
</ul>
<pre><code>[
  {
    "name"              : "kovan-netstats",
    "script"            : "app.js",
    "log_date_format"   : "YYYY-MM-DD HH:mm Z",
    "merge_logs"        : false,
    "watch"             : false,
    "max_restarts"      : 10,
    "exec_interpreter"  : "node",
    "exec_mode"         : "fork_mode",
    "env":
    {
      "NODE_ENV"        : "production",
      "INSTANCE_NAME"   : "LE NOM DE VOTRE NOEUD",
      "CONTACT_DETAILS" : "COMMENT VOUS CONTACTER",
      "WS_SERVER"       : "wss://stats.kovan.network",
      "WS_SECRET"       : "[à demander sur slack ou gitter]",
      "VERBOSITY"       : 2
    }
  }
]</code></pre>
<ul>
 	<li>Lancez l'application!</li>
</ul>
<blockquote>pm2 start app.json</blockquote>
&nbsp;