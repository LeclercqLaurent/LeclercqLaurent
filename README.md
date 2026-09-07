## Laurent Leclercq — Codeam

Développeur backend PHP, à Lyon. Je conçois et j'exploite des applications
métier : une API Symfony comme unique source de données, des interfaces React /
TypeScript par-dessus.

### Comment je travaille

**Architecture hexagonale et DDD.** Le domaine est du PHP pur — aucune
dépendance au framework, aucun ORM, aucun SDK. Symfony et Doctrine sont des
adaptateurs branchés sur des ports définis par le métier, pas la structure du
projet. Les contextes bornés communiquent par événements de domaine, les
lectures et les écritures sont séparées (CQRS).

**La QA n'est pas une étape finale.** PHPStan au niveau 9, PSR-12, 90 % de
couverture minimum, spécifications exécutables en Gherkin écrites *avant* le
code. Un garde-fou hors-ligne tourne avant chaque commit et la CI reste
l'autorité : sans elle au vert, rien ne part.

**Conformité par construction.** RGAA 4 niveau AA, RGPD et recommandations
ANSSI ne sont pas des correctifs de fin de projet mais des contraintes de
conception — CSP stricte sans `unsafe-inline`, données sensibles chiffrées en
base, navigation clavier et contrastes vérifiés en revue.

**Souveraineté des outils.** Analyse statique, capture d'e-mails, tests
d'accessibilité, audit de complexité : tout ce que je peux faire tourner en
local et hors-ligne y reste.

### Ce que je publie ici

| Projet | Ce que c'est |
|---|---|
| [**phpx-complexity**](https://github.com/LeclercqLaurent/phpx-complexity) | Auditeur de complexité PHP multi-lentilles et hors-ligne. Réimplémente nativement S3776 / S107 / S1142, y ajoute deux lentilles maison, et **confronte les lentilles entre elles** : leur divergence révèle ce qu'une métrique isolée laisse passer. Aucun score, jamais — des compteurs confrontés à des seuils. |
| [**rgaa4-referentiel**](https://github.com/LeclercqLaurent/rgaa4-referentiel) | Le **RGAA 4.1.2** en données exploitables — 106 critères, 258 tests — et surtout la jointure **axe-core → WCAG → RGAA** dans les deux sens. Les outils automatisés rapportent en WCAG, l'obligation légale s'exprime en RGAA : entre les deux, rien n'était publié. Paquets PHP et Node servis depuis un jeu de données unique. |
| [**elementor-twig-kit**](https://github.com/LeclercqLaurent/elementor-twig-kit) | Preuve de concept : des widgets Elementor dont le balisage est rendu par **Twig** au lieu d'être concaténé dans des `echo`. Échappement par défaut, gabarits surchargeables, et une logique testable **sans WordPress, sans réseau et sans base**. Le vrai sujet y est le mode dégradé : rien de ce qui manque n'interrompt le rendu du site. |

### Me joindre

[laurent@codeam.fr](mailto:laurent@codeam.fr)
