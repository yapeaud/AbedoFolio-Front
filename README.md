# Frontend

Template de frontend en **React 19** et **TypeScript**, propulsé par **Vite** et stylé avec **Tailwind CSS 4**.

## Stack

| Outil | Rôle |
| --- | --- |
| [React 19](https://react.dev/) | Bibliothèque d'interface utilisateur |
| [TypeScript](https://www.typescriptlang.org/) | Typage statique |
| [Vite](https://vite.dev/) | Serveur de développement (rechargement instantané) et build de production |
| [Tailwind CSS 4](https://tailwindcss.com/) | Styles par classes utilitaires, intégré via le plugin `@tailwindcss/vite` |
| [ESLint](https://eslint.org/) | Analyse du code (règles TypeScript, React Hooks et React Refresh) |

Le projet est configuré en **ES Modules** (`"type": "module"` dans `package.json`).

## Prérequis

- [Node.js](https://nodejs.org/) (version LTS récente recommandée)
- npm (fourni avec Node.js)

## Installation

```bash
cd frontend
npm install
```

## Configuration

Les variables d'environnement sont lues par Vite depuis les fichiers `.env` à la racine de `frontend/`.

1. Copiez le fichier d'exemple :

   ```bash
   cp .env.example .env
   ```

2. Renseignez les valeurs dans `.env`.

Seules les variables préfixées par `VITE_` sont accessibles dans le code, via `import.meta.env` :

```env
VITE_API_URL=http://localhost:3000
```

```ts
const apiUrl = import.meta.env.VITE_API_URL;
```

> Les variables `VITE_*` sont intégrées en clair dans le code envoyé au navigateur : n'y mettez jamais de secret (clé privée, mot de passe…). Pour des valeurs propres à votre poste, utilisez `.env.local`, qui n'est pas commité. Documentez chaque nouvelle variable dans `.env.example`.

## Scripts

| Commande | Description |
| --- | --- |
| `npm run dev` | Démarre le serveur de développement sur `http://localhost:5173` |
| `npm run build` | Vérifie les types (`tsc -b`) puis génère le build de production dans `dist/` |
| `npm run preview` | Sert localement le contenu de `dist/` pour tester le build |
| `npm run lint` | Analyse le code avec ESLint |

## Tailwind CSS

Tailwind est importé une seule fois dans [`src/index.css`](src/index.css) :

```css
@import "tailwindcss";
```

Aucun fichier `tailwind.config.js` n'est nécessaire avec la version 4 : les classes s'utilisent directement dans le JSX.

```tsx
<h1 className="text-4xl font-bold text-amber-600">Bonjour !</h1>
```

La personnalisation (couleurs, polices…) se fait en CSS avec la directive `@theme`.

## Structure du projet

```text
frontend/
├── public/              # Fichiers statiques servis tels quels (favicon…)
├── src/
│   ├── @types/          # Déclarations de types globales
│   ├── api/             # Appels HTTP vers le backend
│   ├── assets/          # Images et ressources importées dans le code
│   ├── components/      # Composants réutilisables
│   ├── hooks/           # Hooks React personnalisés
│   ├── pages/           # Composants correspondant aux pages de l'application
│   ├── routes/          # Définition des routes
│   ├── templates/       # Mises en page communes (en-tête, pied de page…)
│   ├── themes/          # Thème visuel (couleurs, typographie…)
│   ├── utils/           # Fonctions utilitaires
│   ├── validators/      # Validation des formulaires et des données
│   ├── App.tsx          # Composant racine
│   ├── index.css        # Styles globaux et import de Tailwind
│   └── main.tsx         # Point d'entrée : monte <App /> dans index.html
├── .env                 # Variables d'environnement
├── .env.example         # Modèle des variables d'environnement
├── eslint.config.js     # Configuration ESLint
├── index.html           # Page HTML de base
├── package.json
├── tsconfig.json        # Configuration TypeScript (références app et node)
├── tsconfig.app.json    # Configuration TypeScript du code de src/
├── tsconfig.node.json   # Configuration TypeScript des fichiers d'outillage (vite.config.ts)
├── vite.config.ts       # Configuration Vite (plugins React et Tailwind)
└── README.md
```
