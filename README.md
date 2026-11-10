# Vers du jour

**Un poème ou une strophe de poésie française du XIXe siècle chaque jour**, sur iPhone et Mac.

Site statique et PWA, sans Lovable, sans serveur, sans dépendances à installer et sans frais d'hébergement sur GitHub Pages (pour un dépôt public).

## Déploiement (GitHub Pages + GitHub Actions)

1. Le dépôt `vers-du-jour` est déjà créé. Pour l’hébergement gratuit, passez sa visibilité à **Public** dans **Settings → General → Danger Zone → Change repository visibility**.
2. Décompressez `vers-du-jour-github.zip` sur votre ordinateur.
3. Sur la page du dépôt vide, cliquez sur **uploading an existing file** et transférez **les fichiers contenus dans le dossier**, pas le dossier parent ni le ZIP. Attention : l'interface Web GitHub peut ne pas transférer les fichiers cachés (`.github/workflows/deploy.yml`, `.nojekyll`, `.gitignore`). **La méthode Terminal ci-dessous est recommandée** pour garantir la présence du workflow.
4. Dans le dépôt, ouvrez **Settings → Pages → Build and deployment → Source**, sélectionnez **GitHub Actions**.
5. Un `push` vers `main` lance le workflow. Vous pouvez le lancer manuellement dans **Actions → Publier Vers du jour sur GitHub Pages → Run workflow**.
6. Votre URL sera `https://VOTRE_IDENTIFIANT.github.io/vers-du-jour/` (ou l'adresse indiquée dans **Settings → Pages**).

### Méthode Terminal (Mac, recommandée)

Dans le Terminal, placez-vous dans le dossier décompressé `vers-du-jour-github` :

```bash
cd /chemin/vers-du-jour-github
git init
git branch -M main
git add .
git commit -m "Initialiser Vers du jour pour GitHub Pages"
git remote add origin https://github.com/VOTRE_IDENTIFIANT/vers-du-jour.git
git push -u origin main
```

Remplacez `VOTRE_IDENTIFIANT` par votre identifiant GitHub. L'authentification GitHub utilise normalement Git Credential Manager ou un jeton personnel, et non le mot de passe du compte GitHub. Vous pouvez également utiliser GitHub Desktop pour publier tout le dossier, y compris `.github`.

**Important :** l'intégration GitHub Actions doit être autorisée dans les paramètres du dépôt. Si le dépôt a une branche par défaut autre que `main`, adaptez le nom dans le workflow.

## Installation

- **iPhone :** ouvrez l'URL avec **Safari**, puis **Partager → Sur l'écran d'accueil → Ajouter**.
- **Mac :** dans Safari, utilisez **Fichier → Ajouter au Dock** (macOS Sonoma et versions ultérieures). Sinon, ouvrez l'URL depuis un favori dans le navigateur.

## Contenu et limites

- 20 extraits pour 10 auteurs, ordonnés par date. Le cycle revient tous les 20 jours : cette première version ne contient pas 365 textes distincts.
- Changement selon la date locale, sans serveur ni tâche programmée.
- Archives et favoris, avec stockage local sur chaque appareil (non synchronisé entre Mac et iPhone).
- Les textes sont consultables hors connexion après une première ouverture en ligne, sous réserve du cache de l'appareil.
- Pas de notification push quotidienne dans cette version.
- Liens vers les éditions anciennes en bas des poèmes.

## Mise à jour

Modifiez le fichier `index.html` (tableau `poems`) puis poussez vers `main`. GitHub Actions republie le site automatiquement. Le service worker utilise une stratégie de revalidation pour la page d'accueil afin de prendre en compte les mises à jour lors d'une connexion.

## Structure

```text
.github/workflows/deploy.yml  Déploiement automatique
index.html                   Application et corpus
manifest.webmanifest         Informations d'installation
sw.js                        Lecture hors connexion
icon-*.png / icon.svg        Icônes
.nojekyll                    Désactive Jekyll
```