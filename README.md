# 📘 Cahier des Charges - Application Web Poker Elo

## 🎯 Objectif Général
Créer une application web de poker multijoueur **sans argent réel**, reposant sur un **système de classement Elo** à la manière de chess.com. L’objectif est de proposer une expérience compétitive, ludique et éthique, orientée sur la progression et l’analyse des performances.

---

## 📌 Étape 1 – MVP : Prototype Jouable Solo (PoC)

### 🧪 Objectif
Créer une version minimale pour **tester la jouabilité** d’une partie de Poker (Texas Hold’em) en solo contre des bots.

### ✅ Fonctionnalités Clés
- [x] Variante : **Texas Hold'em No Limit**
- [x] Interface web simple (React ou équivalent)
- [x] Affichage :
  - Cartes visibles (joueur + table)
  - Stack, pot, mise actuelle
- [x] Actions disponibles :
  - Fold / Check / Call / Raise
- [x] Adversaires bots simples (logique basique)
- [x] Aucune connexion requise
- [x] Aucune persistance (état en mémoire uniquement)
- [x] Partie 1v1 (joueur vs bot)

### 💻 Stack Technique Suggestée (PoC)
- **Frontend** : React + TailwindCSS
- **Backend** : Node.js ou mock JSON local
- **État** : Zustand, Redux ou state React local
- **Déploiement** : Vercel / Netlify

### 🧠 Points à valider
- Jouabilité et clarté de l’UI
- Logique de tour et gestion du pot
- Première couche d'abstraction du moteur de jeu (deck, mise, showdown)

---

## 📌 Étape 2 – Intégration du Classement Elo

### 🧪 Objectif
Introduire la **dimension compétitive** avec des comptes utilisateurs et un **système de classement Elo** mis à jour à chaque partie.

### ✅ Fonctionnalités Clés
- [x] Création de compte :
  - Login via email ou Google (OAuth)
- [x] Système de classement Elo :
  - Initialisation à 1200
  - Ajustement Elo après chaque match (1v1)
- [x] Historique des parties :
  - Résultat, date, Elo gagné/perdu
- [x] Leaderboard public :
  - Top 100 joueurs, filtre par pseudo
- [x] Matchmaking simple :
  - Joueur vs joueur avec ±100 Elo

### 🔢 Règles de Calcul Elo (proposition)
```text
Elo_new = Elo_current + K * (Result - Expected)

Expected = 1 / (1 + 10^((Elo_opponent - Elo_current)/400))
Result = 1 si victoire, 0 en cas de défaite
K = 32 par défaut, ajustable selon le nombre de parties
```

### 💾 Stack Technique Évoluée
- **Frontend** : React + Next.js
- **Backend** : Node.js + Express
- **DB** : PostgreSQL (joueurs, parties, Elo)
- **Auth** : Supabase Auth / Clerk / Auth0
- **Déploiement** : Railway / Vercel
- **CI/CD** : GitHub Actions

---

## 📌 Étape 3 – Version Multijoueur Live

### 🧪 Objectif
Créer un système **temps réel multijoueur**, où les joueurs s’affrontent autour de tables virtuelles, avec calcul Elo adapté.

### ✅ Fonctionnalités Clés
- [x] Tables de 2 à 6 joueurs
- [x] WebSockets pour synchronisation temps réel :
  - Affichage des cartes communautaires en temps réel
  - Actions visibles en direct par tous les joueurs
- [x] Matchmaking automatisé :
  - File d’attente et affectation à table
- [x] Timer de tour (ex : 30s)
- [x] Elo adapté au format multi-joueur :
  - Classement relatif selon la position finale
  - Bonus pour top 3, malus pour élimination rapide
- [x] Parties privées :
  - Lien d’invitation, code d’accès

### 💬 Optionnel
- Chat en jeu (temporaire ou persistant)
- Système de signalement
- Saisons compétitives

### 🔐 Anti-triche (v1)
- Détection de multi-comptes basique
- Blocage double connexion
- Limitation d’IP pour les parties privées

### ⚙️ Stack Complète Multijoueur
- **Frontend** : React + Zustand (gestion des états complexes)
- **Backend** : Node.js avec Socket.IO
- **DB** : PostgreSQL + Redis pour état live
- **Infra** : Docker, Railway, Render ou VPS
- **Monitoring** : Sentry + Logtail / Prometheus + Grafana

---

## 🔧 DevOps & CI/CD (à partir de l’étape 2)

| Besoin                        | Outil Recommandé         |
|-----------------------------|--------------------------|
| CI/CD                        | GitHub Actions           |
| Monitoring erreurs           | Sentry                   |
| Logs backend                 | Logtail / Datadog        |
| Observabilité / métriques    | Prometheus + Grafana     |
| Environnements isolés        | `.env`, staging/prod     |
| Authentification sécurisée   | JWT ou Supabase Auth     |
| Tests unitaires              | Vitest / Jest            |

---

## 📈 Évolutions possibles (non incluses)
- Revoir Elo avec Glicko-2
- Mode tournois SNG (Sit & Go)
- Coaching ou replays de mains
- Analyse de tendance (ex : % de fold, bluff, etc.)

---

## ✅ Livrables Attendus par Étape

### Étape 1 (PoC Jouabilité)
- Moteur de jeu fonctionnel (solo vs bot)
- Interface complète avec toutes les actions
- Partie auto-resettable après un gagnant

### Étape 2 (Classement Elo)
- Compte joueur
- Matchmaking 1v1 + Elo dynamique
- Historique et classement

### Étape 3 (Multijoueur Live)
- Tables de 2 à 6 joueurs en temps réel
- Mise à jour des états via WebSockets
- Gestion Elo multijoueur

---

## 📂 Annexes Techniques
- Schéma de DB (à venir)
- Diagramme d’architecture (à venir)
- Wireframes UI (à définir)
- Spécifications d’API REST / WebSocket (à définir)

---

> Rédigé par : [Joko]
