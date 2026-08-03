# Palette Sauge, ce qui a changé

## Variables (identiques dans les 16 pages)

| Variable | Avant | Après | Rôle |
|---|---|---|---|
| `--navy` | #0F2744 | **#33372F** | encre des titres et du texte fort |
| `--navy-2` | #0A1C33 | **#262A22** | encre appuyée |
| `--navy-soft` | #1C3A5E | **#4A5044** | encre secondaire |
| `--gold` | #C8A96A | **#6B8A6E** | accent sauge décoratif |
| `--gold-deep` | #B5934C | **#4A6B4E** | boutons, liens, chiffres clés |
| `--gold-hover` | (nouveau) | **#3D5A41** | survol des boutons |
| `--gold-soft` | #EFE6D2 | **#EDF2EC** | fonds de badges et bandeaux |
| `--gold-border` | (nouveau) | **#C9D8C9** | bordure des zones teintées |
| `--bg` | #F7F5F0 | **#FAFAF8** | fond de page |
| `--bg-alt` | (nouveau) | **#F1F3EE** | bandes alternées, pied de page |
| `--text` | #1A1A1A | **#33372F** | texte courant |
| `--muted` | #4A5568 | **#666D62** | texte secondaire |
| `--line` | #E4E0D6 | **#E5E7E0** | filets |
| `--line-strong` | (nouveau) | **#D6DAD1** | bordures de boutons secondaires |

Aucune valeur bleue ni noire ne subsiste dans le CSS.

## Blocs sombres passés en clair

Un bloc `<style id="palette-sauge">` est ajouté juste avant `</body>` dans chaque page. Il surcharge les sections qui étaient en navy plein.

| Élément | Avant | Après |
|---|---|---|
| Nav au scroll | navy 96 % | blanc 94 % + filet bas |
| Hero home | photo + voile navy | fond clair, photo à 10 % en niveaux de gris |
| Heros blog, FAQ, légal, article | navy plein | fond clair, titres encre |
| Bandeau intégrations | navy foncé | vert très pâle |
| Section fonctionnalités `.dark` | navy plein | gris vert pâle, cartes blanches |
| Carte tarif mise en avant | navy plein | blanche, bordure sauge 2 px |
| Encart CTA | dégradé doré animé | vert pâle, bordure, animation retirée |
| Pied de page | navy plein | gris vert pâle, filet haut |
| Barre CTA collante | navy | blanc 96 % + filet haut |
| Bouton primaire | doré, texte navy | sauge foncé, texte blanc |
| Bouton `btn-navy` et `btn-dl` | navy plein | blanc bordé, survol vert pâle |
| Chatbot Temo | navy | sauge foncé, texte blanc |
| Vignettes blog `.pc-1/2/3` | dégradés navy et or | dégradés vert pâle |

## Contrastes vérifiés (WCAG)

| Paire | Ratio | Niveau |
|---|---|---|
| Texte #33372F sur fond #FAFAF8 | 11,63:1 | AAA |
| Texte #33372F sur blanc | 12,15:1 | AAA |
| Secondaire #666D62 sur #FAFAF8 | 5,11:1 | AA |
| Secondaire #666D62 sur #F1F3EE | 4,78:1 | AA |
| Sauge #4A6B4E sur blanc | 5,99:1 | AA |
| Blanc sur sauge #4A6B4E | 5,99:1 | AA |

## Assets régénérés

`favicon.svg`, `favicon-32x32.png`, `favicon-192x192.png`, `apple-touch-icon.png` sont redessinés à l'identique de la géométrie d'origine, seule la couleur change.

`og-image.png` n'est pas redessinée : l'image d'origine est recolorée pixel par pixel. La typographie Plus Jakarta Sans du visuel est donc conservée telle quelle. Le carton navy devient blanc bordé, le texte blanc devient encre, l'or devient sauge.

Le logo inline dans la nav et le pied de page est repassé en sauge dans le HTML.

`hero-bg.jpg` est conservé mais affiché à 10 % en niveaux de gris. Pour supprimer complètement la photo, remplacer dans le bloc `palette-sauge` la ligne `.hero-bg{opacity:.10;filter:grayscale(1);}` par `.hero-bg{display:none;}`.

## Pour revenir en arrière

Supprimer le bloc `<style id="palette-sauge">` et remettre l'ancien `:root`. Les deux modifications sont isolées et repérables.
