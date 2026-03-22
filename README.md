# Mitel 6865i Firmware Mirror

Mirror de firmware et pack de langue FR pour le téléphone IP Mitel 6865i.

## Fichiers

| Fichier | Description |
|---------|-------------|
| `aastra.cfg` | Configuration pour le provisionnement : langue française, fuseau horaire Europe/Paris (heure d'été automatique), format date/heure 24h. |
| `lang_fr.txt` | Pack de langue français pour l'interface LCD du téléphone (~1800 traductions). |

## Installation

### 1. Firmware
Télécharger le firmware depuis le site Mitel (compte requis) ou une source fiable, puis le placer sur un serveur TFTP/HTTP.

### 2. Configuration (`aastra.cfg`)
Inclure ce fichier dans le serveur de provisionning pour que le téléphone le télécharge automatiquement. Il configure :
- Langue du téléphone en français
- Fuseau horaire Paris (UTC+1, heure d'été +1h)
- Format 24h, date française (JJ/MM/AAAA)

### 3. Pack de langue FR
Le fichier `lang_fr.txt` doit être accessible via le même chemin que `aastra.cfg` sur le serveur de provisionning.

## Notes

- Le pack de langue FR officiel Mitel est difficile à trouver, ce repository le conserve pour archive.
- Le téléphone doit être provisionné via TFTP/HTTP avec un serveur accessible sur le réseau.
