# Guide de Développement de Plugins MG Tools

Ce dépôt (`plugin-lib`) héberge les plugins communautaires et officiels pour MG Tools.

## Structure du Dépôt

Chaque plugin doit avoir son propre dossier à la racine de cette branche :

```
plugin-lib/
├── deluge/
│   ├── manifest.json
│   └── deluge.js
├── un-autre-plugin/
│   ├── manifest.json
│   └── index.js
└── README.md
```

## Créer un Plugin

### 1. Structure du Manifest (`manifest.json`)

Le fichier `manifest.json` est obligatoire et doit contenir :

```json
{
  "id": "mon-plugin",
  "name": "Mon Plugin",
  "version": "1.0.0",
  "description": "Description courte",
  "author": "Votre Nom",
  "minAppVersion": "0.1.0"
}
```

### 2. Développement (TypeScript/React)

Les plugins sont développés en React. Ils doivent exporter une définition de plugin conforme à l'interface `PluginDefinition`.

Exemple d'entrée (`index.ts`) :

```typescript
import { PluginDefinition } from '../../types/plugin';
// ... imports

export const MonPlugin: PluginDefinition = {
  manifest: { ... },
  routes: [ ... ],
  sidebarItems: [ ... ],
  settings: { ... },
  services: [ ... ]
};
```

### 3. Compilation

Le plugin doit être compilé en un seul fichier JavaScript (UMD ou IIFE) qui exporte la définition du plugin globalement.

Commande de build recommandée (Vite) :
```bash
vite build -c vite.plugin.config.ts
```

### 4. Publication

Pour publier un plugin :
1. Créez un dossier avec l'ID de votre plugin.
2. Placez-y votre `manifest.json` et votre fichier compilé `.js`.
3. Créez une Pull Request sur cette branche `plugin-lib`.
