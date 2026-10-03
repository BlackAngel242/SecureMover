# SecureMover

[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![PowerShell](https://img.shields.io/badge/PowerShell-5.1%2B-blue.svg)](https://learn.microsoft.com/powershell/)
[![Platform](https://img.shields.io/badge/Platform-Windows-blue.svg)](https://www.microsoft.com/windows)
[![Version](https://img.shields.io/badge/Version-2.0.2-orange.svg)](https://github.com/BlackAngel242/SecureMover/releases)
[![CI](https://github.com/BlackAngel242/SecureMover/actions/workflows/ci.yml/badge.svg)](https://github.com/BlackAngel242/SecureMover/actions/workflows/ci.yml)

🇫🇷 [Version française](README.md)

A PowerShell tool to move, restore, and back up Windows user folders to a separate partition, securely and reversibly.

---

## Table of contents

- [Why SecureMover?](#why-securemover)
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Graphical interface](#graphical-interface)
- [Security](#security)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [License](#license)

---

## Why SecureMover?

When Windows lives on C:, your personal data lives there too. A crash, a reinstall, or a full disk, and everything can be gone.

- **Isolation**: your files sit on a separate partition, shielded from system reinstalls
- **Transparency**: Windows and your apps notice no difference (registry updated)
- **Reversible**: full restore puts everything back in one click
- **Fast**: transfer via `Robocopy`, Microsoft's official tool

---

## Features

| Feature | Description |
|---------|-------------|
| **Secure move** | Moves Desktop, Documents, Downloads, Pictures, Music, Videos to another partition |
| **Full restore** | Puts folders back to their original location (`C:\Users`) |
| **External backup** | Copies folders to an external drive without touching the system |
| **Registry backup** | Automatic backup of Windows keys before any change |
| **Multilingual UI** | FR/EN support with automatic detection |
| **Detailed logging** | Timestamped log of every operation in `SecureMover.log` |
| **Terminal detection** | Automatic icon adaptation (Windows Terminal vs classic console) |

---

## Requirements

- **OS**: Windows 10 / 11 (or Windows 7/8.1 with PowerShell 5.1+)
- **PowerShell**: 5.1 or higher

  ```powershell
  $PSVersionTable.PSVersion
  ```

- **Rights**: Administrator (the script can relaunch itself automatically)
- **Space**: User folders size × 1.5 on the target partition

---

## Installation

```powershell
git clone https://github.com/BlackAngel242/SecureMover.git
cd SecureMover
```

If PowerShell blocks execution:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

---

## Usage

### Launch

```powershell
# Right-click SecureMover.ps1 > "Run with PowerShell"

# Or from an admin terminal:
Start-Process powershell -ArgumentList "-ExecutionPolicy Bypass -File `"$PWD\SecureMover.ps1`"" -Verb RunAs
```

### Home screen

```
╔═══════════════════════════════════════════════════════════════════╗
║   ____                          __  __                           ║
║  / ___|  ___  ___ _   _ _ __ ___|  \/  | _____   _____ _ __     ║
║  \___ \ / _ \/ __| | | | '__/ _ \ |\/| |/ _ \ \ / / _ \ '__|   ║
║   ___) |  __/ (__| |_| | | |  __/ |  | | (_) \ V /  __/ |      ║
║  |____/ \___|\___|\__,_|_|  \___|_|  |_|\___/ \_/ \___|_|      ║
║                                                                   ║
║                      Version 2.0.2                               ║
║          Secure user profile relocation                          ║
╚═══════════════════════════════════════════════════════════════════╝
```

### Options

| Option | Action |
|--------|--------|
| **[1] Move** | Select a profile, choose the target partition, confirm. Reboot required. |
| **[2] Restore** | Automatic detection of moved profiles, put back + registry restore. |
| **[3] Backup** | Copy to an external drive without changing the system. Best before any operation. |

---

## Graphical interface

A graphical interface is available for terminal-free use:

- Double-click `Lancer-GUI.bat`, **or**
- Run `SecureMover-GUI.ps1` from PowerShell.

See [docs/README_GUI.md](docs/README_GUI.md) for the full guide (French).

---

## Security

| Measure | Detail |
|---------|--------|
| **Admin check** | Mandatory check at startup, automatic relaunch if needed |
| **Registry backup** | Timestamped `.reg` file created before any change |
| **Space validation** | Required space computed, abort if insufficient |
| **Permissions** | Write test on the target partition before starting |
| **Error handling** | Try-Catch on all critical operations, rollback possible |
| **Robocopy** | Official Microsoft tool, built-in retry, metadata preservation |

**Generated files:**

```
SecureMover_Backup_YYYYMMDD_HHMMSS.reg   # Registry backup (keep at least 30 days)
SecureMover.log                           # Operations log
```

> **Warning**: this script modifies the Windows registry and moves files. Automatic backups are created, but the author cannot be held responsible for any data loss. Test on a non-critical profile first.

---

## Roadmap

| Version | Status | Features |
|---------|--------|----------|
| **2.0** | Stable | FR/EN interface, restore, backup, logging |
| **2.1** | In progress | Individual folder selection, silent mode, simultaneous multi-profiles |
| **3.0** | Planned | Scheduled backups, compression, space statistics |

---

## Contributing

Contributions are welcome. See [docs/CONTRIBUTING.md](docs/CONTRIBUTING.md) for the full guide (French).

```powershell
git checkout -b feature/my-feature
git commit -m "feat: short description"
git push origin feature/my-feature
# Open a Pull Request on GitHub
```

Questions or bugs: [GitHub Issues](https://github.com/BlackAngel242/SecureMover/issues)

---

## License

This project is under the **MIT** license — see [LICENSE](LICENSE).

---

<div align="center">

*"Protect your data, secure your future"*

[Back to top](#securemover)

</div>
