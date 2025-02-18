# SnapFile - Gestion de Fichiers Base64 avec Versions

SnapFile est une application web qui permet de gérer des fichiers de manière locale dans le navigateur. Elle est idéale pour stocker, sauvegarder et versionner des fichiers. Utilisant IndexedDB pour le stockage, cette application est disponible hors ligne et vous permet une gestion avancée de vos fichiers.

---

## 📖 Fonctionnalités

### 1. **Ajout de fichiers**
- Glissez-déposez vos fichiers vers l'interface (zone de dépôt).
- Chaque fichier est converti en Base64.
- L'application permet de regrouper les fichiers selon leur nom, et de leur assigner plusieurs versions (_versioning_).

### 2. **Versionnage des fichiers**
- Chaque fichier ajouté est automatiquement stocké comme une nouvelle "version".
- Les anciennes versions d'un fichier sont conservées pour consultation ou téléchargement ultérieur.
- Gestion des versions via une interface modale :
    - Télécharger une version spécifique.
    - Supprimer une version précise d'un fichier.

### 3. **Téléchargement et suppression**
- Téléchargez les fichiers stockés dans leur format d'origine à n'importe quel moment.
- Supprimez une version spécifique ou l'ensemble d'un groupe de fichiers avec un seul clic.

### 4. **Sauvegarde et restauration**
- **Sauvegarde :** Exportez l'ensemble des fichiers enregistrés sous forme d'un fichier `.json`.
- **Restauration :** Importez un fichier `.json` pour restaurer tous les fichiers et leurs versions dans l'application.

### 5. **Modal de gestion des versions**
- Afficher les détails d'une version : taille, date d'ajout, etc.
- Cliquez en dehors de la modale ou sur le bouton "Fermer" pour quitter.

---

## 🛠️ Technologies utilisées

- **Frontend :**
  - HTML
  - CSS
  - JavaScript

- **Backend (local) :**
  - **IndexedDB** : Stockage des fichiers et métadonnées (versions, tailles, etc.).

---

## 🚀 Comment utiliser SnapFile ?

### Usage basique
1. Téléchargez ou clonez le projet.
2. Ouvrez le fichier `SnapFile.html` dans votre navigateur.
3. Interagissez avec l'interface utilisateur pour :
   - Glissez-déposez des fichiers sur la zone de dépôt pour les ajouter.
   - Utilisez les boutons "Sauvegarder" et "Restaurer" pour la gestion des fichiers.
   - Cliquez sur "Voir les versions" pour consulter ou télécharger des versions spécifiques.

### Détails des fonctionnalités :
#### **Ajout de fichiers**
Lorsque vous déposez un fichier dans la zone de dépôt (DIV `#dropZone`), voici ce qui se passe :
- Le fichier est lu et converti au format Base64 à l'aide de l'API `FileReader`.
- Une version unique est générée. Si un fichier avec le même nom existe déjà, il sera ajouté au même groupe avec une nouvelle version.
- Les fichiers sont stockés dans un groupement (`groupName`) pour permettre un versionnage facile.

#### **Gestion des versions**
- Sélectionnez un groupe de fichiers, puis cliquez sur "Voir les versions".
- Une modale s'ouvre avec toutes les versions disponibles.
- Depuis cette modale, vous pouvez :
  - Télécharger une version particulière sous son format original.
  - Supprimer une version spécifique.
  - Si toutes les versions d'un fichier sont supprimées, le groupe est également supprimé.

#### **Sauvegarde et restauration**
- Lorsque vous cliquez sur le bouton "Sauvegarder", tous les fichiers et leurs métadonnées (nom de groupe, versions, timestamps) sont exportés au format JSON.
- Pour restaurer, utilisez le bouton "Restaurer" et choisissez un fichier de sauvegarde `.json`. L'application :
  - Supprime tous les fichiers existants enregistrés dans IndexedDB.
  - Recharge les fichiers et données à partir de la sauvegarde.

---

## 🎨 Interface utilisateur

### Layout principal
- **Zone de dépôt des fichiers :** Une grande zone de texte où vous pouvez glisser-déposer vos fichiers.
- **Liste des fichiers :** Une liste des fichiers sauvegardés, regroupés par leur nom. Chaque groupe correspond à un fichier avec différentes versions.
  - Boutons pour afficher les versions ou supprimer un groupe entier.

### Modal (gestion des versions)
- Liste des versions disponibles d'un fichier.
- Actions accessibles sur chaque version : Télécharger ou Supprimer.

---

## ⚙️ Fonctionnement technique

### Architecture des données
- **IndexedDB** est utilisé comme base de données locale dans le navigateur. 
- Les données sont organisées comme suit :
  - `groupName`: Nom du fichier (groupement de versions).
  - `versions`: Liste de versions contenant :
    - `versionId`: Identifiant unique pour chaque version.
    - `base64`: Contenu du fichier en Base64.
    - `timestamp`: Date et heure d'ajout de cette version.
    - `size`: Taille du fichier.
    - `originalName`: Nom original du fichier.
    - `type`: Type MIME du fichier.

### Interaction avec IndexedDB
- **Ajout/modification :**
  - Chaque groupe est une entrée dans la base de données avec un `groupName` comme clé unique.
- **Lecture :**
  - Récupération de tous les groupes ou d'un groupe spécifique pour afficher son contenu.
- **Suppression :**
  - Suppression d'une version ou d'un groupe entier.

---

## 📦 Installation et déploiement

1. Clonez ce dépôt :
   ```bash
   git clone https://github.com/<votre-utilisateur>/snapfile.git
