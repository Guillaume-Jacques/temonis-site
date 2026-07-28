# Correction « Page en double sans URL canonique » — temonis.com

**Repo :** `Guillaume-Jacques/temonis-site` (branche `main`)
**Netlify :** projet `temonis.com`, deploys from GitHub — synchronisé, commit `7d40ddb`
**URL canonique retenue :** version **sans `.html`**

---

## Le diagnostic

Aucun de tes fichiers HTML ne contient de balise `<link rel="canonical">`. J'ai lu le
`<head>` complet de `blog-roi-customer-marketing.html` : favicons, Open Graph, JSON-LD,
Plausible — tout y est sauf la canonique.

Netlify sert automatiquement chaque page sous deux URLs, toutes deux en HTTP 200 :

```
https://temonis.com/blog-roi-customer-marketing.html   → 200
https://temonis.com/blog-roi-customer-marketing        → 200, même fichier
```

Et tu envoies trois signaux contradictoires à Google :

| Source | Forme utilisée |
|---|---|
| `sitemap.xml` | `.../blog-roi-customer-marketing.html` |
| `blog.html` (liste d'articles) | `.../blog-roi-customer-marketing` |
| « À lire aussi » + footer des articles | `blog-acheteurs-b2b-case-studies.html` (relatif) |

Sans canonique pour trancher, Google a choisi lui-même la version sans `.html` et exclu
les `.html` listées dans ton sitemap. D'où le message sur ces 5 pages.

---

## Les 3 fichiers fournis

### 1. `_redirects` — nouveau fichier

À déposer **à la racine du repo** (même niveau que `index.html`). Nom exact : `_redirects`,
sans extension, sans point devant.

C'est le correctif principal : il force une seule URL indexable par page. Le `!` après
`301` est indispensable — sans lui, Netlify sert en priorité le fichier `.html` qui existe
réellement et la règle ne se déclenche jamais.

### 2. `sitemap.xml` — remplace l'existant

Toutes les URLs passent en version sans `.html`. J'ai aussi ajouté `/mentions-legales` et
`/confidentialite` qui manquaient, et mis à jour le `lastmod` de l'article corrigé.

`guide-telecharger.html` est volontairement **absent** : si c'est bien ta page de
remerciement post-téléchargement, elle ne doit pas être indexée. Ajoute-lui plutôt
`<meta name="robots" content="noindex, follow" />` dans son `<head>`.

### 3. `blog-roi-customer-marketing.html` — remplace l'existant

Quatre corrections :

- **Texte Kapost** rétabli à la place de Gartner/Forrester (2 paragraphes + la ligne
  « Revenu additionnel » qui repasse de 90-150 k€ à 60-90 k€)
- **Balise canonique** ajoutée, plus `og:url` et `mainEntityOfPage` dans le JSON-LD
- **Liens internes** en absolu sans `.html` (`/blog-acheteurs-b2b-case-studies`,
  `/mentions-legales`, etc.)
- **Navigation** : `/#blog` → `/blog` et `/#faq` → `/faq`, puisque `blog.html` et
  `faq.html` existent désormais comme pages à part entière. Libellé « FAQ » → « Centre
  d'aide » pour coller à tes articles récents. Si tu préfères garder les ancres de la page
  d'accueil, c'est la seule modification à annuler.

---

## Ce qu'il reste à faire sur les 13 autres pages

Une seule ligne à ajouter dans le `<head>`, juste après la balise `<meta name="description">` :

```html
<link rel="canonical" href="https://temonis.com/URL-DE-LA-PAGE" />
```

| Fichier | Valeur du `href` |
|---|---|
| `index.html` | `https://temonis.com/` |
| `blog.html` | `https://temonis.com/blog` |
| `faq.html` | `https://temonis.com/faq` |
| `guide-temoignage-client-b2b.html` | `https://temonis.com/guide-temoignage-client-b2b` |
| `blog-collecter-temoignages-clients.html` | `https://temonis.com/blog-collecter-temoignages-clients` |
| `blog-exemples-temoignages-clients-b2b.html` | `https://temonis.com/blog-exemples-temoignages-clients-b2b` |
| `blog-logiciel-temoignage-client.html` | `https://temonis.com/blog-logiciel-temoignage-client` |
| `blog-automatiser-temoignages-b2b.html` | `https://temonis.com/blog-automatiser-temoignages-b2b` |
| `blog-acheteurs-b2b-case-studies.html` | `https://temonis.com/blog-acheteurs-b2b-case-studies` |
| `blog-modjo-customer-marketing.html` | `https://temonis.com/blog-modjo-customer-marketing` |
| `blog-cycles-vente-preuve-sociale.html` | `https://temonis.com/blog-cycles-vente-preuve-sociale` |
| `mentions-legales.html` | `https://temonis.com/mentions-legales` |
| `confidentialite.html` | `https://temonis.com/confidentialite` |
| `guide-telecharger.html` | *(pas de canonique — mettre `noindex`)* |

Toujours en absolu, en HTTPS, sans slash final. Ajoute la même valeur en `og:url` si la
balise est présente.

> Le `_redirects` règle déjà le problème à lui seul. Les canoniques sont une ceinture de
> sécurité : elles protègent si un lien externe pointe un jour vers une variante d'URL.
> Tu peux les ajouter tranquillement, page par page.

---

## Déposer les fichiers sur GitHub

1. Repo → bouton **Add file** → **Upload files**
2. Glisse les 3 fichiers d'un coup (les 2 existants seront écrasés, c'est voulu)
3. Message de commit : `SEO: canoniques, redirections .html, correction source Kapost`
4. **Commit changes** → Netlify déploie automatiquement en 1 à 2 minutes

---

## Vérification après déploiement

```bash
# doit répondre 301 + Location: /blog-roi-customer-marketing
curl -sI https://temonis.com/blog-roi-customer-marketing.html | head -5

# doit répondre 200
curl -sI https://temonis.com/blog-roi-customer-marketing | head -5

# doit afficher une seule balise, sans .html
curl -s https://temonis.com/blog-roi-customer-marketing | grep -i canonical

# doit afficher Kapost, pas Gartner
curl -s https://temonis.com/blog-roi-customer-marketing | grep -i kapost
```

Puis dans la Search Console :

1. **Inspection de l'URL** sur `https://temonis.com/blog-roi-customer-marketing.html`
   → doit indiquer une redirection
2. *Indexation des pages* → ligne « Page en double sans URL canonique sélectionnée par
   l'utilisateur » → **Valider la correction**
3. Renvoie ton `sitemap.xml` depuis l'onglet *Sitemaps*
4. Compte 1 à 3 semaines : Google doit re-crawler chaque URL

---

## Sur l'urgence réelle

Ces 5 pages ne sont pas pénalisées. Google les indexe correctement, il a juste choisi
l'URL de référence à ta place. Le gain ici est de la propreté technique et du contrôle,
pas un déblocage de trafic. À traiter en fond de tâche.

Le point qui mérite plus d'attention, c'est le contenu : ton dernier upload a réintroduit
une version antérieure de `blog-roi-customer-marketing.html`. Vérifie que les autres
fichiers du commit `7d40ddb` sont bien les bons avant de repartir dessus.
