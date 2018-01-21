# Cours de 4TC(A)-CSC : Cryptographie et Sécurité des Communications

_François Lesueur ([francois.lesueur@insa-lyon.fr](mailto:francois.lesueur@insa-lyon.fr), [@FLesueur](https://twitter.com/FLesueur))_,
_Walid Bechkit ([walid.bechkit@insa-lyon.fr](mailto:walid.bechkit@insa-lyon.fr))_

<!-- ici un commentaire -->



[Structure](#structure-du-cours-4tc-csc) |
[Intro](#introduction-à-la-crypto) |
[Bases](#bases-de-la-crypto) |
[Maths](#maths-pour-la-crypto) |
[Passwords](#stockage-des-mots-de-passe) |
[PKI1](#pki1-autorités-de-certification) |
[PKI2](#pki2-dane-et-pgp) |
[Protocoles](#protocoles-cryptos) |
[Biblio](#bibliographie)


Introduction à la crypto
========================

Pour cette séance, vous devez étudier l'histoire de la cryptographie et de son utilisation. Nous nous baserons pour cela sur l'article de Wikipedia qui propose un bon historique : [WikipediaFR](https://fr.wikipedia.org/wiki/Histoire_de_la_cryptologie) 

N'oubliez pas d'aller remplir ensuite le QCM sur moodle !

<!-- La version anglaise va un peu plus loin et notamment sur les aspects politiques plus récents : [WikipediaEN](https://en.wikipedia.org/wiki/History_of_cryptography) -->

<!-- Intro sur la sécurité des coms en général, de césar/ égyptien a signal -->


Bases de la crypto
=================

Vous devez lire le cours de [Ghislaine Labouret](https://web.archive.org/web/20170516210655/http://www.hsc.fr/ressources/cours/crypto/crypto.pdf) <!-- http://www.hsc.fr/ressources/cours/crypto/crypto.pdf https://doc.lagout.org/security/Cryptographie%20.%20Algorithmes%20.%20Steganographie/HSC%20-%20Introduction%20a%20la%20cryptographie.pdf --> (jusqu'à la page 27/32). Vous y verrez les notions de cryptographie symétrique (ex AES), asymétrique (ex RSA), hash, chiffrement, signature ainsi que le problème de la distribution des clés. Ce cours est intéressant car bien construit mais assez ancien (2001). Les notions, principes et difficultés n'ont pas changé depuis, les algorithmes et tailles de clés si : cela vous donne une idée de l'évolution à attendre pendant les 10 prochaines années (hors découverte majeure). À vous de chercher quels sont les algorithmes souhaitables aujourd'hui. Pour les tailles de clés, le site [Key Length](http://www.keylength.com/) est très pratique.


La suite du travail est d'étudier le fonctionnement de RSA (sans entrer, pour l'instant, dans les fondements mathématiques), par exemple sur [Wikipedia](https://fr.wikipedia.org/wiki/Chiffrement_RSA). Prêtez une attention particulière à la génération des clés, aux mécanismes de chiffrement et déchiffrement.

Enfin, le programme [Bullrun](https://fr.wikipedia.org/wiki/Bullrun) donne un bon aperçu des forces et faiblesses de la cryptographie moderne : la partie mathématique est plutôt sûre, les attaques se concentrent sur l'usage (standardisation), le déploiement, l'implémentation, etc.

Ouverture (obligatoire): [La sélection de l'AES](https://videlalvaro.github.io/2014/03/you-dont-roll-your-own-crypto.html)

Ouverture (facultative): 

* [L'histoire de Dual\_EC\_DRBG](https://en.wikipedia.org/wiki/Dual_EC_DRBG)
* [Listen up, FBI: Juniper code shows the problem with backdoors, _Fahmida Y. Rashid, InfoWorld_](http://www.infoworld.com/article/3018029/virtual-private-network/listen-up-fbi-juniper-code-shows-the-problem-with-backdoors.html)

Cette section sera conclue par le TD1.





Maths pour la crypto
====================

Cette partie de cours s'intéresse principalement aux foncements mathématiques des cryptosystèmes asymétriques basés sur la difficulté du problème de la factorisation des grands nombres entiers et en particulier le cryptosystème RSA l’objet principal des deux séances. 

Chacune des deux séances de TD et TP va se dérouler en deux phases:

*	La première phase vise à comprendre la génération des clés RSA, la justification des choix des paramètres, le chiffrement, le déchiffrement, la preuve d’exactitude et l’évaluation du coût des opérations. Le cryptosystème RSA sera mis en place en TP en utilisant Python 3 et une évaluation de temps d’exécution des opérations de chiffrement déchiffrement en fonction des tailles de clés sera effectuée.

*	La deuxième phase concernera le problème RSA et son lien avec la factorisation des grands nombre entiers. Quelques algorithmes de factorisation basiques seront proposées progressivement en TD et ensuite implémentés, évaluées et comparés en TP.

Pour mieux suivre les différentes preuves et la conception de quelques algorithmes de factorisation, vous devez lire le cours de Marine Minier "Arithmétique pour la cryptographie" disponible sur http://perso.citi.insa-lyon.fr/mminier/images/Arithmetique_pour_Cryptographie_impression.pdf jusqu'à la slide 32. Ce cours donne les bases d’arithmétique nécessaires pour comprendre le cryptosystème RSA et les méthodes de factorisation qui seront traités. Pour la Crible d'Ératosthène, lisez plus de détails sur la page [Wikipedia](https://fr.wikipedia.org/wiki/Crible_d%27%C3%89ratosth%C3%A8ne). Pour la fonction indicatrice d'Euleur, lisez plus de détails sur la page [Wikipedia](https://fr.wikipedia.org/wiki/Indicatrice_d%27Euler).


Pour la première phase, relisez attentivement la [page Wikipedia]( https://fr.wikipedia.org/wiki/Chiffrement_RSA) expliquant RSA jusqu’à la section « Asymétrie ». 

Pour la partie problème RSA et factorisation, lisez la [page du problème RSA sur Wikipedia]( https://fr.wikipedia.org/wiki/Probl%C3%A8me_RSA) jusqu’à la section « Lien avec la factorisation ».

Ouverture (obligatoire):

Pour la partie factorisation, lisez le principe de l’algorithme p-1 de Pollard [Page Wikipédia, section principe]( https://fr.wikipedia.org/wiki/Algorithme_p-1_de_Pollard), le principe de l’algorithme de Pollard Rho [Page Wikipédia, section définition formelle]( https://fr.wikipedia.org/wiki/Algorithme_rho_de_Pollard) et le principe de l’algorithme de factorisation de Fermat [Page Wikipédia, sections intuition et méthode de base](https://fr.wikipedia.org/wiki/M%C3%A9thode_de_factorisation_de_Fermat)



<!-- 
Extrait du livre [Discrete Math for Computer Science Students, _Ken Bogart, Scot Drysdale, Cliff Stein_](https://web.archive.org/web/20170829125913/http://www.cse.iitd.ernet.in/~bagchi/courses/discrete-book/fullbook.pdf) ? 
pages de 66 à 82.

-->

<!-- https://www.kth.se/social/files/557ec6b0f27654784e263d66/fullbook.pdf  ,  
www.cse.iitd.ernet.in/~bagchi/courses/discrete-book/fullbook.pdf -->

<!--
Ouverture (obligatoire) : [Exemple de crypto symétrique : AES](http://www.moserware.com/2009/09/stick-figure-guide-to-advanced.html)

Stockage des mots de passe
==========================

Stockage des mots de passe [Serious Security: How to store your users’ passwords safely, _Paul Ducklin_](https://nakedsecurity.sophos.com/2013/11/20/serious-security-how-to-store-your-users-passwords-safely/)

[OWASP](https://www.owasp.org/index.php/Password_Storage_Cheat_Sheet)


PKI1, autorités de certification
================================

Ouverture (facultative): 

* Attaque Comodo 2011 [Lessons Learned from DigiNotar, Comodo and RSA Breaches, _Jeff Hudson, SecurityWeek_](http://www.securityweek.com/lessons-learned-diginotar-comodo-and-rsa-breaches)
-->

<!-- plus orienté CA/TLS/modèles de confiance : pinning, hsts, TOFU trust on first use, révocation. puis TP plus libre, sans le début trop bidouille RSA dans openssl, démarrer à CA avec plus de réflexion. SUjet limité à 2 pages, pas pousse-bouton. https://en.wikipedia.org/wiki/Opportunistic_encryption  -->


<!--

PKI2, DANE et PGP
=================

Vous avez vu dans le cours précédent les autorités de certification (CA) pour obtenir les clés publiques de tiers. Étudiez maintenant la [toile de confiance](https://en.wikipedia.org/wiki/Web_of_trust) telle qu'utilisée par PGP pour résoudre ce même problème (avec ses avantages et ses inconvénients). L'obtention de clés publiques est un service orthogonal au service de sécurité rendu par la cryptographie (ie, un même service, le mail chiffré et signé par exemple, peut-être rendu avec une approche type CA avec S/MIME ou une approche toile de confiance avec PGP).

-->

<!-- moxie : https://www.youtube.com/watch?v=pDmj_xe7EIQ  https://www.youtube.com/watch?v=Z7Wl2FW2TcA  https://moxie.org/blog/ssl-and-the-future-of-authenticity/  https://media.defcon.org/DEF%20CON%2019/DEF%20CON%2019%20video%20and%20slides/DEF%20CON%2019%20Hacking%20Conference%20Presentation%20By%20-%20Moxie%20Marlinspike%20-%20SSL%20And%20The%20Future%20Of%20Authenticity%20-%20Video%20and%20Slides.m4v-->

<!--

Protocoles cryptos
==================

Quelques protocoles et usages de la cryptographie, à étudier de manière adaptée au temps disponible :

* Le protocole [TLS](https://fr.wikipedia.org/wiki/Transport_Layer_Security) pour la sécurisation des échanges, qui utilise notamment [Diffie-Hellman](https://fr.wikipedia.org/wiki/%C3%89change_de_cl%C3%A9s_Diffie-Hellman) pour la génération d'une clé de session
* Le protocole [Kerberos](https://fr.wikipedia.org/wiki/Kerberos_%28protocole%29) pour l'authentification et l'autorisation, qui utilise notamment [Needham–Schroeder](https://en.wikipedia.org/wiki/Needham%E2%80%93Schroeder_protocol)
* Les [VPN](https://en.wikipedia.org/wiki/Virtual_private_network)

-->

<!-- Ouverture (obligatoire): [One Year of SSL Internet Measurement, _Olivier Levillain, Arnaud Ébalard, Benjamin Morin,Hervé Debar_](https://www.acsac.org/2012/openconf/modules/request.php?module=oc_program&action=view.php&a=&id=163&type=4&OPENCONF=tnkb1t3p2cgfsdcegc1dl5m251) -->
<!-- Ouverture (obligatoire): Neither Snow Nor Rain Nor MITM... An Empirical Analysis of Email Delivery Security -->

<!--
Cette section sera conclue par le TP OpenSSL.

Enjeux éthiques
===============

Crypto wars https://en.wikipedia.org/wiki/Crypto_Wars

-->

...

Bibliographie
=============

Livres :
* Histoire des codes secrets : De l'Égypte des Pharaons à l'ordinateur quantique, _Simon Singh_
* Architectures PKI et communications sécurisées, _DUMAS Jean-Guillaume, LAFOURCADE Pascal, REDON Patrick_
* Serious Cryptography, _Jean-Philippe Aumasson_

Films :
* Mr Robot
* The Imitation Game
* Citizenfour

![xkcd](http://imgs.xkcd.com/comics/security.png)

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/2.0/fr/"><img alt="Licence Creative Commons" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/2.0/fr/88x31.png" /></a><br />Ce(tte) œuvre est mise à disposition selon les termes de la <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/2.0/fr/">Licence Creative Commons Attribution - Pas d’Utilisation Commerciale - Partage dans les Mêmes Conditions 2.0 France</a>.
