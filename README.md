# nsi.xyz — archive statique de la v2

Export statique du WordPress `nsi.xyz` (v2, 2021-2026), déployé sur **Cloudflare Pages**
(projet `nsi-xyz`), en production sur **https://nsi.xyz** depuis le 20/10/2026.
Le site est figé : il conserve les URL d'origine.

Dépôt public : **https://github.com/nsi-xyz/nsi.xyz**

- `/` : portail nsi.xyz (fichiers du dépôt `nsi-xyz/portail`) ;
- `/v2/` : accueil de l'archive ;
- `/v2/plan/` : plan du site (l’ancien `/plan/` redirige) ;
- articles : `/projets/`, `/tutoriels/`, `/art/`, `/numapps/`, `/ds/`, `/decouvrir/`.

## Médias non versionnés

`wp-content/uploads/` (13 236 fichiers, 1,98 Go) et `local/cache-vignettes/` sont
**exclus de Git** : ils proviennent de `sauvegarde SSH/` et `www.nsi.xyz-static/`
(sauvegardes de référence en lecture seule). L'optimisation WebP prévue
(2,1 Go → ~0,6 Go) permettra de les intégrer ensuite. Le dépôt public contient
donc les pages et le code de l’archive, mais pas ces médias lourds.

## Déploiement

La production combine ce dossier avec le portail. Utiliser le script du dépôt
`nsi-xyz/portail` :

```bash
portail/outils-dev/deployer.sh /chemin/vers/archive-v2 production
```

Wrangler doit être lancé **depuis le dossier de staging** pour trouver
`functions/`. Node ≥ 22 requis. `functions/_middleware.js` rejoue les anciennes
URL WordPress (`?p=`, `?cat=`, `?tag=`, `?author=`…).

## Structure technique

| Fichier | Rôle |
|---|---|
| `_redirects` | 149 redirections 301 |
| `functions/_middleware.js` | anciennes URL WordPress |
| `_routes.json` | limite le middleware aux pages HTML |
| `_headers` | en-têtes de sécurité et cache |
| `sitemap.xml`, `sitemap_index.xml`, `robots.txt` | SEO |
| `404.html` | page d'erreur |

Les rapports d'audit et le mode d'emploi détaillé sont dans
`outils/export_propre/` (hors dépôt).
