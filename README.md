# SecureMover

[![Licence](https://img.shields.io/badge/Licence-MIT-green.svg)](LICENSE)
[![PowerShell](https://img.shields.io/badge/PowerShell-5.1%2B-blue.svg)](https://learn.microsoft.com/powershell/)
[![Plateforme](https://img.shields.io/badge/Plateforme-Windows-blue.svg)](https://www.microsoft.com/windows)
[![Version](https://img.shields.io/badge/Version-2.0.2-orange.svg)](https://github.com/BlackAngel242/SecureMover/releases)
[![CI](https://github.com/BlackAngel242/SecureMover/actions/workflows/ci.yml/badge.svg)](https://github.com/BlackAngel242/SecureMover/actions/workflows/ci.yml)

🇬🇧 [English version](README.en.md)

Outil PowerShell pour déplacer, restaurer et sauvegarder les dossiers utilisateurs Windows vers une partition séparée, de manière sécurisée et réversible.

---

## Table des matières

- [Pourquoi SecureMover ?](#pourquoi-securemover-)
- [Fonctionnalités](#fonctionnalités)
- [Prérequis](#prérequis)
- [Installation](#installation)
- [Utilisation](#utilisation)
- [Interface graphique](#interface-graphique)
- [Sécurité](#sécurité)
- [Roadmap](#roadmap)
- [Contribution](#contribution)
- [Licence](#licence)

---

## Pourquoi SecureMover ?

Quand Windows est sur C:, vos données personnelles y sont aussi. Un crash, une réinstallation, ou un disque saturé, et tout peut disparaître.

- **Isolation** : vos fichiers sont sur une partition distincte, protégés des réinstallations système
- **Transparence** : Windows et vos applications ne voient aucune différence (registre mis à jour)
- **Réversible** : la restauration complète remet tout en place en un clic
- **Rapide** : transfert via `Robocopy`, outil officiel Microsoft

---

## Fonctionnalités

| Fonctionnalité | Description |
|----------------|-------------|
| **Déplacement sécurisé** | Déplace Desktop, Documents, Downloads, Pictures, Music, Videos vers une autre partition |
| **Restauration complète** | Remet les dossiers à leur emplacement d'origine (`C:\Users`) |
| **Sauvegarde externe** | Copie les dossiers sur un lecteur externe sans toucher au système |
| **Sauvegarde du registre** | Backup automatique des clés Windows avant toute modification |
| **Interface multilingue** | Support FR/EN avec détection automatique |
| **Logging détaillé** | Journal horodaté de toutes les opérations dans `SecureMover.log` |
| **Détection terminal** | Adaptation automatique des icônes (Windows Terminal vs console classique) |

---

## Prérequis

- **OS** : Windows 10 / 11 (ou Windows 7/8.1 avec PowerShell 5.1+)
- **PowerShell** : 5.1 ou supérieur

  ```powershell
  $PSVersionTable.PSVersion
  ```

- **Droits** : Administrateur (le script peut se relancer automatiquement)
- **Espace** : Taille des dossiers utilisateurs × 1.5 sur la partition cible

---

## Installation

```powershell
git clone https://github.com/BlackAngel242/SecureMover.git
cd SecureMover
```

Si PowerShell bloque l'exécution :

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

---

## Utilisation

### Lancement

```powershell
# Clic droit sur SecureMover.ps1 > "Exécuter avec PowerShell"

# Ou depuis un terminal admin :
Start-Process powershell -ArgumentList "-ExecutionPolicy Bypass -File `"$PWD\SecureMover.ps1`"" -Verb RunAs
```

### Écran d'accueil

```
╔═══════════════════════════════════════════════════════════════════╗
║   ____                          __  __                           ║
║  / ___|  ___  ___ _   _ _ __ ___|  \/  | _____   _____ _ __     ║
║  \___ \ / _ \/ __| | | | '__/ _ \ |\/| |/ _ \ \ / / _ \ '__|   ║
║   ___) |  __/ (__| |_| | | |  __/ |  | | (_) \ V /  __/ |      ║
║  |____/ \___|\___|\__,_|_|  \___|_|  |_|\___/ \_/ \___|_|      ║
║                                                                   ║
║                      Version 2.0.2                               ║
║          Déplacement sécurisé des profils utilisateurs           ║
╚═══════════════════════════════════════════════════════════════════╝
```

### Menu principal

```
+==================== MENU PRINCIPAL ====================+
|                                                        |
|  [1] Déplacer un Profil Utilisateur                   |
|  [2] Restaurer un Profil Utilisateur                  |
|  [3] Créer une sauvegarde d'un Profil                 |
|  [4] Aide et Informations                             |
|  [5] Quitter                                           |
|                                                        |
+========================================================+
```

### Options

| Option | Action |
|--------|--------|
| **[1] Déplacer** | Sélectionner un profil, choisir la partition cible, confirmer. Redémarrage requis. |
| **[2] Restaurer** | Détection automatique des profils déplacés, remise en place + restauration registre. |
| **[3] Sauvegarder** | Copie vers lecteur externe sans modifier le système. Idéal avant toute opération. |

---

## Interface graphique

Une interface graphique est disponible pour un usage sans terminal :

- Double-cliquez sur `Lancer-GUI.bat`, **ou**
- Lancez `SecureMover-GUI.ps1` depuis PowerShell.

Voir [docs/README_GUI.md](docs/README_GUI.md) pour le guide complet.

---

## Sécurité

| Mesure | Détail |
|--------|--------|
| **Vérification admin** | Contrôle obligatoire au démarrage, relancement automatique si nécessaire |
| **Backup registre** | Fichier `.reg` horodaté créé avant toute modification |
| **Validation espace** | Calcul de l'espace requis, arrêt si insuffisant |
| **Permissions** | Test d'écriture sur la partition cible avant de commencer |
| **Gestion d'erreurs** | Try-Catch sur toutes les opérations critiques, rollback possible |
| **Robocopy** | Outil Microsoft officiel, retry intégré, préservation des métadonnées |

**Fichiers générés :**

```
SecureMover_Backup_YYYYMMDD_HHMMSS.reg   # Sauvegarde registre (conserver 30 jours min)
SecureMover.log                           # Journal des opérations
```

> **Avertissement** : ce script modifie le registre Windows et déplace des fichiers. Des sauvegardes automatiques sont créées, mais l'auteur ne peut être tenu responsable de toute perte de données. Testez d'abord sur un profil non critique.

---

## Roadmap

| Version | Statut | Fonctionnalités |
|---------|--------|-----------------|
| **2.0** | Stable | Interface FR/EN, restauration, sauvegarde, logging |
| **2.1** | En cours | Sélection de dossiers individuels, mode silencieux, multi-profils simultanés |
| **3.0** | Planifié | Sauvegardes planifiées, compression, statistiques d'espace |

---

## Contribution

Les contributions sont les bienvenues. Voir [CONTRIBUTING.md](docs/CONTRIBUTING.md) pour le guide complet.

```powershell
git checkout -b feature/ma-fonctionnalite
git commit -m "feat: description courte"
git push origin feature/ma-fonctionnalite
# Ouvrir une Pull Request sur GitHub
```

**Contributions acceptées** : corrections de bugs, nouvelles fonctionnalités, documentation, traductions, tests.

Questions ou bugs : [GitHub Issues](https://github.com/BlackAngel242/SecureMover/issues)

---

## Licence

Ce projet est sous licence **MIT** — voir [LICENSE](LICENSE).

---

<div align="center">

*« Protégez vos données, sécurisez votre avenir »*

[Retour en haut](#securemover)

</div>
