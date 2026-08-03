# Audit et uniformisation du site

## Les deux anomalies signalées

**Barre de navigation transparente sur certaines pages.** La barre était configurée en `background: transparent`, et ne devenait blanche qu'après ajout de la classe `scrolled` par un script au défilement. Or ce script n'existe que sur la page d'accueil. Les articles de blog compensaient en écrivant la classe en dur dans le HTML. Restaient six pages sans script ni classe : blog, centre d'aide, mentions légales, confidentialité, notre approche et la page de téléchargement. Leur barre restait transparente en permanence, laissant voir le contenu défiler derrière.

Correctif : la barre est désormais opaque sur toutes les pages, sans dépendance à JavaScript. Fond blanc à 94 %, flou d'arrière-plan, filet bas. Le comportement est identique partout, y compris sur la page d'accueil qui perd son effet transparent en haut de page.

**Pieds de page différents.** Quatre variantes coexistaient : la version complète de la page d'accueil, une version réduite sur les articles, une version encore plus courte sur les pages légales, et une version minimale sur la page de téléchargement.

Correctif : un pied de page unique sur 15 pages, celui de la page d'accueil. La page `guide-telecharger` conserve volontairement son pied de page minimal, c'est une page de conversion sur laquelle on limite les sorties.

## Uniformisation

| Élément | État |
|---|---|
| Barre de navigation | 1 seule version sur 15 pages, plus la version réduite de la landing page |
| Pied de page | 1 seule version sur 15 pages, plus la version réduite de la landing page |
| Libellés du menu | Fonctionnement, Automatisation, Tarifs, Ressources, Notre approche, Centre d'aide |
| Bouton de démo | ouvre le formulaire en modale sur les 15 pages |
| Menu burger | fonctionnel sur toutes les pages, bascule sous 1080 px |

Les pages blog, mentions légales et confidentialité ont reçu la modale de démonstration, qui leur manquait. Leur bouton « Demander une démo » renvoyait vers la page d'accueil.

## Contrôles automatiques passés

- **Liens internes : 0 cassé.** Les 15 pages ont été analysées, chaque `href` interne a été résolu vers un fichier existant, et chaque ancre vérifiée comme présente dans la page cible.
- **Aucun identifiant HTML dupliqué.**
- **Tous les scripts inline valides** (contrôle syntaxique Node sur chaque bloc de chaque page).
- **Tous les blocs JSON-LD valides.**
- **Balises équilibrées** sur `style`, `nav`, `footer`, `body`.
- **Canonique et titre uniques** présents sur chaque page.

## Point d'attention pour la suite

Le site est un ensemble de fichiers HTML autonomes, chacun embarquant sa propre copie de la barre de navigation, du pied de page et des styles. Toute modification de l'un de ces éléments communs doit être répercutée sur les 15 pages, sinon les écarts réapparaissent. C'est l'origine des deux anomalies corrigées ici.
