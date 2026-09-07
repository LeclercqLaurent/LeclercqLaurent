## Laurent Leclercq · Codeam

**Développeur backend PHP, à Lyon.** Applications métier : une API Symfony
comme unique source de données, des interfaces React / TypeScript par-dessus,
et la vitrine publique servie par la même stack plutôt que par un CMS de plus.

![PHP](https://img.shields.io/badge/PHP-8.2+-777BB4?logo=php&logoColor=white)
![Symfony](https://img.shields.io/badge/Symfony-8-000000?logo=symfony&logoColor=white)
![Doctrine](https://img.shields.io/badge/Doctrine-ORM-FC6A31?logo=doctrine&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?logo=react&logoColor=black)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?logo=typescript&logoColor=white)
![PHPStan](https://img.shields.io/badge/PHPStan-level%209-2A9D8F)
![RGAA](https://img.shields.io/badge/RGAA%204-niveau%20AA-0053B3)

---

## 🧭 Comment je travaille

> Pas une liste d'intentions : chaque point se vérifie dans les dépôts plus bas.

🧩 &nbsp;**Le métier ne dépend de rien.**
Domaine en PHP pur : ni framework, ni ORM, ni SDK. Symfony et Doctrine sont des
adaptateurs branchés sur des ports définis par le métier, pas la structure du
projet.
*→ La suite de tests d'`elementor-twig-kit` tourne **sans WordPress, sans réseau
et sans base**. Pas un exploit : la conséquence mécanique d'une dépendance
orientée vers l'intérieur.*

🚦 &nbsp;**La QA est une barrière, pas une relecture.**
PHPStan niveau 9, PSR-12, un plancher de couverture à 90 % qui fait échouer le
build, du Gherkin écrit *avant* le code. La CI est l'autorité : sans elle au
vert, rien ne part.
*→ Là où l'outillage manque, je l'écris : `phpstan-sonar-rules`.*

📏 &nbsp;**Des faits, jamais une note.**
Une métrique confrontée à un seuil est un fait ; la même résumée en 7,5/10 est
une opinion déguisée en mesure. Idem pour les tests : les valeurs attendues
viennent de la spécification, jamais de la sortie de l'outil, car figer sa
propre sortie ne prouve que sa constance.
*→ `phpx-complexity` refuse de produire le moindre score, et des tests le
vérifient sur chaque format de sortie.*

🧯 &nbsp;**Concevoir la panne autant que le fonctionnement.**
Configuration incomplète, API injoignable, donnée mal saisie, dépendances
absentes : chacun dégrade le service et le journalise, aucun n'interrompt le
rendu de la page. Une extension qui casse un site parce qu'une clé manque coûte
plus cher que la fonctionnalité qu'elle apporte.

🗃️ &nbsp;**Le schéma de base ne dérive jamais.**
Toute modification passe par une migration Doctrine, générée par `diff`, relue,
testée sur base vierge. Jamais de `schema:update --force` : il tient en dev et
tombe à la première base reconstruite depuis les seules migrations, c'est-à-dire
en production, en CI, ou sur le poste du suivant.

♿ &nbsp;**Conformité par construction.**
RGAA 4 niveau AA, RGPD et ANSSI sont des contraintes de conception, pas des
correctifs de fin de projet : CSP stricte sans `unsafe-inline`, données sensibles
chiffrées, journalisation sans secret, contrastes et navigation clavier vérifiés
en revue.
*→ `rgaa4-referentiel` est né de ce travail.*

🔌 &nbsp;**Souveraineté et hors-ligne.**
Analyse statique, audit de complexité, capture d'e-mails, tests d'accessibilité :
tout ce qui peut tourner en local y reste. Une barrière qualité qui dépend d'un
service tiers n'est pas une barrière, c'est une dépendance de plus.

📝 &nbsp;**Documenter l'écart plutôt que le dissimuler.**
Aucun de ces principes ne tient à 100 % partout. Quand l'un cède, l'écart et son
motif sont écrits noir sur blanc. C'est plus utile au suivant que de prétendre
que le compromis n'existe pas.

---

## 📦 Ce que je publie ici

### 🔬 [phpx-complexity](https://github.com/LeclercqLaurent/phpx-complexity)
Auditeur de complexité PHP **multi-lentilles** et hors-ligne. Réimplémente
S3776 / S107 / S1142 nativement, y ajoute deux lentilles maison, puis **confronte
les lentilles entre elles** : leur divergence révèle ce qu'une métrique isolée
laisse passer. Aucun score, jamais.

### 🚦 [phpstan-sonar-rules](https://github.com/LeclercqLaurent/phpstan-sonar-rules)
Les deux règles de complexité **SonarQube** sans équivalent PHPStan : **S107**
(trop de paramètres) et **S1142** (trop de points de sortie). Seuils
configurables, sans serveur Sonar : la barrière existe avant le commit.

### ♿ [rgaa4-referentiel](https://github.com/LeclercqLaurent/rgaa4-referentiel)
Le **RGAA 4.1.2** en données exploitables (106 critères, 258 tests) et la
jointure **axe-core → WCAG → RGAA** dans les deux sens. Les outils automatisés
rapportent en WCAG, l'obligation légale s'exprime en RGAA : entre les deux, rien
n'était publié. Paquets PHP et Node.

### 🧩 [elementor-twig-kit](https://github.com/LeclercqLaurent/elementor-twig-kit)
Preuve de concept : des widgets Elementor rendus par **Twig** au lieu d'être
concaténés dans des `echo`. Échappement par défaut, gabarits surchargeables,
logique testable sans WordPress. Le vrai sujet y est le **mode dégradé**.

> **Le fil entre les quatre** : deux outils qui mesurent la complexité sans la
> résumer, un jeu de données qui rend l'accessibilité vérifiable, et une preuve
> de concept qui montre à quoi ressemble du code dont le métier ne dépend de rien.

---

## ✉️ Me joindre

[laurent@codeam.fr](mailto:laurent@codeam.fr)
