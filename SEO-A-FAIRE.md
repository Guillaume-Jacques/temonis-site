# Correctifs SEO, ce qui est fait et ce qui reste à faire à la main

## Fait dans les fichiers livrés

**15 balises canoniques.** Chaque page porte désormais sa canonique en version sans `.html`, placée juste après la balise viewport. La page `blog-roi-customer-marketing` avait déjà la sienne, elle est conservée à l'identique.

| Page | Canonique |
|---|---|
| index.html | https://temonis.com/ |
| blog.html | https://temonis.com/blog |
| faq.html | https://temonis.com/faq |
| guide-temoignage-client-b2b.html | https://temonis.com/guide-temoignage-client-b2b |
| guide-telecharger.html | https://temonis.com/guide-telecharger |
| mentions-legales.html | https://temonis.com/mentions-legales |
| confidentialite.html | https://temonis.com/confidentialite |
| les 8 articles de blog | https://temonis.com/{slug} |

**Indexation cohérente.**

- `guide-telecharger.html` reçoit `<meta name="robots" content="noindex, follow" />`. C'est la page de remerciement post-téléchargement, elle n'a rien à faire dans l'index. Elle est déjà absente du sitemap, les deux signaux concordent.
- `mentions-legales.html` et `confidentialite.html` perdent leur `noindex`. Elles étaient listées dans le sitemap tout en étant marquées noindex, deux signaux contradictoires. Ces pages renforcent la crédibilité du domaine, autant les laisser indexables.

**63 liens internes normalisés.** Tous les `href` vers des pages internes passent de `page.html` à `/page`. Plus aucune redirection 301 déclenchée par un clic depuis le site.

**sitemap.xml.** Les 14 `lastmod` passent au 2026-08-03 pour signaler la mise à jour à Google. Les URL étaient déjà correctes.

## À faire à la main dans le dépôt

**Supprimer `confidentialite-4a35bc42.html`.** Ce fichier est un doublon de la politique de confidentialité, accessible publiquement, absent du sitemap et des redirections. Sur GitHub : ouvrir le fichier, menu `...` en haut à droite, `Delete file`, puis commit.

## À faire dans la Search Console après déploiement

1. Envoyer à nouveau le sitemap (`https://temonis.com/sitemap.xml`) pour déclencher un recrawl.
2. Utiliser l'inspection d'URL sur la page d'accueil et sur `/blog-acheteurs-b2b-case-studies`, puis demander l'indexation. Les titres de cette page ont changé (79 % au lieu de 97 %).
3. Surveiller le rapport Indexation dans deux à trois semaines. L'alerte « Page en double sans URL canonique » doit disparaître.
