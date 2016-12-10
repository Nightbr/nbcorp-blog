---
ID: 22
post_title: >
  Installer un serveur Starbound sur
  Debian x32/64
author: Titouan BENOIT
post_date: 2014-12-23 20:52:45
post_excerpt: ""
layout: post
permalink: >
  http://blog.nbcorp.fr/2014/12/installer-un-serveur-starbound-sur-debian-x3264/
published: true
post_views_count:
  - "603"
---
<p line-height:="" span="" style="\&quot;font-family:" trebuchet="">
 Bonjour &agrave; tous !
</p>

<p 100x="" access="" ai="" alors="" beta="" ce="" de="" en="" est="" et="" faut="" hui="" il="" jeu="" jeux="" mais="" me="" mieux="" moment="" ne="" o="" on="" p="" parler="" pas="" plus="" steam="" style="\&quot;text-align:" sur="" terraria="" va="">
 Pour ceux qui ne conna&icirc;trait pas Terraria, Starbound est un jeu type bac &agrave; sable/plateforme/aventure en 2D&nbsp;du style Minecraft mais en 2D. On se balade &agrave; bord d&#39;un vaisseau de plan&egrave;tes en plan&egrave;tes pour explorer, construire, piller, d&eacute;couvrir un univers g&eacute;n&eacute;r&eacute; proceduralement &agrave; l&#39;infini ! Vous trouverez plus d&#39;information sur le site officiel :&nbsp;<a href="https://playstarbound.com/">https://playstarbound.com/</a>
</p>

<p alors="" amis...="" avec="" box="" client="" de="" des="" donner="" en="" est="" et="" existants="" faut="" forcement="" google="" il="" installe="" ip="" jeu="" jouer="" la="" lancer="" le="" les="" leur="" local="" machine="" me="" on="" ouvre="" p="" personnes="" ports="" pour="" que="" s="" sa="" sachant="" seau="" serveur="" serveurs="" ses="" soit="" style="\&quot;text-align:" sur="" ton="" un="" vont="">
 Mais si on poss&egrave;de un serveur (chez soit ou ailleurs), voici une proc&eacute;dure pour installer Starbound sur son serveur :
</p>

<div class="\&quot;bb_h1\&quot;">
   Nous allons utiliser Steam en ligne de commande donc il vous faudra un compte steam avec le jeu Starbound.
</div>

<h2>
   1. Installation des librairies
</h2>

<p>
   Connecter vous en ssh &agrave; votre serveur (soit via putty pour windows, ou par la commande sur un syst&egrave;me linux)
</p>

<p>
  Il est possible que ces librairies soit d&eacute;j&agrave; install&eacute; (sur Ubuntu server par exemple).
</p>

<pre lang="\&quot;shell\&quot;">
apt-get install libvorbisfile3

dpkg --add-architecture i386

apt-get update

apt-get install ia32-libs
</pre>

<p>
  <br />
  R&eacute;cup&eacute;rer screen pour d&eacute;tacher le serveur du terminal o&ugrave; il sera lanc&eacute; :
</p>

<div class="\&quot;bb_code\&quot;">
 <pre class="\&quot;brush:bash;\&quot;">
apt-get install screen</pre>
</div>

<h2>
   2. Cr&eacute;er un nouvelle utilisateur
</h2>

<div class="\&quot;bb_code\&quot;">
  <pre class="\&quot;brush:php;\&quot;">
useradd -m -s /bin/bash -d /home/starbound starbound</pre>
</div>

<p>
  Changer le mot de passe :
</p>

<div class="\&quot;bb_code\&quot;">
  <pre class="\&quot;brush:bash;\&quot;">
passwd starbound</pre>
</div>

<p>
 <br />
  Maintenant, se connecter avec l&#39;utilisateur <strong>starbound</strong>
</p>

<h2>
 <strong>3. Installation de Steam</strong>
</h2>

<p>
 On va cr&eacute;er un nouveau dossier et installer steam dedans :
</p>

<div class="\&quot;bb_code\&quot;">
 <pre class="\&quot;brush:bash;\&quot;">
mkdir steamcmd

cd steamcmd

wget http://media.steampowered.com/client/steamcmd_linux.tar.gz

tar -xvzf steamcmd_linux.tar.gz

rm steamcmd_linux.tar.gz</pre>
</div>

<p>
 <br />
  Lancer un premi&egrave;re fois steamcmd pour faire des &eacute;ventuelles mise &agrave; jour :
</p>

<div class="\&quot;bb_code\&quot;">
  <pre class="\&quot;brush:bash;\&quot;">
./steamcmd.sh</pre>

   <p>
     &nbsp;
  </p>
</div>

<h2>
   4. T&eacute;l&eacute;chargement de Starbound
</h2>

<p>
 Apr&egrave;s avoir lancer SteamCMD, il va falloir se connecter &agrave; votre compte steam qui contient le jeu Starbound.<br />
 <b>Pas de soucis, c&#39;est un client steam comme les autres, votre mot de passe reste toujours prot&eacute;g&eacute;.</b>
</p>

<div class="\&quot;bb_code\&quot;">
 <pre class="\&quot;brush:bash;\&quot;">
login username password</pre>
</div>

<div class="\&quot;bb_code\&quot;">
  Remplacer username et password par vos logins.
</div>

<p>
 Si jamais SteamGuard vous demande un code, aller v&eacute;rifier vos emails pour r&eacute;cup&eacute;rer le code.
</p>

<p>
  Une fois connect&eacute;, nous allons donc t&eacute;l&eacute;charger le jeu Starbound sur le serveur (les fichiers du serveur sont inclues avec le jeu).
</p>

<p>
  On peut choisir o&ugrave; installer le jeu avec la commande :
</p>

<div class="\&quot;bb_code\&quot;">
  <pre class="\&quot;brush:bash;\&quot;">
force_install_dir ./starbound</pre>

  <p>
     Puis installer le jeu avec cette commande :
 </p>

   <pre class="\&quot;brush:bash;\&quot;">
app_update 211820</pre>
</div>

<p>
   Et maintenant allez&nbsp;vous chercher un caf&eacute;... le jeu t&eacute;l&eacute;charge.
</p>

<div class="\&quot;bb_code\&quot;">
 Une fois termin&eacute;, vous pouvez quitter steamcmd via cette commande :
</div>

<div class="\&quot;bb_code\&quot;">
  <pre class="\&quot;brush:bash;\&quot;">
quit</pre>

   <p>
     &nbsp;
  </p>
</div>

<h2>
   5. Lancement du serveur
</h2>

<p>
 Aller dans le dossier de Starbound (Attention, si vous n&#39;avez pas fait la commande force_install_dir, le jeu se trouve dans ~/Steam/SteamApp/common)
</p>

<pre class="\&quot;brush:bash;\&quot;">
cd starbound</pre>

<p>
   choisir le bon dossier si vous &ecirc;tes sur un os x32 ou x64 :
</p>

<div class="\&quot;bb_code\&quot;">
  <pre class="\&quot;brush:bash;\&quot;">
cd linux64 ou cd linux32

chmod +x *</pre>

 <p>
     Maintenant nous allons cr&eacute;er un script shell pour pouvoir lancer proprement le serveur avec screen pour pouvoir quitter notre console ssh sans terminer le serveur :
  </p>
</div>

<div class="\&quot;bb_code\&quot;">
   <pre class="\&quot;brush:bash;\&quot;">
nano startserver.sh</pre>
</div>

<div class="\&quot;bb_code\&quot;">
   copier/coller ce code dans le fichier:
   <p>
     &nbsp;
  </p>

   <pre class="\&quot;brush:bash;\&quot;">
screen -AmS sb ./starbound_server</pre>

 <p>
     Puis :
  </p>

   <pre class="\&quot;brush:bash;\&quot;">
Ctrl+X

y

chmod +x startserver.sh</pre>
</div>

<p>
 Finalement lancer le serveur !
</p>

<div class="\&quot;bb_code\&quot;">
   <pre class="\&quot;brush:bash;\&quot;">
./startserver.sh
</pre>
</div>

<p>
   Maintenant si vous voulez fermer votre console SSH, utiliser cette combinaison de touches :
</p>

<div class="\&quot;bb_code\&quot;">
  ctrl+a+d
   <p>
     &nbsp;
  </p>

   <p>
     &nbsp;
  </p>

   <p>
     <span .="" 6.="" :="" cette="" class="\&quot;brush:bash;\&quot;" client="" commande="" courant="" ctrl="" div="" du="" est="" et="" exemple="" fermer="" jour="" lancer="" le="" mise="" ou="" par="" pour="" pouvez="" pre="" putty="" retrouver="" screen="" serveur="" si="" steamcmd="" style="\&quot;font-size:" terminal="" terminer="" utiliser="" votre="" voulez="" vous=""><span :="" class="\&quot;brush:bash;\&quot;" finalement="" jeu="" jour="" le="" mettez="" pre="" style="\&quot;font-size:">Note : si vous avez&nbsp;un Firewall n&#39;oubli&eacute; pas de forward le port 21025 </span></span>
   </p>

   <p>
     <span .="" 6.="" :="" cette="" class="\&quot;brush:bash;\&quot;" client="" commande="" courant="" ctrl="" div="" du="" est="" et="" exemple="" fermer="" jour="" lancer="" le="" mise="" ou="" par="" pour="" pouvez="" pre="" putty="" retrouver="" screen="" serveur="" si="" steamcmd="" style="\&quot;font-size:" terminal="" terminer="" utiliser="" votre="" voulez="" vous=""><span :="" class="\&quot;brush:bash;\&quot;" finalement="" jeu="" jour="" le="" mettez="" pre="" style="\&quot;font-size:">source : http://steamcommunity.com/sharedfiles/filedetails/?id=200785834 </span></span>
 </p>
</div>