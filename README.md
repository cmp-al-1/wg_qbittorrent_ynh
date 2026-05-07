# WireGuard pour qBittorrent — App YunoHost

Route **uniquement** le trafic qBittorrent via NordVPN (WireGuard/NordLynx).
Le reste du serveur (Jellyfin, Radarr, Sonarr…) continue sur votre connexion normale.

## Installation

1. Dans YunoHost : **Applications → Installer → URL custom**
   - URL : `https://github.com/<username>/wg_qbittorrent_ynh`
2. Après installation, ouvrir les **Paramètres** de l'app
3. Coller votre **Access Token NordVPN**
   - Disponible sur [account.nordvpn.com](https://account.nordvpn.com) → Manual Setup → Access Token
4. Optionnel : saisir un code pays (FR, DE, US…) pour choisir la région
5. Sauvegarder — l'app fait tout le reste automatiquement

## Ce que ça fait automatiquement

- Récupère vos clés WireGuard via l'API NordVPN
- Sélectionne le serveur avec la charge la plus faible
- Configure le tunnel WireGuard (interface `nordvpn`)
- Route uniquement qBittorrent via le VPN (policy routing + fwmark)
- Active le killswitch iptables (qBittorrent bloqué si VPN déconnecté)
- Configure le binding d'interface dans qBittorrent.conf
- Tout persiste au redémarrage via systemd (PostUp/PostDown)

## Schéma

```
qBittorrent ──► iptables fwmark ──► WireGuard (nordvpn) ──► NordVPN ──► Internet
                                                                           (IP cachée)

Jellyfin / Radarr / Sonarr ──────────────────────────────────────────► Internet
                                                                        (IP normale)
```
