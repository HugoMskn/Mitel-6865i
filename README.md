# Mitel 6865i Firmware Mirror

Mirror de firmware et pack de langue FR pour le téléphone IP Mitel 6865i.

## Fichiers

| Fichier | Description |
|---------|-------------|
| `6865i.st` | Firmware pour le Mitel 6865i. |
| `aastra.cfg` | Configuration pour le provisionnement : langue française, fuseau horaire Europe/Paris (heure d'été automatique), format date/heure 24h. |
| `lang_fr.txt` | Pack de langue français pour l'interface LCD du téléphone (~1800 traductions). |

## Installation

### 1. Firmware
Le fichier `6865i.st` doit être servi via TFTP/HTTP sur un serveur accessible par le téléphone. Utiliser `aastra.cfg` pour pointer vers ce fichier.

### 2. Configuration (`aastra.cfg`)
Inclure ce fichier dans le serveur de provisionning pour que le téléphone le télécharge automatiquement. Il configure :
- Langue du téléphone en français
- Fuseau horaire Paris (UTC+1, heure d'été +1h)
- Format 24h, date française (JJ/MM/AAAA)

### 3. Pack de langue FR
Le fichier `lang_fr.txt` doit être accessible via le même chemin que `aastra.cfg` sur le serveur de provisionning.

## Sonneries custom

L'upload via le navigateur ne fonctionne pas avec les navigateurs modernes (ils cancel le transfert à cause du header `Expect: 100-continue` en HTTP). Utiliser curl à la place.

### Conversion avec ffmpeg

```bash
ffmpeg -y -i musique.mp3 -acodec pcm_alaw -ar 8000 -ac 1 -t 30 -map_metadata -1 -fflags +bitexact sonnerie.wav
```

- `-acodec pcm_alaw` : format requis par le Mitel
- `-ar 8000` : 8 kHz
- `-ac 1` : mono
- `-t 30` : max 30 secondes

### Upload via curl

```bash
curl -H "Authorization: Basic $(echo -n username:password | base64)" \
     -H "Expect:" \
     -F "upload_ringtone/newfile=@sonnerie.wav;type=audio/wav" \
     "http://IP_DU_TEL:PORT/cgi-bin/webconfig?page=upload_ringtone&action=submit&section=0&conn=0"
```

Remplacer :
- `IP_DU_TEL` : adresse IP du téléphone
- `PORT` : port web (par défaut 80)
- `username` et `password` : credentials admin du téléphone
- `sonnerie.wav` : nom du fichier converti

### Authentification

L'auth Basic utilise le format `username:password` encodé en Base64. Exemple pour `admin:22222` :
```bash
echo -n "admin:22222" | base64
# → YWRtaW46MjIyMjI=
```

## Notes

- Le pack de langue FR officiel Mitel est difficile à trouver, ce repository le conserve pour archive.
- Le téléphone doit être provisionné via TFTP/HTTP avec un serveur accessible sur le réseau.
