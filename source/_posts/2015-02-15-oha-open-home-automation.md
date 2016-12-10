---
ID: 57
post_title: 'OHA : Open Home Automation'
author: Titouan BENOIT
post_date: 2015-02-15 11:25:47
post_excerpt: ""
layout: post
permalink: >
  http://blog.nbcorp.fr/2015/02/oha-open-home-automation/
published: true
post_views_count:
  - "359"
---
<h1>
   OHA - Open Home Automation
</h1>

<p>
 En derni&egrave;re ann&eacute;e d&#39;&eacute;cole d&#39;ing&eacute;nieur, nous avions la possibilit&eacute; de r&eacute;aliser un projet technique sur le sujet de notre choix. Il se trouve que j&#39;avais depuis longtemps envie de d&eacute;velopper ma propre solution de domotique. En effet, je regardais souvent du c&ocirc;t&eacute; de <a href="http://blog.encausse.net/s-a-r-a-h/">S.A.R.A.H.</a> ou encore <a href="http://gladysproject.com/accueil">Gladys</a>. Il en existe plein d&#39;autre qui offre souvent la couche logicielle et qui sont Open Source mais je n&#39;ai jamais vraiment trouv&eacute; de solution compl&egrave;te Open Hardware et Open Source.
</p>

<p>
  Mais dans un premier temps, un petit rappel sur ce qu&#39;est la domotique :
</p>

<p>
   <em>La domotique est l&rsquo;ensemble des techniques de l&#39;&eacute;lectronique, de physique du b&acirc;timent, d&#39;automatisme, de l&#39;informatique et des t&eacute;l&eacute;communications utilis&eacute;es dans les b&acirc;timents, plus ou moins &laquo; interop&eacute;rables &raquo; et permettant de centraliser le contr&ocirc;le des diff&eacute;rents syst&egrave;mes et sous-syst&egrave;mes de la maison et de l&#39;entreprise (chauffage, volets roulants, porte de garage, portail d&#39;entr&eacute;e, prises &eacute;lectriques, etc.).</em>
</p>

<p>
  <strong>Mais qu&#39;est ce que OHA :</strong>
</p>

<p>
 Open Home Automation est un projet de domotique Open Source innovant qui permettra de contr&ocirc;ler les &eacute;quipements de la maison, volets, lampes, chauffages par l&rsquo;interm&eacute;diaire de son smartphone, tablette, PC, Laptop, etc. OHA propose une solution domotique qui ne n&eacute;cessitera pas de changement important dans les installations de la maison, comme c&rsquo;est le cas pour les solutions domotiques du march&eacute;. De plus chacun (particulier ou entreprise) pourra construire et ajouter son propre &eacute;quipement connect&eacute; gr&acirc;ce &agrave; la Centrale Intelligente OHA qui d&eacute;tecte automatiquement les nouveaux &eacute;quipements domotiques compatibles. OHA n&rsquo;est pas qu&rsquo;un simple syst&egrave;me domotique propri&eacute;taire, c&rsquo;est un univers d&rsquo;objets connect&eacute;s o&ugrave; chacun peut ajouter le sien.
</p>

<p>
   Pour OHA, nous voulions d&eacute;velopper un syst&egrave;me ouvert offrant une bonne base pour toutes les applications de domotique. Voici un sch&eacute;ma fonctionnel du syst&egrave;me :
</p>

<p>
   <a href="http://blog.nbcorp.fr/wp-content/uploads/2015/02/schéma-principale.png"><img alt="schéma principale" class="alignnone size-large wp-image-62" height="539" src="http://blog.nbcorp.fr/wp-content/uploads/2015/02/schéma-principale-1024x756.png" width="730" /></a>
</p>

<p>
   Cette article pr&eacute;sentera globalement le syst&egrave;me mais je ferais s&ucirc;rement d&#39;autre article plus technique qui d&eacute;taillera les diff&eacute;rentes parties du syst&egrave;me.
</p>

<p>
 Nous &ecirc;tions une &eacute;quipe de 4 personnes (2 personnes sur le logiciel API+client web et 2 personnes sur le reste : d&eacute;veloppement du daemon python + des modules Arduino). Ce projet a dur&eacute; environ 6 mois (de Septembre 2014 &agrave; Janvier 2015) et nous nous &eacute;tions fix&eacute; comme objectif d&#39;avoir un serveur communicant avec un module simple de lampe connect&eacute;e.
</p>

<p>
 Voici la maquette finale du syst&egrave;me :
</p>

<p>
  <a href="http://blog.nbcorp.fr/wp-content/uploads/2015/02/oha-maquette-1.jpg"><img alt="oha-maquette (1)" class="alignnone size-full wp-image-64" height="506" src="http://blog.nbcorp.fr/wp-content/uploads/2015/02/oha-maquette-1.jpg" width="900" /></a>
</p>

<p>
  Voici quelques vid&eacute;os (playlist Youtube) de d&eacute;monstration qui montrent les fonctionnalit&eacute;s de base de syst&egrave;me.
</p>

<p>
 <iframe allowfullscreen="" frameborder="0" height="315" src="https://www.youtube.com/embed/videoseries?list=PLsTK3RYVBmuDBkJ-arTuKlfv2TFFZgNXX" width="560"></iframe>
</p>

<p>
 Et sinon comme le syst&egrave;me est Open Source, retrouvez tous nos documents sur Dropbox et le code sur notre serveur git :
</p>

<ul>
 <li>
    <a href="https://www.dropbox.com/sh/elvth88n0mhhb0w/AADJKHIOZmS7qmZaeL1MDOVha?dl=0">OHA Dropbox</a>
  </li>
   <li>
    git OHA Web client : <a href="http://git.nbcorp.fr/oha/oha-web-client">http://git.nbcorp.fr/oha/oha-web-client</a>
  </li>
   <li>
    git OHA API : <a href="http://git.nbcorp.fr/oha/oha-api">http://git.nbcorp.fr/oha/oha-api</a>
  </li>
   <li>
    git OHA Python Core : <a href="http://git.nbcorp.fr/oha/oha-python-core">http://git.nbcorp.fr/oha/oha-python-core</a>
  </li>
   <li>
    git OHA Module Core : <a href="http://git.nbcorp.fr/oha/oha-module-core">http://git.nbcorp.fr/oha/oha-module-core</a>
  </li>
</ul>

<p>
 Voil&agrave;, &ccedil;a sera tout pour cette article d&#39;introduction, je vais refaire d&#39;autre article sur le sujet pour pr&eacute;senter l&#39;architecture globale du syst&egrave;me, les diff&eacute;rents composants (API, Daemon, ...).
</p>

<p>
  Si vous avez des questions, n&#39;h&eacute;sitez pas &agrave; les poser en commentaire ;)
</p>

<p>
  &nbsp;
</p>