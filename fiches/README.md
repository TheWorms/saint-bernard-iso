# Fiches pratiques

Une fiche par outil : à quoi il sert, sa couleur de risque, comment l'ouvrir, puis ses usages courants pas à pas, avec des commandes prêtes à copier (`sdX` = disque à secourir, protégé en lecture seule ; `sdY` = disque de destination). Les mêmes fiches sont dans le système, en français et en anglais.

| Fiche | Sujet |
|---|---|
| [badblocks](badblocks.md) | lire la surface d’une copie |
| [blkdiscard](blkdiscard.md) | libérer les blocs d’une cible confirmée |
| [blockdev](blockdev.md) | consulter taille, secteurs et protection |
| [borg](borg.md) | sauvegarder et restaurer une archive chiffrée |
| [btrfs](btrfs.md) | contrôler et extraire sans réparer |
| [chntpw](chntpw.md) | examiner un SAM et préparer une copie autorisée |
| [clamscan](clamscan.md) | analyser une copie sans supprimer |
| [cryptsetup](cryptsetup.md) | examiner et ouvrir LUKS sans écriture |
| [dd](dd.md) | copier des octets sans reprise |
| [ddrescue](ddrescue.md) | cloner avec une carte de reprise |
| [ddrescuelog](ddrescuelog.md) | examiner une carte ddrescue |
| [debugfs](debugfs.md) | inspecter ext et extraire un fichier |
| [disktype](disktype.md) | identifier les structures d’un support |
| [dislocker](dislocker.md) | lire un volume BitLocker |
| [dmesg](dmesg.md) | lire les messages du noyau |
| [dmidecode](dmidecode.md) | lire les informations SMBIOS |
| [dumpe2fs](dumpe2fs.md) | lire les métadonnées ext |
| [e2fsck](e2fsck.md) | contrôler et réparer ext2/ext3/ext4 sur une copie |
| [edac-util](edac-util.md) | lire les compteurs ECC du noyau |
| [efibootmgr](efibootmgr.md) | lire et modifier les entrées UEFI |
| [extundelete](extundelete.md) | essayer une récupération ext3 ou ext4 compatible |
| [f3probe](f3probe.md) | sonder une capacité flash sur un support sacrifiable |
| [fdisk](fdisk.md) | lister ou éditer une table MBR/GPT |
| [fls](fls.md) | lister les entrées d’un système de fichiers |
| [foremost](foremost.md) | extraire des fichiers par signatures |
| [freshclam](freshclam.md) | mettre à jour les signatures officielles |
| [fsarchiver](fsarchiver.md) | archiver un système de fichiers sain |
| [fsck.exfat](fsck.exfat.md) | contrôler et réparer exFAT sur une copie |
| [fsck.fat](fsck.fat.md) | contrôler et réparer FAT sur une copie |
| [gdisk](gdisk.md) | examiner ou éditer une GPT avec un dialogue |
| [grub-install](grub-install.md) | réinstaller GRUB sur une copie |
| [guestmount](guestmount.md) | monter une image avec libguestfs en RO |
| [hdparm](hdparm.md) | identifier un disque ATA et mesurer sa lecture |
| [ioping](ioping.md) | mesurer la latence de lecture |
| [ip](ip.md) | lire les interfaces et les routes |
| [losetup](losetup.md) | présenter une image en lecture seule |
| [lsblk](lsblk.md) | identifier les disques et leurs partitions |
| [lshw](lshw.md) | inventorier le matériel |
| [lspci](lspci.md) | identifier les cartes PCI et leur pilote |
| [lsusb](lsusb.md) | inventorier les périphériques USB |
| [mc](mc.md) | parcourir et copier avec deux panneaux |
| [mdadm](mdadm.md) | lire les membres et assembler un RAID en lecture seule |
| [memtester](memtester.md) | tester une allocation de RAM |
| [mmls](mmls.md) | lire la table de partitions d’une image |
| [mount.cifs](mount.cifs.md) | monter un partage SMB identifié |
| [ms-sys](ms-sys.md) | lire ou remplacer un code MBR Microsoft |
| [ntfsclone](ntfsclone.md) | copier un NTFS sain |
| [ntfsfix](ntfsfix.md) | diagnostiquer les défauts NTFS élémentaires |
| [ntfsundelete](ntfsundelete.md) | lire et extraire des entrées NTFS supprimées |
| [nvme](nvme.md) | identifier un SSD NVMe et lire ses journaux |
| [nwipe](nwipe.md) | effacer un support explicitement choisi |
| [ocs-sr](ocs-sr.md) | sauvegarder et restaurer avec Clonezilla |
| [os-prober](os-prober.md) | chercher les systèmes sur des copies |
| [parted](parted.md) | lire et modifier une table de partitions |
| [photorec](photorec.md) | récupérer par signatures vers un autre support |
| [ping](ping.md) | tester une réponse ICMP bornée |
| [pv](pv.md) | suivre un transfert de fichiers sains |
| [pvs](pvs.md) | inventorier les volumes physiques LVM |
| [qemu-img](qemu-img.md) | examiner et convertir une image virtuelle |
| [qemu-nbd](qemu-nbd.md) | exposer une image virtuelle en lecture seule |
| [rclone](rclone.md) | copier vers un stockage configuré |
| [rescue-bench](rescue-bench.md) | mesurer la lecture d’un disque |
| [rescue-boot-repair](rescue-boot-repair.md) | diagnostiquer et réparer le démarrage |
| [rescue-clone](rescue-clone.md) | cloner avant de travailler |
| [rescue-collect](rescue-collect.md) | conserver le diagnostic de la machine |
| [rescue-disks](rescue-disks.md) | identifier les disques |
| [rescue-fsck](rescue-fsck.md) | vérifier avant de réparer |
| [rescue-help](rescue-help.md) | suivre la méthode de récupération |
| [rescue-hwinfo](rescue-hwinfo.md) | relever le matériel |
| [rescue-install](rescue-install.md) | installer sur un disque dédié |
| [rescue-lang](rescue-lang.md) | choisir la langue et le clavier |
| [rescue-menu](rescue-menu.md) | ouvrir le menu texte de secours |
| [rescue-mount](rescue-mount.md) | monter sans rejouer de journal |
| [rescue-net](rescue-net.md) | utiliser une destination réseau |
| [rescue-pxe](rescue-pxe.md) | servir Saint-Bernard par le réseau |
| [rescue-recover](rescue-recover.md) | retrouver les fichiers sur une copie |
| [rescue-report](rescue-report.md) | produire le rapport d’intervention |
| [rescue-ro](rescue-ro.md) | remettre un disque en lecture seule |
| [rescue-rw](rescue-rw.md) | autoriser l’écriture sur une destination |
| [rescue-smart](rescue-smart.md) | lire la santé d’un disque |
| [rescue-ssh](rescue-ssh.md) | ouvrir temporairement un accès distant |
| [rescue-terminal-theme](rescue-terminal-theme.md) | choisir les couleurs du terminal |
| [rescue-umount](rescue-umount.md) | refermer les montages et volumes |
| [rescue-wipe](rescue-wipe.md) | effacer un disque destiné au recyclage |
| [restic](restic.md) | sauvegarder dans un dépôt chiffré |
| [rsync](rsync.md) | copier puis comparer des fichiers |
| [sensors](sensors.md) | lire températures et tensions |
| [sfdisk](sfdisk.md) | sauvegarder et restaurer une table |
| [sgdisk](sgdisk.md) | examiner et écrire une GPT |
| [sha256sum](sha256sum.md) | calculer et vérifier des empreintes |
| [shred](shred.md) | écraser une cible sacrifiable |
| [smartctl](smartctl.md) | lire SMART et les autotests |
| [smbclient](smbclient.md) | lire ou copier sans monter un partage |
| [ssh](ssh.md) | ouvrir une session avec identité vérifiée |
| [stress-ng](stress-ng.md) | charger CPU et mémoire avec une durée fixée |
| [testdisk](testdisk.md) | analyser une copie et ses partitions |
| [tmux](tmux.md) | conserver une console et s’y rattacher |
| [tsk_recover](tsk_recover.md) | extraire les fichiers d’une image |
| [tune2fs](tune2fs.md) | lire ou modifier les paramètres ext sur une copie |
| [virt-filesystems](virt-filesystems.md) | inventorier les volumes d’une image |
| [wimlib-imagex](wimlib-imagex.md) | lire et extraire des archives WIM |
| [wipefs](wipefs.md) | lire ou retirer des signatures |
| [xfs_repair](xfs_repair.md) | vérifier ou réparer XFS démonté |
| [zpool](zpool.md) | découvrir et importer ZFS en lecture seule |

[Tous les outils](../OUTILS.md) · [Présentation](../README.md)
