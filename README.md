# nsi.xyz — archive statique de la v2

Export statique du WordPress `nsi.xyz` (v2, 2021-2026), déployé sur **Cloudflare Pages**
(projet `nsi-xyz`). Le site est figé : il conserve les URL d'origine.

- `/` : page d'attente (`noindex`) du futur portail ;
- `/v2/` : accueil de l'archive ;
- `/plan/` : plan du site ;
- articles : `/projets/`, `/tutoriels/`, `/art/`, `/numapps/`, `/ds/`, `/decouvrir/`.

## Médias non versionnés

`wp-content/uploads/` (13 236 fichiers, 1,98 Go) et `local/cache-vignettes/` sont
**exclus de Git** : ils proviennent de `sauvegarde SSH/` et `www.nsi.xyz-static/`
(sauvegardes de référence en lecture seule). L'optimisation WebP prévue
(2,1 Go → ~0,6 Go) permettra de les intégrer ensuite.

## Déploiement

Voir `deployer.sh` (dans `outils/export_propre/` du dossier de travail) :

```bash
wrangler pages deploy . --project-name nsi-xyz --branch main
```

Wrangler doit être lancé **depuis la racine** de ce dossier pour trouver `functions/`.
Node ≥ 22 requis. `functions/_middleware.js` rejoue les anciennes URL WordPress
(`?p=`, `?cat=`, `?tag=`, `?author=`…).

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
