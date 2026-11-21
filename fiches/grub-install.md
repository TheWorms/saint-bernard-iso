# grub-install — réinstaller GRUB sur une copie

**Couleur : rouge.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Démarrage et Windows ; fenêtre `assistant-grub-install` ; terminal : `sudo grub-install`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une cible distincte, sacrifiable pour les effacements. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. `/tmp` et les rapports du live sont en RAM, perdus à l’arrêt. Un serveur distant doit être autorisé et son identité vérifiée.

## Usages

### 1. Réinstaller le chargeur BIOS — rouge

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY2 /mnt/CIBLE &&
sudo grub-install --target=i386-pc --boot-directory=/mnt/CIBLE/boot /dev/sdY
```

Copie GPT avec partition BIOS Boot et racine déjà identifiées ; pas de --force pour masquer un problème d’intégration.

### 2. Installer UEFI sans changer la NVRAM — rouge

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/ESP &&
sudo grub-install --target=x86_64-efi --efi-directory=/mnt/ESP --boot-directory=/mnt/ESP/boot --bootloader-id=RECUP --no-nvram
```

ESP FAT montée sur la copie. Écrit des fichiers EFI mais aucune entrée du firmware ; adapter ensuite la configuration de démarrage.

### 3. Installer le chemin UEFI amovible — rouge

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/ESP &&
sudo grub-install --target=x86_64-efi --efi-directory=/mnt/ESP --boot-directory=/mnt/ESP/boot --removable --no-nvram
```

Écrit EFI/BOOT/BOOTX64.EFI sur la copie. Vérifier qu’aucun chargeur existant à conserver n’occupe ce chemin.

## Pièges

- Ne pas confondre BIOS/MBR et UEFI/ESP ; le disque passé en argument BIOS est le disque entier.
- Ces commandes ne régénèrent pas grub.cfg. Un fichier EFI présent ne prouve pas le démarrage ; tester la copie et vérifier le guide Secure Boot.

## Voir aussi

`rescue-ro`, `rescue-rw`, `sha256sum`, guide 10.
