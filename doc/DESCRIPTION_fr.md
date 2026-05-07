Cette application configure automatiquement un tunnel VPN WireGuard dédié à qBittorrent sur votre serveur YunoHost.

**Ce que ça fait :**
- Seul le trafic qBittorrent passe par le VPN — le reste du serveur (Jellyfin, Radarr, etc.) utilise votre connexion normale
- Killswitch intégré : si le VPN tombe, qBittorrent est bloqué (votre IP réelle ne fuite pas)
- Compatible avec tout fournisseur VPN supportant WireGuard : NordVPN (NordLynx), Mullvad, AirVPN, ProtonVPN, etc.
- Fonctionne avec la persistance au redémarrage via systemd

**Prérequis :**
- L'application qBittorrent doit être installée sur ce serveur YunoHost
- Un abonnement VPN avec support WireGuard
- Le fichier `.conf` WireGuard de votre fournisseur VPN

**Obtenir votre fichier NordVPN WireGuard :**
1. Allez sur account.nordvpn.com
2. Manual Setup > WireGuard
3. Choisissez un serveur et téléchargez le fichier `.conf`
4. Copiez-collez son contenu dans les paramètres de cette app
