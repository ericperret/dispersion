<!--
  Nom      : LISEZMOI.md
  Objet    : Présentation de la simulation de dispersion balistique et gazeuse
  Auteur   : Eric Perret
  Date     : 2026-10-27
  Version  : 6.3
-->

# Simulation de dispersion balistique et gazeuse

🇬🇧 [English version: README.md](README.md)

▶️ **[Lancer la simulation](https://ericperret.github.io/dispersion/dispersion_v62.html)** — 📖 [documentation technique](https://ericperret.github.io/dispersion/dispersion_doc.html)

> Fichier HTML unique et autonome — zéro dépendance, zéro installation, zéro serveur.

![Simulation v6.3 : ELA-4, explosion à 10 000 m, zones de retombée et barbules de vent](screenshot.jpg)

Outil de simulation de dispersion pour le **Centre Spatial Guyanais** (CSG / Kourou) et d'autres pas de tir dans le monde.
Calcule la trajectoire de retombées de débris balistiques et la diffusion atmosphérique de HCl issu des boosters. Interface en français.

## Fichiers

| Fichier | Description |
|---------|-------------|
| `dispersion_v62.html` | Application principale — ouvrir directement dans le navigateur |
| `dispersion_doc.html` | Documentation technique complète (architecture, ETS, modèles) |

## Fonctionnalités

| Module | Description |
|--------|-------------|
| **Pas de tir** | CSG (ELA-4, ELV, ELS), Floride, Vandenberg, Baïkonour, Plesetsk, Vostochny, Wenchang, Jiuquan, Xichang, Tanegashima, Sriharikota |
| **Balistique RK45** | Intégrateur Dormand-Prince adaptatif · Cd(Mach) tabulé · atmosphère ISA 7 couches · force de Coriolis |
| **Dispersion gazeuse** | Modèle Pasquill-Gifford classes A→F auto · σ Turner (1970) · seuil AEGL-1/10 HCl = 0,1 mg/m³ |
| **Météo temps réel** | Profil vertical Open-Meteo (vent, pression, humidité) — requête GET HTTPS, aucune donnée personnelle |
| **Cartographie** | Imagerie Esri World Imagery + étiquettes Esri, sans clé ni API · zones de retombée · isocontours AEGL · barbules de vent |
| **Carte tactile** | Déplacement à un doigt, zoom par pincement |
| **Web Workers** | Calculs parallèles non-bloquants |
| **Sécurité** | CSP strict · watchdog · sanity checks intégrés |

## Déploiement

Ouvrir le lien ci-dessus, ou télécharger `dispersion_v62.html` et l'ouvrir dans un navigateur moderne.
Aucune installation, aucun serveur, aucun accès administrateur requis.

Deux appels réseau sortants uniquement :

| Destination | Objet | Données transmises |
|-------------|-------|--------------------|
| `api.open-meteo.com` | Profil vent vertical | Lat/lon du point de tir uniquement |
| `server.arcgisonline.com` | Tuiles cartographiques Esri (sans clé) | Coordonnées de tuile (zoom/x/y) |

## Sécurité & audit SSI

Code source en clair — non minifié, non obfusqué. Lisible dans n'importe quel éditeur texte.

- Zéro bibliothèque externe · aucun CDN · surface d'attaque supply chain nulle
- Aucun cookie · aucun localStorage · aucune écriture disque
- Toutes les données de calcul en mémoire RAM uniquement

## Modèles physiques

- **Atmosphère** — ISA standard 7 couches
- **Intégrateur** — RK45 Dormand-Prince adaptatif
- **Aérodynamique** — Cd(Mach) tabulé
- **Coriolis** — force intégrée dans le vecteur d'état
- **Diffusion** — Pasquill-Gifford A→F · coefficients Turner (1970) · 6 classes
- **Seuil opérationnel** — AEGL-1/10 = 0,1 mg/m³ (HCl)

## Historique

| Version | Évolution |
|---|---|
| 6.0 | Balistique RK45, Pasquill-Gifford, profil de vent open-meteo, Web Workers, CSP stricte |
| 6.1 | Carte tactile : déplacement à un doigt, zoom par pincement |
| 6.2 | Fond de carte Esri sans clé ni API, tuiles CARTO retirées |
| 6.3 | Charte graphique AZS (application et documentation), lien de retour vers www.azs.fr, documentation claire / sombre |

## Avertissement

Cet outil est une **aide à la décision opérationnelle**. Il ne se substitue pas aux systèmes de sécurité officiels du CSG ni aux procédures réglementaires en vigueur. Les résultats doivent être interprétés par du personnel qualifié.

---

© Eric Perret 2026 · v6.3 · [www.azs.fr](https://www.azs.fr/)

## Licence

**Usage libre non commercial** — [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/deed.fr), avec mention obligatoire de la source et de l'auteur :

> dispersion — Eric PERRET — https://github.com/ericperret/dispersion

Toute utilisation commerciale est interdite sans autorisation écrite de l'auteur, à demander par courriel : **eperret@azs.fr**.
Conditions complètes (français / anglais) : [LICENSE](LICENSE).
