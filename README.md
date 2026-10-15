# Seddo Mobilité · Maquettes V1

Prototype cliquable des trois produits Seddo (app client et mini app Max it, app chauffeur, backoffice), servi par nginx dans un conteneur Docker.

## Contenu

| Fichier | Rôle |
| --- | --- |
| `site/index.html` | Les maquettes (une seule page, sans dépendance à installer) |
| `Dockerfile` | Image nginx:1.27-alpine avec le site |
| `nginx.conf` | Compression, en-têtes de sécurité, pas de cache sur le HTML, `/healthz` |
| `docker-compose.yml` | Pour un déploiement Dokploy en mode Compose ou un test local |

## Déployer sur Dokploy

Option A, application Dockerfile (la plus simple) :

1. Poussez ce dossier dans un dépôt Git (GitHub, GitLab, Gitea) ou utilisez l'envoi de fichier « Drop » de Dokploy.
2. Dans Dokploy : Project > Create Service > Application.
3. Source : votre dépôt et la branche. Build Type : **Dockerfile**, chemin `./Dockerfile`.
4. Onglet Domains : ajoutez votre domaine (ex. `maquettes.seddo.sn`), **Container Port 80**, activez HTTPS (Let's Encrypt).
5. Deploy.

Option B, Compose : Create Service > Compose, source = ce dépôt, fichier `docker-compose.yml`, puis ajoutez le domaine sur le service `seddo-maquettes`, port 80.

## Tester en local

```bash
docker build -t seddo-maquettes .
docker run --rm -p 8080:80 seddo-maquettes
# puis ouvrir http://localhost:8080
```

## Notes

- Les polices viennent de Google Fonts : les visiteurs doivent avoir accès à internet. Sans accès, la page reste lisible avec des polices de secours.
- Les données et les montants affichés sont fictifs.
- La page n'est pas indexée par les moteurs de recherche (`noindex`). Pour la réserver à l'équipe, ajoutez une authentification basique dans Dokploy (onglet Security de l'application).
- Pour mettre à jour les maquettes : remplacez `site/index.html` et redéployez.
# seddo-vtc-maquette
