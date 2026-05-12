# Pandora Player

Page mobile (portrait) hébergée pour les joueurs de **Pandora 2026**. Affiche en temps réel le score, le rang, le classement et les messages flash pour un joueur donné, en lisant l'état du jeu depuis Firebase RTDB (`lumiia-live` → `/pandora/live`).

URL publique : **https://i-immersion.github.io/pandora-player/**

Le joueur scanne un QR code généré côté Mac (app Electron Pandora 2026), qui contient `https://i-immersion.github.io/pandora-player/?p=<N>` où `<N>` est son numéro de joueur (1 à 6).

## Stack

- HTML/CSS/JS vanilla, pas de framework, pas de build
- Firebase SDK modular v10.12 (CDN gstatic)
- Aucune authentification : le node `/pandora/live` est en lecture publique

## Architecture

```
┌─────────────────┐                       ┌────────────────────┐
│ App Pandora     │  PUT /pandora/live   │  Firebase RTDB      │
│ (Mac Electron)  │ ─────────────────────▶  lumiia-live        │
└─────────────────┘                       └─────────┬──────────┘
                                                    │ onValue
                                                    ▼
                                          ┌─────────────────────┐
                                          │ pandora-player      │
                                          │ (cette page)        │
                                          │ ?p=1..6             │
                                          └─────────────────────┘
```

## Déploiement

Push sur `main` → GitHub Pages publie automatiquement (build : `none`, source : `main / root`).

## Affichage

- Numéro et nom du joueur en haut
- Score géant à sa couleur
- Rang actuel (1er, 2e, ...) + écart au leader
- Temps restant (mode Timer/Mort subite) ou objectif (mode Course)
- Bannière d'état (En cours / Mort subite / Terminé)
- Classement complet en temps réel
- Overlay clignotant pour les messages flash envoyés depuis la régie

## URL params

| Param | Valeurs | Description |
|-------|---------|-------------|
| `p`   | 1 à 6   | Numéro du joueur (obligatoire) |

## Licence

MIT
