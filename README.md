# Denbox.net — Site Vitrine & Portfolio

Site statique personnel de **Laurent Guilbert**, vitrine pour les projets de l'écosystème Denbox :
- **SilverScreen** : [https://silverscreen.denbox.net/](https://silverscreen.denbox.net/)
- **OmniBox** : [https://omnibox.denbox.net/](https://omnibox.denbox.net/) (bientôt disponible)
- Présentation, boîte à outils et contact.

## Structure du projet

- `index.html` : Structure sémantique HTML5 complète avec métadonnées SEO/OpenGraph.
- `style.css` : Design moderne, sombre, responsive avec typographie fluide et effets néon.
- `logo.svg` : Logo vectoriel Denbox (icône et favicon).
- `CNAME` : Contient `www.denbox.net` pour le domaine personnalisé sur GitHub Pages.
- `.nojekyll` : Désactive le parsing Jekyll pour GitHub Pages.

---

## Déploiement sur GitHub Pages & Configuration DNS

### 1. Pousser le projet sur GitHub

1. Créez un nouveau dépôt public sur GitHub nommé par exemple `denbox.net` (ou `denbox`).
2. Dans ce dossier, liez le dépôt distant et poussez la branche principale :
   ```bash
   git init
   git add .
   git commit -m "Initial commit: Denbox portfolio and showcase"
   git branch -M main
   git remote add origin https://github.com/<votre-pseudo>/denbox.net.git
   git push -u origin main
   ```

### 2. Activer GitHub Pages

1. Dans votre dépôt GitHub, allez dans **Settings** > **Pages**.
2. Dans **Build and deployment** :
   - Source : **Deploy from a branch**
   - Branch : `main` / `/ (root)`
   - Cliquez sur **Save**.
3. Dans **Custom domain** :
   - Vérifiez que `www.denbox.net` est renseigné (détecté via le fichier `CNAME`).
   - Cochez **Enforce HTTPS** (dès que le certificat TLS est provisionné).

### 3. Configuration DNS (sur votre hébergeur / Cloudflare)

Pour que `www.denbox.net` et `denbox.net` pointent sur GitHub Pages :

#### Option A (Recommandée avec Cloudflare) :
- **CNAME pour `www`** :
  - Nom : `www`
  - Cible : `<votre-pseudo>.github.io`
  - Proxy : DNS only (gris) au départ pour valider le certificat GitHub Pages, ou Proxied si vous utilisez SSL Cloudflare.
- **Redirection racine `denbox.net` vers `www.denbox.net`** (ou CNAME flattening) :
  - Sur Cloudflare, créez une règle de redirection (Redirect Rule) de `https://denbox.net/*` vers `https://www.denbox.net/$1`.

#### Option B (DNS Standard avec adresses IP GitHub Pages pour l'Apex `denbox.net`) :
- **Enregistrements A** pour `@` (denbox.net) :
  - `185.199.108.153`
  - `185.199.109.153`
  - `185.199.110.153`
  - `185.199.111.153`
- **Enregistrement CNAME** pour `www` :
  - Nom : `www`
  - Cible : `<votre-pseudo>.github.io`
