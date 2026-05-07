# WireGuard pour qBittorrent — App YunoHost

Route le trafic qBittorrent via un VPN WireGuard (NordVPN, Mullvad, AirVPN…) sans affecter le reste du serveur.

## Installation via YunoHost

Dans l'interface admin YunoHost :
1. Applications > Installer > Installer une app custom
2. URL du dépôt : `https://github.com/<votre-username>/wg_qbittorrent_ynh`
3. Après installation, aller dans les **Paramètres** de l'app et coller votre fichier `.conf` WireGuard

## Fichier NordVPN WireGuard

1. [account.nordvpn.com](https://account.nordvpn.com) > Manual Setup > WireGuard
2. Choisissez un pays/serveur > Download Config
3. Copiez-collez le contenu dans les paramètres

## Architecture

```
qBittorrent (user: qbittorrent)
    │
    ├── iptables fwmark 0x1
    ├── ip rule: fwmark 0x1 → table 100
    ├── ip route: table 100 default → wg interface
    │
    └── WireGuard (nordvpn / wg0)
            │
            └── Serveur NordVPN (endpoint:51820)
                        │
                        └── Internet (IP cachée)

Reste du serveur (Jellyfin, Radarr, Sonarr…) → Internet direct (IP normale)
```

## Killswitch

Quand activé : si le VPN se déconnecte, qBittorrent est bloqué via iptables.
Les règles sont injectées dans `PostUp`/`PostDown` du fichier WireGuard → persistance automatique au redémarrage.
