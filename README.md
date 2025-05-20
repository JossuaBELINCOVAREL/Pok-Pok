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
