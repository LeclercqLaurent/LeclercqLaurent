## Laurent Leclercq — Codeam

Développeur backend PHP, à Lyon. Je conçois et j'exploite des applications
métier : une API Symfony comme unique source de données, des interfaces React /
TypeScript par-dessus, et la vitrine publique servie par la même stack plutôt
que par un CMS de plus — un seul périmètre à auditer, un seul design system.

---

### Comment je travaille

Ce qui suit n'est pas une liste d'intentions : chaque point se vérifie dans les
dépôts ci-dessous.

**Le métier ne dépend de rien.** Architecture hexagonale et DDD : le domaine est
du PHP pur, sans framework, sans ORM, sans SDK. Symfony et Doctrine sont des
adaptateurs branchés sur des ports définis par le métier — pas la structure du
projet. Les contextes bornés communiquent par événements de domaine, les
lectures et les écritures sont séparées, et tout concept porteur d'invariant
devient un objet-valeur plutôt qu'une primitive nue.

La conséquence est vérifiable, et c'est à ça qu'on reconnaît que la séparation
tient : dans [`elementor-twig-kit`](https://github.com/LeclercqLaurent/elementor-twig-kit),
la suite de tests s'exécute **sans WordPress, sans Elementor, sans réseau et
sans base de données**. Ce n'est pas un tour de force, c'est ce que produit
mécaniquement une dépendance qui ne va que vers l'intérieur.

**La QA est une barrière, pas une relecture.** PHPStan au niveau 9, PSR-12,
un plancher de couverture à 90 % qui fait échouer le build, et des spécifications
exécutables en Gherkin écrites *avant* le code. Un garde-fou hors-ligne tourne
avant chaque commit ; la CI reste l'autorité — sans elle au vert, rien ne part.

Là où l'outillage manque, je l'écris :
[`phpstan-sonar-rules`](https://github.com/LeclercqLaurent/phpstan-sonar-rules)
comble les deux règles de complexité SonarQube que l'écosystème PHPStan laissait
sans équivalent, pour que la barrière existe avant le commit et pas seulement en
revue.

**Des faits, jamais une note.** Une métrique confrontée à un seuil est un fait ;
la même résumée en 7,5/10 est une opinion déguisée en mesure.
[`phpx-complexity`](https://github.com/LeclercqLaurent/phpx-complexity) pousse ce
parti pris jusqu'au refus explicite de produire le moindre score, et des tests le
vérifient sur chaque format de sortie. Le corollaire vaut pour les tests
eux-mêmes : les valeurs attendues sont dérivées de la spécification, pas de la
sortie de l'outil — figer sa propre sortie ne prouve que sa constance.

**Concevoir la panne autant que le fonctionnement.** Configuration incomplète,
API injoignable, réponse illisible, donnée mal saisie, dépendances absentes :
chacun de ces cas doit dégrader le service et le journaliser, aucun ne doit
interrompre le rendu de la page. Une extension qui casse un site en production
parce qu'une clé manque coûte plus cher que la fonctionnalité qu'elle apporte.
C'est le vrai sujet d'`elementor-twig-kit`, davantage que les gabarits.

**Le schéma de base ne dérive jamais.** Toute modification passe par une
migration Doctrine, générée par `diff`, relue, et testée sur une base vierge
avant la production. Jamais de `schema:update --force` : il fait tenir le schéma
en développement et le fait tomber à la première base reconstruite depuis les
seules migrations — c'est-à-dire en production, en CI, ou sur le poste du
suivant.

**Conformité par construction.** RGAA 4 niveau AA, RGPD et recommandations ANSSI
sont des contraintes de conception, pas des correctifs de fin de projet : CSP
stricte sans `unsafe-inline`, données sensibles chiffrées en base, journalisation
sans secret, navigation clavier et contrastes vérifiés en revue.
[`rgaa4-referentiel`](https://github.com/LeclercqLaurent/rgaa4-referentiel) est né
de ce travail : les outils automatisés rapportent en WCAG, l'obligation légale
s'exprime en RGAA, et personne ne publiait la correspondance.

**Souveraineté et hors-ligne.** Analyse statique, audit de complexité, capture
d'e-mails, tests d'accessibilité : tout ce qui peut tourner en local y reste. Une
barrière qualité qui dépend d'un service tiers n'est pas une barrière, c'est une
dépendance de plus — et elle tombe le jour où le réseau tombe.

**Documenter l'écart plutôt que le dissimuler.** Aucun de ces principes ne tient
à 100 % dans tous les contextes. Quand l'un cède, l'écart et son motif sont
écrits noir sur blanc, dans le code et dans le README — c'est plus utile au
suivant que de prétendre que le compromis n'existe pas.

---

### Ce que je publie ici

| Projet | Ce que c'est |
|---|---|
| [**phpx-complexity**](https://github.com/LeclercqLaurent/phpx-complexity) | Auditeur de complexité PHP multi-lentilles et hors-ligne. Réimplémente nativement S3776 / S107 / S1142, y ajoute deux lentilles maison, et **confronte les lentilles entre elles** : leur divergence révèle ce qu'une métrique isolée laisse passer. Aucun score, jamais — des compteurs confrontés à des seuils. |
| [**phpstan-sonar-rules**](https://github.com/LeclercqLaurent/phpstan-sonar-rules) | Les deux règles de complexité **SonarQube** que l'écosystème PHPStan laissait sans équivalent : **S107** (trop de paramètres) et **S1142** (trop de points de sortie). Seuils configurables, hors-ligne, sans serveur Sonar — la barrière existe avant le commit, pas seulement en revue. |
| [**rgaa4-referentiel**](https://github.com/LeclercqLaurent/rgaa4-referentiel) | Le **RGAA 4.1.2** en données exploitables — 106 critères, 258 tests — et surtout la jointure **axe-core → WCAG → RGAA** dans les deux sens. Les outils automatisés rapportent en WCAG, l'obligation légale s'exprime en RGAA : entre les deux, rien n'était publié. Paquets PHP et Node servis depuis un jeu de données unique. |
| [**elementor-twig-kit**](https://github.com/LeclercqLaurent/elementor-twig-kit) | Preuve de concept : des widgets Elementor dont le balisage est rendu par **Twig** au lieu d'être concaténé dans des `echo`. Échappement par défaut, gabarits surchargeables, et une logique testable **sans WordPress, sans réseau et sans base**. Le vrai sujet y est le mode dégradé : rien de ce qui manque n'interrompt le rendu du site. |

Le fil entre les quatre : deux outils qui mesurent la complexité sans la
résumer, un jeu de données qui rend l'accessibilité vérifiable, et une preuve de
concept qui montre à quoi ressemble du code dont le métier ne dépend de rien.

---

### Me joindre

[laurent@codeam.fr](mailto:laurent@codeam.fr)
