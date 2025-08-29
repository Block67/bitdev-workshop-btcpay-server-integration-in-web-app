# Vue 3 + Vite + Tailwind CSS v4

Ce template vous aide à démarrer le développement avec Vue 3, Vite et Tailwind CSS v4. Le template utilise Vue 3 `<script setup>` SFCs, consultez cette [page](https://dev.to/osalumense/install-tailwind-css-v4-in-a-vue-3-vite-project-319g) pour en savoir plus.

## 🚀 Fonctionnalités

- **Vue 3** - Framework JavaScript progressif
- **Vite** - Outil de build ultra-rapide
- **Tailwind CSS v4** - Framework CSS utility-first avec les dernières améliorations

## 🆕 Nouveautés de Tailwind CSS v4

- **Pas de configuration PostCSS requise** – Plus besoin de `postcss.config.js`
- **Temps de construction plus rapides** – Grâce à de meilleures optimisations
- **Nouveau plugin `@tailwindcss/vite`** – Intégration transparente avec Vite

## 📦 Installation

### Créer le projet
```bash
npm create vite@latest my-vue-app -- --template vue
cd my-vue-app
npm install
```

### Installer Tailwind CSS v4
```bash
npm install -D tailwindcss @tailwindcss/vite
```

### Configuration Vite
Modifiez `vite.config.ts` (ou `vite.config.js`) :

```javascript
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import tailwindcss from '@tailwindcss/vite'

export default defineConfig({
  plugins: [
    vue(),
    tailwindcss(),
  ],
})
```

### Ajouter Tailwind aux styles
Dans `src/style.css`, ajoutez :

```css
@import 'tailwindcss';
```

### Vérifier l'import dans main.ts
Assurez-vous que `src/main.ts` importe le CSS :

```javascript
import { createApp } from 'vue'
import App from './App.vue'
import './style.css'

createApp(App).mount('#app')
```

## 🏃‍♂️ Démarrage

```bash
npm run dev
```

## 💡 Pourquoi Vue 3 + Vite ?

- **Performance optimale** : Vue 3 est léger sans les surcharges additionnelles
- **Contrôle total** : Vous décidez de l'architecture de votre application
- **Simplicité** : Idéal pour les SPA sans besoin de SSR/SSG
- **Builds rapides** : Vite offre un développement et déploiement ultra-rapides

## 📚 Ressources

En savoir plus sur le support IDE pour Vue dans le [Guide Vue Docs Scaling up](https://vuejs.org/guide/scaling-up/tooling.html#ide-support).

## 🎨 Utilisation de Tailwind

Vous pouvez maintenant utiliser les classes Tailwind directement dans vos composants Vue :

```vue
<template>
  <div class="bg-blue-500 text-white p-4 rounded-lg">
    <h1 class="text-2xl font-bold">Hello Tailwind CSS v4!</h1>
  </div>
</template>
```