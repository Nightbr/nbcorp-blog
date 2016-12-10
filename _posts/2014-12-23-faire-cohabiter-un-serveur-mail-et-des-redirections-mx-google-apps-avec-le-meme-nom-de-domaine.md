---
ID: 18
post_title: >
  Faire cohabiter un serveur mail et des
  redirections MX (Google Apps) avec le
  même nom de domaine
author: Titouan BENOIT
post_date: 2014-12-23 20:45:15
post_excerpt: ""
layout: post
permalink: >
  http://blog.nbcorp.fr/2014/12/faire-cohabiter-un-serveur-mail-et-des-redirections-mx-google-apps-avec-le-meme-nom-de-domaine/
published: true
post_views_count:
  - "505"
---
<p>
 Il se trouve que j&#39;ai eu ce probl&egrave;me et que j&#39;ai perdu une soir&eacute;e la dessus&nbsp;(et bien &eacute;videment juste au moment de passer un projet en ligne sinon c&#39;est pas dr&ocirc;le ^^) et donc je vais proposer quelques explications sur ce sujet.
</p>

<p>
 j&#39;ai trouv&eacute; pas mal de sujet relatant ce probl&egrave;me : (ici des probl&egrave;mes en utilisant sendmail comme serveur smtp)
</p>

<ul>
 <li>
    <a href="http://stackoverflow.com/questions/351297/can-i-use-google-apps-for-domain-email-and-still-use-a-sendmail-server-to-send?rq=1">http://stackoverflow.com/questions/351297/can-i-use-google-apps-for-domain-email-and-still-use-a-sendmail-server-to-send?rq=1</a>
 </li>
   <li>
    <a href="http://stackoverflow.com/questions/524224/how-do-i-send-mail-to-my-google-apps-mail-server-from-the-webserver-with-the-sam?rq=1">http://stackoverflow.com/questions/524224/how-do-i-send-mail-to-my-google-apps-mail-server-from-the-webserver-with-the-sam?rq=1</a>
   </li>
</ul>

<p>
 Je vais tout d&#39;abord replacer le contexte.
</p>

<h2>
  Contexte :
</h2>

<p>
  J&#39;ai un nom de domaine que l&#39;on nommera <strong>domaine.net </strong>et j&#39;ai une machine d&eacute;di&eacute; (un petit kimsufi&nbsp;qui sont de retour ^^) pour un projet d&#39;application web. J&#39;ai besoin d&#39;un serveur SMTP pour envoyer des mails depuis mon application web, j&#39;utilise <strong>Postfix</strong>. De plus, j&#39;ai des redirections MX de mon domaine.net vers les serveurs de Google App pour avoir des adresses mail du type :&nbsp;
</p>

<ul>
 <li>
    contact@domaine.net
 </li>
   <li>
    postmaster@domaine.net
 </li>
   <li>
    ...
  </li>
</ul>

<p>
 Et je laisse Gmail g&eacute;rer mes mails et j&#39;ai acc&egrave;s &agrave; tous les services de Google : drive , calendar, ...
</p>

<p>
   Bon jusque l&agrave; tous&nbsp;vas bien !
</p>

<p>
  J&#39;installe postfix normalement (via apt mais il est souvent d&eacute;j&agrave; install&eacute;), et ensuite je lance la configuration :
</p>

<pre class="\&quot;code\&quot;">
sudo dpkg-reconfigure postfix</pre>

<p>
   Donc on suit les instructions, on ajoute notre nom de domaine <strong>domaine.net</strong> partout o&ugrave; c&#39;est demand&eacute; pour avoir une configuration de base pour postfix.
</p>

<p>
   Le probl&egrave;me, c&#39;est que maintenant on a un serveur mail avec le nom de domaine <strong>domaine.net&nbsp;</strong>et quand on envoit un mail via l&#39;application web h&eacute;berg&eacute; par le serveur &agrave; l&#39;adresse &quot;contact@domaine.net&quot; et bien &ccedil;a ne fonctionne pas !!
</p>

<p>
 Mais que fait donc notre serveur ?!! En fait, si on regarde dans les logs de postfix, on peut voir que le Serveur de messagerie a bien essay&eacute; d&#39;envoyer le message mais l&#39;utilisateur local &quot;contact&quot; n&#39;existe pas dans la machine... En effet, si on dit qu&#39;on est sur le serveur mail domaine.net, contact@domaine.net devrait pointer sur ce serveur... Mais dans notre DNS, on a bien sp&eacute;cifi&eacute; une redirection MX (Mail eXchange) vers les serveurs google App. Il faut donc dire au serveur mail de ne pas chercher directement un utilisateur local pour le domaine <strong>domaine.net</strong>.
</p>

<h2>
   Solution :&nbsp;
</h2>

<p>
  La solution est dans une option de postfix :
</p>

<p>
  Dans le<em> </em><em>/etc/postfix/main.cf</em> il faut v&eacute;rifier que notre nom domaine <strong>domaine.net</strong> n&#39;y est pas inscrit dans l&#39;option mydestination :
</p>

<pre class="\&quot;code\&quot;">
mydestination = localhost, 127.0.0.1, ...</pre>

<p>
  Apr&egrave;s un petit reload du service &ccedil;a devrait fonctionner :
</p>

<pre class="\&quot;code\&quot;">
sudo service postfix reload</pre>

<p>
 <span style="\&quot;color:#008000;\&quot;">Et maintenant moment magique, on peut enfin envoyer des mails via notre serveur SMTP vers des adresses en xxx@domaine.net !!!</span>
</p>

<p>
 Cet&nbsp;article est assez complexe et traite d&#39;un point particulier qui pourra&nbsp;s&ucirc;rement aider les personnes qui sont face &agrave; ce probl&egrave;me. Il est en aucun cas un Tuto pour configurer un serveur Postfix et des redirections MX pour Google App.
</p>

<p>
  J&#39;esp&egrave;re que cet article permettera &agrave; certains de ne pas perdre une soir&eacute;e sur ce probl&egrave;me ;)
</p>

<p>
  &nbsp;
</p>