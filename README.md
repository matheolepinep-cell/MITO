# MITO 🎭

Jeu de société multijoueur basé sur le bluff, la déduction et la prise de parole.  
Chaque manche, un rôle secret : **vérité** ou **mensonge**. À toi de ne pas te faire griller.

---

## Stack technique

| Couche | Techno |
|--------|--------|
| Frontend | HTML / CSS / JS vanille (single file) |
| Base de données | Supabase (PostgreSQL + Realtime) |
| Hébergement | Vercel |

---

## Structure du repo

```
/
├── index.html        # App complète (frontend)
├── schema.sql        # Schéma Supabase (tables, RLS, realtime)
├── questions.sql     # Les 70 questions du jeu
└── README.md
```

---

## Installation

### 1. Supabase

1. Crée un projet sur [supabase.com](https://supabase.com)
2. Va dans **SQL Editor**
3. Exécute `schema.sql` (tables + policies + realtime)
4. Exécute `questions.sql` (insère les 70 questions)
5. Récupère ton **URL** et ta **clé anon** dans *Project Settings → API*

### 2. Configuration

Dans `index.html`, remplace les deux lignes en haut du bloc `<script>` :

```js
const SUPABASE_URL = 'https://TON-PROJET.supabase.co';
const SUPABASE_KEY = 'ta-cle-anon-publique';
```

### 3. Déploiement Vercel

1. Push le repo sur GitHub
2. Importe le projet sur [vercel.com](https://vercel.com)
3. Aucune configuration requise — Vercel détecte le fichier statique automatiquement

---

## Comment jouer

1. **Un joueur crée la partie** → choisit le nombre de manches (3, 5 ou 7) et le nombre de menteurs
2. **Les autres rejoignent** avec le code à 4 chiffres affiché
3. **Chaque manche :**
   - Chaque joueur reçoit secrètement son rôle (vérité ou mensonge)
   - Une question s'affiche — tout le monde répond à voix haute
   - Discussion libre, puis chacun vote pour celui qu'il suspecte
   - Révélation des rôles + calcul des points
4. **Fin de partie :** podium des meilleurs détecteurs (et meilleurs menteurs)

### Système de points

| Situation | Points |
|-----------|--------|
| Menteur non détecté par la majorité | +2 |
| Joueur vérité qui vote pour un vrai menteur | +1 |

---

## Design

- Fond `#0F0F0F`, accent `#FF3B3B`
- Typographies : **Sora** (titres) + **Inter** (texte)
- Mobile-first, optimisé pour les petits écrans

---

## Limitations MVP

- Pas de reconnexion automatique si on quitte l'app en cours de partie
- Le polling se fait toutes les 2 secondes (pas de WebSocket natif)
- Les questions ne se répètent pas dans une même partie mais la table `used` n'est pas encore mise à jour entre parties

---

## Roadmap

- [ ] Marquage des questions utilisées pour éviter les répétitions inter-parties  
- [ ] Reconnexion automatique (localStorage du player ID)  
- [ ] Animations de transition entre les écrans  
- [ ] Mode spectateur  
- [ ] Son / vibration sur les événements clés
