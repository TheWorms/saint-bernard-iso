# Les outils de Saint-Bernard

Version 2026.11.4 · **328 outils** en 16 rubriques, rangés comme dans le menu **SOS** du bureau. 300 ont un assistant graphique (une fenêtre qui pose les questions dans l'ordre et montre la commande avant de la lancer) ; 105 ont une fiche pratique (usages courants, commandes prêtes à copier, pièges).

Page générée depuis le catalogue du système (`outils.tsv`), la même source que le menu SOS : elle ne décrit que ce qui est réellement dans l'image.

## Couleurs de risque

Chaque outil porte la couleur de ce qu'il peut faire de pire au disque. Le menu SOS l'affiche aussi en toutes lettres.

| | Couleur | Ce que l'outil peut faire |
|---|---|---|
| ⚪ | aucun | sans rapport avec les disques |
| 🟢 | vert | inventaire, lecture de métadonnées |
| 🟡 | jaune | lecture intensive : peut achever un disque instable |
| 🟠 | orange | écrit sur un disque de destination |
| 🔴 | rouge | modifie ou détruit |

Dans le système, un outil en terminal s'ouvre avec son aide (options, exemples) affichée au-dessus de l'invite ; les fiches pratiques vont plus loin (usages pas à pas, pièges). [Toutes les fiches](fiches/README.md).

Les disques de la machine sont protégés en lecture seule au démarrage. Un outil orange ou rouge n'écrit que sur un disque déverrouillé exprès (`rescue-rw`). 🔒 : l'outil a besoin des droits administrateur ; le menu le lance avec `sudo`.

## Rubriques

| Rubrique | Outils |
|---|---:|
| [Diagnostic des disques](#diagnostic-des-disques) | 21 |
| [Tests et mesures](#tests-et-mesures) | 22 |
| [Mémoire (RAM)](#mémoire-ram) | 9 |
| [Matériel et système](#matériel-et-système) | 23 |
| [Clonage et images](#clonage-et-images) | 44 |
| [Images et machines virtuelles](#images-et-machines-virtuelles) | 13 |
| [Récupération de fichiers](#récupération-de-fichiers) | 34 |
| [Windows, macOS et analyse](#windows-macos-et-analyse) | 11 |
| [Partitions et volumes](#partitions-et-volumes) | 43 |
| [Systèmes de fichiers](#systèmes-de-fichiers) | 41 |
| [Sauvegarde](#sauvegarde) | 10 |
| [Démarrage et Windows](#démarrage-et-windows) | 16 |
| [Effacement](#effacement) | 9 |
| [Antivirus](#antivirus) | 2 |
| [Réseau](#réseau) | 21 |
| [Bureau](#bureau) | 9 |

## Diagnostic des disques

| Outil | Ce qu'il fait | Risque | S'ouvre | Fiche pratique |
|---|---|---|---|---|
| **blockdev** 🔒 | taille et secteurs d'un disque ; --setro pour le bloquer en lecture seule — assistant : Lire la capacité et l’état du périphérique bloc | 🟢 vert | assistant graphique, terminal | [fiche](fiches/blockdev.md) |
| **GSmartControl** 🔒 | SMART, interface graphique | 🟢 vert | fenêtre |  |
| **hdparm -I** 🔒 | identité d'un disque ATA — assistant : Lire l’identité et les limites ATA | 🟡 jaune | assistant graphique, terminal | [fiche](fiches/hdparm.md) |
| **lsblk, blkid** 🔒 | topologie et systèmes de fichiers — assistant : Lire la topologie et les signatures | 🟢 vert | assistant graphique, terminal | [fiche](fiches/lsblk.md) |
| **lsscsi** | inventaire SCSI, SATA, USB — assistant : Inventorier les chemins SCSI et USB | 🟢 vert | assistant graphique, terminal |  |
| **Messages du noyau en direct** 🔒 | erreurs d'E/S, resets — assistant : Lire les erreurs du noyau | 🟢 vert | assistant graphique, terminal plein écran | [fiche](fiches/dmesg.md) |
| **nvme** 🔒 | santé et journaux des SSD NVMe — assistant : Lire la santé et l’identité NVMe | 🟢 vert | assistant graphique, terminal | [fiche](fiches/nvme.md) |
| **openSeaChest_Info** 🔒 | identité détaillée d'un disque — assistant : Lire l’identité détaillée openSeaChest | 🟢 vert | assistant graphique, terminal |  |
| **openSeaChest_Logs** 🔒 | lecture des journaux internes du disque : --listSupportedLogs, --farm — assistant : Afficher les journaux openSeaChest | 🟢 vert | assistant graphique, terminal |  |
| **openSeaChest_SMART** 🔒 | diagnostic ATA, SAS, NVMe — assistant : Lire le diagnostic SMART openSeaChest | 🟢 vert | assistant graphique, terminal |  |
| **QDiskInfo** 🔒 | état SMART façon CrystalDiskInfo, autotests SMART | 🟡 jaune | fenêtre |  |
| **rescue-disks** 🔒 | tableau des disques : modèle, série, bus, lecture seule ou écriture, montages, verdict SMART — assistant : Afficher le tableau des disques | 🟢 vert | assistant graphique, terminal plein écran | [fiche](fiches/rescue-disks.md) |
| **rescue-report** 🔒 | rapport d'intervention HTML : disque, SMART, journal, clonage, récupération ; aucun nom de fichier — assistant : Préparer le rapport d’intervention | 🟢 vert | assistant graphique, terminal | [fiche](fiches/rescue-report.md) |
| **rescue-smart** 🔒 | rapport SMART lisible et verdict prudent, pont USB détecté ; --test lance un autotest : jaune — assistant : Lire le rapport SMART prudent | 🟢 vert | assistant graphique, terminal | [fiche](fiches/rescue-smart.md) |
| **sdparm** 🔒 | pages de mode SCSI — assistant : Lire les pages de mode SCSI | 🟢 vert | assistant graphique, terminal |  |
| **sg3-utils : sg_inq, sg_logs, sg_readcap** 🔒 | SCSI bas niveau — assistant : Lire l’identité et la capacité SCSI | 🟢 vert | assistant graphique, terminal |  |
| **sg_logs** 🔒 | journaux SCSI/SAS : erreurs, température ; -a tout lire ; écrire --readonly en toutes lettres, jamais -R ni --reset — assistant : Lire les journaux SCSI et SAS | 🟢 vert | assistant graphique, terminal |  |
| **sg_sat_identify** 🔒 | IDENTIFY ATA à travers un pont USB/SAS ; -R pour ouvrir en lecture seule — assistant : Lire IDENTIFY ATA à travers un pont | 🟢 vert | assistant graphique, terminal |  |
| **sg_vpd** 🔒 | pages VPD SCSI : numéro de série, identifiants, limites de blocs — assistant : Lire les identifiants VPD SCSI | 🟢 vert | assistant graphique, terminal |  |
| **smartctl** 🔒 | SMART en ligne de commande — assistant : Lire SMART et ses journaux — smartctl | 🟢 vert | assistant graphique, terminal | [fiche](fiches/smartctl.md) |
| **État des disques** | Lire l’état lecture seule des disques | 🟢 vert | assistant graphique |  |

## Tests et mesures

| Outil | Ce qu'il fait | Risque | S'ouvre | Fiche pratique |
|---|---|---|---|---|
| **badblocks -sv** 🔒 | surface en lecture ; -w détruit les données — assistant : Examiner la surface sans écrire | 🟡 jaune | assistant graphique, terminal | [fiche](fiches/badblocks.md) |
| **blkparse** | décode les traces d'E/S de blktrace, ex. sudo blktrace -d /dev/sdX -o - / blkparse -i - — assistant : Décoder une trace bloc existante | 🟢 vert | assistant graphique, terminal |  |
| **blktrace** 🔒 | trace des requêtes d'E/S — assistant : Enregistrer une trace des accès bloc | 🟠 orange | assistant graphique, terminal |  |
| **bonnie++** | performances d'un système de fichiers ; écrit — assistant : Mesurer un système de fichiers sur une destination distincte | 🟠 orange | assistant graphique, terminal |  |
| **btt** | statistiques de latence à partir d'une trace blktrace — assistant : Analyser les latences d’une trace bloc | 🟠 orange | assistant graphique, terminal |  |
| **F3 : f3fix** 🔒 | réécrit la table de partitions à la capacité réelle d'une fausse clé — assistant : Réécrire les partitions d’une copie de fausse clé | 🔴 rouge | assistant graphique, terminal |  |
| **F3 : f3probe** 🔒 | --destructive efface le support — assistant : Examiner une copie physique avec F3 Probe | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/f3probe.md) |
| **F3 : f3read** 🔒 | relit et vérifie les fichiers écrits par f3write ; lecture seule — assistant : Relire les fichiers de capacité F3 existants | 🟡 jaune | assistant graphique, terminal |  |
| **F3 : f3write puis f3read** | capacité réelle d'une clé ; écrit — assistant : Tester la capacité par fichiers F3 sur la destination | 🟠 orange | assistant graphique, terminal |  |
| **fio** 🔒 | performances ; écrit selon le job — assistant : Mesurer les entrées-sorties avec un travail fio borné | 🟠 orange | assistant graphique, terminal |  |
| **hdparm -t** 🔒 | débit de lecture — assistant : Lire l’identité ATA et mesurer le débit | 🟡 jaune | assistant graphique, terminal | [fiche](fiches/hdparm.md) |
| **ioping** 🔒 | latence d'accès ; sur un périphérique, pas sur un dossier, où il écrit un fichier de test — assistant : Mesurer la latence de lecture d’un disque | 🟡 jaune | assistant graphique, terminal | [fiche](fiches/ioping.md) |
| **iostat** | débit et attente par disque — assistant : Observer les entrées-sorties d’un disque | 🟢 vert | assistant graphique, terminal |  |
| **iotop** 🔒 | processus qui sollicitent les disques — assistant : Voir les processus qui sollicitent les disques | 🟢 vert | assistant graphique, terminal plein écran |  |
| **KDiskMark** 🔒 | mesure de débit disque façon CrystalDiskMark, via fio ; écrit un gros fichier de test sur le volume choisi : disque sain et monté en écriture uniquement | 🟠 orange | fenêtre |  |
| **likwid-perfctr** 🔒 | compteurs matériels du processeur ; -a liste les groupes, module msr requis — assistant : Lire les groupes et compteurs de performance | ⚪ aucun | assistant graphique, terminal |  |
| **openSeaChest_GenericTests** 🔒 | tests de lecture de surface --shortGeneric, --longGeneric ; --repairOnFly réécrit les secteurs défectueux — assistant : Lire la surface avec openSeaChest sans réparation | 🔴 rouge | assistant graphique, terminal |  |
| **pidstat** 🔒 | E/S disque par processus, ex. pidstat -d 2 — assistant : Observer les entrées-sorties des processus | 🟢 vert | assistant graphique, terminal |  |
| **rescue-bench** 🔒 | débit de lecture au début, au milieu et à la fin du disque, latence d'accès ; refusé si SMART est critique — assistant : Mesurer une lecture avec les garde-fous Saint-Bernard | 🟡 jaune | assistant graphique, terminal | [fiche](fiches/rescue-bench.md) |
| **stress-ng** | charge processeur, mémoire, E/S — assistant : Appliquer une charge CPU ou mémoire bornée | 🟡 jaune | assistant graphique, terminal | [fiche](fiches/stress-ng.md) |
| **WHDD** 🔒 | test de surface en lecture ; ses fonctions d'effacement et de HPA détruisent — assistant : Comprendre les limites du lancement WHDD | 🔴 rouge | assistant graphique, terminal plein écran |  |
| **zcav /dev/sdX** 🔒 | débit zone par zone d'un disque, en lecture ; -w détruit les données — assistant : Lire le débit zone par zone | 🟡 jaune | assistant graphique, terminal |  |

## Mémoire (RAM)

| Outil | Ce qu'il fait | Risque | S'ouvre | Fiche pratique |
|---|---|---|---|---|
| **decode-dimms** 🔒 | lecture SPD des barrettes : type, taille, timings ; charger d'abord le module at24 (DDR à DDR3) ou ee1004 (DDR4) — assistant : Lire les caractéristiques SPD des barrettes | 🟢 vert | assistant graphique, terminal |  |
| **edac-util** | compteurs d'erreurs mémoire ECC du noyau, lecture seule ; utile seulement avec une carte mère et des barrettes ECC — assistant : Lire les compteurs mémoire ECC | 🟢 vert | assistant graphique, terminal | [fiche](fiches/edac-util.md) |
| **likwid-bench** | bande passante mémoire ; -a liste les tests, ex. -t load -w S0:1GB — assistant : Mesurer la bande passante mémoire — LIKWID | 🟡 jaune | assistant graphique, terminal |  |
| **memtester** 🔒 | mémoire, sans redémarrer — assistant : Tester une portion de la mémoire vive | 🟢 vert | assistant graphique, terminal | [fiche](fiches/memtester.md) |
| **numactl** | topologie NUMA : nœuds, processeurs et mémoire par nœud, --hardware pour lire sans rien changer — assistant : Lire la topologie NUMA | ⚪ aucun | assistant graphique, terminal |  |
| **numastat** | statistiques d'allocation mémoire par nœud NUMA, -m pour la répartition — assistant : Lire les allocations par nœud NUMA | ⚪ aucun | assistant graphique, terminal |  |
| **ras-mc-ctl** 🔒 | erreurs mémoire ECC/EDAC : --status, --error-count, --summary — assistant : Lire les erreurs ECC et EDAC | 🟢 vert | assistant graphique, terminal |  |
| **stressapptest** | stress de la mémoire, ex. -s 60 -M 2000 ; ne pas utiliser -d ni -f, qui écrivent sur disque — assistant : Tester les échanges en mémoire | 🟡 jaune | assistant graphique, terminal |  |
| **sysbench memory** | Mesurer le débit mémoire — sysbench | ⚪ aucun | assistant graphique |  |

## Matériel et système

| Outil | Ce qu'il fait | Risque | S'ouvre | Fiche pratique |
|---|---|---|---|---|
| **biosdecode** 🔒 | structures du BIOS : SMBIOS, ACPI, PnP, PIR — assistant : Examiner les structures du BIOS | 🟢 vert | assistant graphique, terminal |  |
| **bmc-info, ipmi-fru** 🔒 | identité du BMC et inventaire FRU — assistant : Identifier le BMC et l’inventaire FRU | 🟢 vert | assistant graphique, terminal |  |
| **btop** | ce qui tourne : processus, processeur, mémoire, disques — assistant : Surveiller la charge — btop | 🟢 vert | assistant graphique, terminal plein écran |  |
| **dmidecode** 🔒 | carte mère, BIOS, barrettes — assistant : Lire les tables SMBIOS | 🟢 vert | assistant graphique, terminal | [fiche](fiches/dmidecode.md) |
| **fwupdmgr** 🔒 | mise à jour des firmwares de disques, SSD et périphériques via LVFS ; get-devices pour seulement lister ; son service fwupd est masqué : utiliser fwupdtool, ou sudo systemctl unmask --now fwupd — assistant : Lire l’inventaire du service fwupd | 🔴 rouge | assistant graphique, terminal |  |
| **fwupdtool** 🔒 | firmwares sans démon ; get-devices pour lister, install et update flashent le firmware — assistant : Inspecter les firmwares sans démon | 🔴 rouge | assistant graphique, terminal |  |
| **Hardinfo2** | inventaire matériel et benchmarks, interface graphique ; les benchmarks chargent le processeur | 🟢 vert | fenêtre |  |
| **hwinfo** 🔒 | détection matérielle détaillée — assistant : Détecter le matériel — hwinfo | 🟢 vert | assistant graphique, terminal |  |
| **i2cdetect** 🔒 | sonde les bus I2C/SMBus, peut perturber le bus ; -l pour lister sans sonder ; module i2c-dev requis — assistant : Examiner les bus I2C et SMBus | 🟡 jaune | assistant graphique, terminal |  |
| **inxi** | résumé du système — assistant : Résumer la configuration — inxi | 🟢 vert | assistant graphique, terminal |  |
| **ipmi-sel** 🔒 | journal d'événements matériels du BMC ; --clear et --delete l'effacent — assistant : Lire les événements du BMC local | 🔴 rouge | assistant graphique, terminal |  |
| **ipmi-sensors** 🔒 | capteurs BMC/IPMI : températures, ventilateurs, tensions ; cartes serveur seulement — assistant : Lire les capteurs du BMC local | 🟢 vert | assistant graphique, terminal |  |
| **ipmitool** 🔒 | lecture BMC/IPMI des serveurs : sensor, sel list, fru ; éviter chassis power, sel clear, mc reset, hpm et les commandes set — assistant : Lire le BMC local — ipmitool | 🔴 rouge | assistant graphique, terminal |  |
| **likwid-topology** | topologie du processeur : cœurs, caches, nœuds mémoire — assistant : Lire la topologie du processeur | 🟢 vert | assistant graphique, terminal |  |
| **lshw** 🔒 | inventaire matériel — assistant : Inventorier le matériel — lshw | 🟢 vert | assistant graphique, terminal | [fiche](fiches/lshw.md) |
| **lspci** | cartes et contrôleurs PCI — assistant : Lire les périphériques PCI | 🟢 vert | assistant graphique, terminal | [fiche](fiches/lspci.md) |
| **lsusb** | périphériques USB — assistant : Lire les périphériques USB | 🟢 vert | assistant graphique, terminal | [fiche](fiches/lsusb.md) |
| **ncdu** | occupation d'un dossier — assistant : Examiner l’occupation d’un dossier | 🟢 vert | assistant graphique, terminal plein écran |  |
| **rescue-collect** 🔒 | archive de diagnostic : journaux, matériel, disques, SMART ; dans RESCUE-DATA ; lecture seule — assistant : Collecter un diagnostic local | 🟢 vert | assistant graphique, terminal | [fiche](fiches/rescue-collect.md) |
| **rescue-hwinfo** 🔒 | relevé matériel pour la fiche de test : processeur, carte mère, contrôleurs, disques ; enregistré sur RESCUE-DATA — assistant : Produire le relevé matériel | 🟢 vert | assistant graphique, terminal plein écran | [fiche](fiches/rescue-hwinfo.md) |
| **sensors** | températures — assistant : Lire les températures et ventilateurs | 🟢 vert | assistant graphique, terminal | [fiche](fiches/sensors.md) |
| **sensors-detect** 🔒 | détecte les puces de capteurs ; sonde le matériel, peut écrire /etc/modules — assistant : Détecter les puces de capteurs | 🟠 orange | assistant graphique, terminal |  |
| **strace** 🔒 | voir les appels système d'un programme : pourquoi il échoue — assistant : Observer les appels système — strace | ⚪ aucun | assistant graphique, terminal |  |

## Clonage et images

| Outil | Ce qu'il fait | Risque | S'ouvre | Fiche pratique |
|---|---|---|---|---|
| **affconvert** | convertir une image brute en AFF ou l'inverse, écrit une nouvelle image — assistant : Convertir entre image brute et AFF | 🟠 orange | assistant graphique, terminal |  |
| **affinfo** | informations et métadonnées d'une image forensique AFF — assistant : Lire les informations d’une image AFF | 🟢 vert | assistant graphique, terminal |  |
| **affverify** | vérifier la signature numérique d'une image AFF signée — assistant : Vérifier les signatures d’une image AFF | 🟡 jaune | assistant graphique, terminal |  |
| **bmaptool** 🔒 | copie rapide d'une image vers un disque avec carte des blocs ; create génère la carte, copy écrase la destination — assistant : Créer une carte de blocs ou copier son image | 🔴 rouge | assistant graphique, terminal |  |
| **btrfs-image** 🔒 | copie les métadonnées Btrfs dans un fichier image pour analyse — assistant : Exporter les métadonnées Btrfs | 🟠 orange | assistant graphique, terminal |  |
| **Clonezilla** 🔒 | cloner ou restaurer un disque sain — assistant : Sauvegarder avec Clonezilla | 🟠 orange | assistant graphique, terminal plein écran |  |
| **dc3dd** 🔒 | copie brute avec empreintes — assistant : Copier avec empreintes dc3dd | 🟠 orange | assistant graphique, terminal |  |
| **dd** 🔒 | copie brute ; inverser if et of est catastrophique — assistant : Copier des octets avec dd | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/dd.md) |
| **ddrescuelog** | lire un mapfile — assistant : Lire une carte GNU ddrescue | 🟢 vert | assistant graphique, terminal | [fiche](fiches/ddrescuelog.md) |
| **DDRescueView** | voir un mapfile | 🟢 vert | fenêtre |  |
| **ddru_ntfsbitmap** 🔒 | fichier de domaine NTFS pour ddrescue : ne copier que les clusters utilisés — assistant : Créer un domaine ddrescue pour NTFS | 🟠 orange | assistant graphique, terminal |  |
| **ddru_ntfsfindbad** 🔒 | fichiers NTFS touchés par les secteurs illisibles d'un mapfile — assistant : Relier les erreurs ddrescue aux fichiers NTFS | 🟠 orange | assistant graphique, terminal |  |
| **ddrutility** 🔒 | fichiers touchés par les secteurs illisibles — assistant : Relier les erreurs aux fichiers d’une image | 🟠 orange | assistant graphique, terminal |  |
| **e2image** 🔒 | sauvegarder les métadonnées ext2/3/4 dans un fichier image, -r ou -Q ; -I les réécrit sur le disque — assistant : Sauver ou restaurer les métadonnées ext | 🔴 rouge | assistant graphique, terminal |  |
| **ewf-tools : ewfacquire, ewfinfo, ewfmount** 🔒 | images EWF — assistant : Acquérir une image forensique EWF | 🟠 orange | assistant graphique, terminal |  |
| **ewfinfo** | métadonnées d'une image EWF/E01 : taille, hachages, notes d'acquisition — assistant : Lire les métadonnées EWF | 🟢 vert | assistant graphique, terminal |  |
| **ewfmount** 🔒 | monte une image EWF/E01 en lecture seule via FUSE, démonter avec umount — assistant : Ouvrir une image EWF en lecture seule | 🟢 vert | assistant graphique, terminal |  |
| **ewfverify** | vérifie l'intégrité d'une image EWF/E01 en recalculant ses hachages — assistant : Recalculer l’intégrité d’une image EWF | 🟡 jaune | assistant graphique, terminal |  |
| **exfat2img** 🔒 | copie les métadonnées exFAT vers une image avec -o ; sait aussi restaurer une image sur une partition — assistant : Sauver ou restaurer les métadonnées exFAT | 🔴 rouge | assistant graphique, terminal |  |
| **FSArchiver** 🔒 | archive de systèmes de fichiers — assistant : Archiver ou restaurer un système de fichiers | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/fsarchiver.md) |
| **GNU ddrescue** 🔒 | cloner un disque défaillant, avec mapfile — assistant : Cloner avec GNU ddrescue | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/ddrescue.md) |
| **Guymager** 🔒 | acquisition forensic en image dd, E01 ou AFF avec hachages MD5/SHA, source lue sans écriture | 🟠 orange | fenêtre |  |
| **hashdeep** | empreintes récursives d'une arborescence, -r ; audit d'une copie par rapport à une liste avec -a -k liste.txt, sans rien écrire sur la source — assistant : Comparer une arborescence avec ses empreintes | 🟡 jaune | assistant graphique, terminal |  |
| **kpartx -r** 🔒 | partitions d'une image, en lecture seule — assistant : Lire ou exposer les partitions d’une image | 🟢 vert | assistant graphique, terminal |  |
| **losetup -r** 🔒 | présenter une image comme un disque, en lecture seule — assistant : Présenter une image en lecture seule | 🟢 vert | assistant graphique, terminal | [fiche](fiches/losetup.md) |
| **myrescue** 🔒 | copie à erreurs, historique — assistant : Copier avec le moteur historique myrescue | 🟠 orange | assistant graphique, terminal |  |
| **myrescue-stat** 🔒 | bilan des blocs copiés, lents ou en échec d'un fichier de suivi myrescue — assistant : Lire le suivi d’une copie myrescue | 🟢 vert | assistant graphique, terminal |  |
| **ntfsclone** 🔒 | copie d'un NTFS sain — assistant : Sauvegarder ou restaurer un NTFS sain | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/ntfsclone.md) |
| **ocs-chkimg** 🔒 | vérifier qu'une image Clonezilla est restaurable, sans toucher aux disques — assistant : Vérifier une image Clonezilla | 🟡 jaune | assistant graphique, terminal |  |
| **ocs-onthefly** 🔒 | clonage direct disque à disque ; -f source -d cible, la cible est écrasée — assistant : Cloner localement un disque sain vers sa copie | 🔴 rouge | assistant graphique, terminal |  |
| **ocs-sr** 🔒 | sauvegarde Clonezilla en ligne de commande : savedisk/saveparts ; restoredisk écrase le disque cible — assistant : Sauvegarder ou restaurer une image Clonezilla | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/ocs-sr.md) |
| **OpenSuperClone** 🔒 | clonage d'un disque malade, modes « passthrough » ; sans son pilote noyau | 🟠 orange | fenêtre |  |
| **OSCViewer** | voir le journal d'un clonage OpenSuperClone | 🟢 vert | fenêtre |  |
| **Partclone** 🔒 | blocs utilisés d'une partition : .ntfs, .ext4, .fat... — assistant : Sauvegarder une partition NTFS avec Partclone | 🟠 orange | assistant graphique, terminal |  |
| **partclone.chkimg** 🔒 | vérifie l'intégrité d'une image Partclone, en lecture seule — assistant : Vérifier une image Partclone | 🟡 jaune | assistant graphique, terminal |  |
| **partclone.info** 🔒 | affiche l'en-tête d'une image Partclone : système de fichiers, taille, blocs utilisés — assistant : Lire l’en-tête d’une image Partclone | 🟢 vert | assistant graphique, terminal |  |
| **partclone.restore** 🔒 | restaure une image sur une partition, qui est écrasée ; vérifier -o deux fois — assistant : Restaurer une image Partclone sur une copie | 🔴 rouge | assistant graphique, terminal |  |
| **Partimage** 🔒 | sauvegarde de partitions, historique — assistant : Sauvegarder une partition avec Partimage | 🔴 rouge | assistant graphique, terminal plein écran |  |
| **pv** | suivre un transfert — assistant : Copier un fichier en suivant son transfert | 🟠 orange | assistant graphique, terminal | [fiche](fiches/pv.md) |
| **rescue-clone** 🔒 | assistant ddrescue : trois phases, mapfile hors de la source, reprise, garde-fous, empreinte — assistant : Cloner et reprendre avec Saint-Bernard | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/rescue-clone.md) |
| **rhash** | sommes de contrôle multiples, -c pour vérifier une liste — assistant : Calculer ou vérifier des sommes de contrôle | 🟢 vert | assistant graphique, terminal |  |
| **safecopy** 🔒 | copie à erreurs, historique — assistant : Copier avec le moteur historique safecopy | 🟠 orange | assistant graphique, terminal |  |
| **sha256sum, hashdeep** | empreintes — assistant : Calculer une empreinte SHA-256 | 🟢 vert | assistant graphique, terminal | [fiche](fiches/sha256sum.md) |
| **xxhsum** | empreintes rapides XXH3 et XXH128 pour comparer de gros fichiers ; pas une preuve, garder SHA-256 — assistant : Comparer rapidement les empreintes XXH | 🟢 vert | assistant graphique, terminal |  |

## Images et machines virtuelles

| Outil | Ce qu'il fait | Risque | S'ouvre | Fiche pratique |
|---|---|---|---|---|
| **guestfish** 🔒 | shell d'examen et de modification hors ligne des images de VM et disques, --ro pour lire sans écrire — assistant : Examiner les systèmes de fichiers d’une image hors ligne | 🔴 rouge | assistant graphique, terminal |  |
| **guestmount** 🔒 | monter le contenu d'une image de machine virtuelle ; toujours avec --ro — assistant : Monter le contenu d’une image avec libguestfs en lecture seule | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/guestmount.md) |
| **libguestfs-test-tool** 🔒 | vérifie que libguestfs démarre sa petite machine virtuelle ; plusieurs minutes sans virtualisation matérielle — assistant : Diagnostiquer le démarrage de libguestfs | 🟢 vert | assistant graphique, terminal |  |
| **mksquashfs** | créer une image SquashFS compressée sur une destination — assistant : Créer une image SquashFS sur une autre destination | 🟠 orange | assistant graphique, terminal |  |
| **nbdkit** | serveur NBD à greffons pour images ; écoute par défaut sur toutes les interfaces, port 10809, en écriture : -r pour la lecture seule, --filter=cow pour écrire dans un calque jetable — assistant : Servir une image brute sur un socket privé | 🟠 orange | assistant graphique, terminal |  |
| **qemu-img** | images disque virtuelles : info, check sans -r, convert ; check -r, resize, amend, commit modifient l'image — assistant : Examiner et convertir une image virtuelle | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/qemu-img.md) |
| **qemu-nbd** 🔒 | exposer une image virtuelle en /dev/nbd ; ajouter --read-only pour ne rien écrire — assistant : Exposer une image par NBD local en lecture seule | 🟠 orange | assistant graphique, terminal | [fiche](fiches/qemu-nbd.md) |
| **unsquashfs** | lister ou extraire une image SquashFS, -l pour lister sans extraire — assistant : Lire ou extraire une image SquashFS | 🟠 orange | assistant graphique, terminal |  |
| **vhdiinfo, vhdimount** | images VHD/VHDX Hyper-V, lecture seule — assistant : Examiner une image Hyper-V VHD ou VHDX | 🟢 vert | assistant graphique, terminal |  |
| **virt-filesystems** 🔒 | liste partitions, LVM et systèmes de fichiers d'une image de VM ou d'un disque, lecture seule — assistant : Inventorier partitions et volumes d’une image de VM | 🟢 vert | assistant graphique, terminal | [fiche](fiches/virt-filesystems.md) |
| **virt-rescue** 🔒 | shell de secours dans une image de VM ou un disque, --ro pour ne rien modifier — assistant : Ouvrir un shell de secours avec source protégée | 🔴 rouge | assistant graphique, terminal |  |
| **vmdkinfo** | informations sur une image disque VMware VMDK — assistant : Lire les informations d’une image VMware autonome | 🟢 vert | assistant graphique, terminal |  |
| **vmdkmount** 🔒 | expose une image VMware VMDK en lecture seule via FUSE — assistant : Exposer une image VMware en lecture seule | 🟢 vert | assistant graphique, terminal |  |

## Récupération de fichiers

| Outil | Ce qu'il fait | Risque | S'ouvre | Fiche pratique |
|---|---|---|---|---|
| **7-Zip** | ouvrir les archives récupérées : 7z, zip, rar, iso ; extraire vers la destination — assistant : Examiner ou extraire une archive récupérée | 🟠 orange | assistant graphique, terminal |  |
| **binwalk** | structures dans un fichier binaire — assistant : Identifier les structures d’un fichier binaire | 🟢 vert | assistant graphique, terminal |  |
| **btrfs-find-root** 🔒 | cherche d'anciennes racines Btrfs pour btrfs restore -t, lecture seule — assistant : Rechercher d’anciennes racines Btrfs | 🟡 jaune | assistant graphique, terminal |  |
| **cabextract** | archives CAB de Windows ; extraire vers la destination — assistant : Extraire une archive Windows CAB | 🟠 orange | assistant graphique, terminal |  |
| **dislocker-file** 🔒 | déchiffre un volume BitLocker vers un fichier image NTFS sur une destination — assistant : Déchiffrer BitLocker vers une image NTFS | 🟠 orange | assistant graphique, terminal |  |
| **dupemap** | repère les doublons parmi les fichiers récupérés ; « report » liste sans rien toucher, « delete » efface les doublons — assistant : Repérer les doublons sans suppression | 🔴 rouge | assistant graphique, terminal |  |
| **e2cp** 🔒 | copier des fichiers hors d'un volume ext2/3/4 non monté vers une destination ; ne jamais copier vers le volume source — assistant : Extraire un fichier ext sans montage | 🟠 orange | assistant graphique, terminal |  |
| **ext3grep** 🔒 | ext3 ; ancien — assistant : Explorer les anciens journaux ext3 | 🟠 orange | assistant graphique, terminal |  |
| **ext4magic** 🔒 | ext3, ext4 par le journal — assistant : Récupérer les fichiers par le journal ext | 🟠 orange | assistant graphique, terminal |  |
| **extundelete** 🔒 | ext3, ext4 ; ancien — assistant : Récupérer les fichiers ext avec extundelete | 🟠 orange | assistant graphique, terminal | [fiche](fiches/extundelete.md) |
| **fatcat** 🔒 | explorer une FAT abîmée ; -z, -S, -m, -p, -w, -f et -e écrivent dans le volume : sur une copie seulement — assistant : Explorer ou extraire une FAT endommagée | 🟠 orange | assistant graphique, terminal |  |
| **fidentify** | identifie le vrai type des fichiers récupérés par PhotoRec, lecture seule — assistant : Identifier le type réel d’un fichier | 🟠 orange | assistant graphique, terminal |  |
| **Findoid** 🔒 | liste les versions d'un fichier dans les instantanés ZFS, lecture seule — assistant : Lister les versions d’un fichier dans ZFS | 🟢 vert | assistant graphique, terminal |  |
| **Foremost** 🔒 | fichiers par signatures — assistant : Extraire des signatures avec Foremost | 🟠 orange | assistant graphique, terminal | [fiche](fiches/foremost.md) |
| **GHex** 🔒 | éditeur hexadécimal graphique ; écrit dans le fichier ou le disque ouvert à l'enregistrement | 🔴 rouge | fenêtre |  |
| **hexdump** | vue hexadécimale en lecture seule ; -C pour l'affichage canonique, -s/-n pour lire un secteur précis — assistant : Lire un fichier avec hexdump | 🟢 vert | assistant graphique, terminal |  |
| **hexedit** 🔒 | éditeur hexadécimal ; écrit dans le fichier ouvert — assistant : Éditer une copie de fichier en hexadécimal | 🔴 rouge | assistant graphique, terminal |  |
| **MagicRescue** 🔒 | signatures par recettes — assistant : Extraire des images avec MagicRescue | 🟠 orange | assistant graphique, terminal |  |
| **magicsort** | range par type les fichiers récupérés, en les déplaçant dans des sous-dossiers du dossier donné — assistant : Classer une copie des fichiers récupérés | 🟠 orange | assistant graphique, terminal |  |
| **mcopy** 🔒 | copier des fichiers d'un volume FAT sans le monter, ex. mcopy -i /dev/sdX1 -s :: /destination — assistant : Copier les fichiers FAT sans montage | 🟠 orange | assistant graphique, terminal |  |
| **ntfscat** 🔒 | lire un fichier d'un NTFS non monté vers la sortie standard, à rediriger — assistant : Extraire un fichier d’un NTFS non monté | 🟠 orange | assistant graphique, terminal |  |
| **ntfsundelete** 🔒 | fichiers supprimés sur NTFS — assistant : Rechercher des fichiers supprimés sur NTFS | 🟠 orange | assistant graphique, terminal | [fiche](fiches/ntfsundelete.md) |
| **PhotoRec** 🔒 | fichiers retrouvés par signatures — assistant : Récupérer par signatures avec PhotoRec | 🟠 orange | assistant graphique, terminal plein écran | [fiche](fiches/photorec.md) |
| **QPhotoRec** 🔒 | PhotoRec en fenêtre : fichiers retrouvés par signatures | 🟠 orange | fenêtre |  |
| **recoverjpeg, recovermov** 🔒 | photos et vidéos — assistant : Extraire les photographies JPEG | 🟠 orange | assistant graphique, terminal |  |
| **recovermov** 🔒 | récupération de vidéos MOV/QuickTime : lit le disque ou l'image, écrit les fichiers dans le dossier courant ou -o — assistant : Extraire les vidéos MOV ou QuickTime | 🟠 orange | assistant graphique, terminal |  |
| **rescue-recover** 🔒 | PhotoRec ou TestDisk avec garde-fous : fichiers jamais sur le disque source ni en mémoire ; de préférence sur l'image clonée — assistant : Récupérer avec les garde-fous Saint-Bernard | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/rescue-recover.md) |
| **Scalpel** 🔒 | signatures configurables — assistant : Extraire des signatures avec Scalpel | 🟠 orange | assistant graphique, terminal |  |
| **TestDisk** 🔒 | partitions perdues ; analyse sans risque, écrit la table seulement si on le valide — assistant : Analyser les partitions avec TestDisk | 🔴 rouge | assistant graphique, terminal plein écran | [fiche](fiches/testdisk.md) |
| **The Sleuth Kit : fls, icat, fsstat** 🔒 | analyser une image — assistant : Inventorier une image avec The Sleuth Kit | 🟢 vert | assistant graphique, terminal | [fiche](fiches/fls.md) |
| **The Sleuth Kit : istat** 🔒 | métadonnées d'un inode : propriétaire, droits, taille, dates, blocs occupés — assistant : Lire les métadonnées d’un inode | 🟢 vert | assistant graphique, terminal |  |
| **The Sleuth Kit : mmls** 🔒 | table de partitions d'une image — assistant : Lire les partitions d’une image | 🟢 vert | assistant graphique, terminal | [fiche](fiches/mmls.md) |
| **The Sleuth Kit : tsk_recover** 🔒 | copier les fichiers supprimés d'une image ou d'un disque vers un dossier ; -e tous les fichiers, -a les seuls fichiers présents — assistant : Extraire les fichiers d’une image avec TSK | 🟠 orange | assistant graphique, terminal | [fiche](fiches/tsk_recover.md) |
| **xxd** | vue hexadécimale — assistant : Lire un fichier avec xxd | 🟢 vert | assistant graphique, terminal |  |

## Windows, macOS et analyse

| Outil | Ce qu'il fait | Risque | S'ouvre | Fiche pratique |
|---|---|---|---|---|
| **Autopsy** 🔒 | enquête numérique sur une image disque via le navigateur, http://localhost:9999/autopsy ; laisser le terminal ouvert, travailler sur une copie en lecture seule — assistant : Démarrer une analyse Autopsy locale | 🟡 jaune | assistant graphique, terminal |  |
| **disktype** 🔒 | identifier le contenu d'un disque ou d'une image : tables de partitions, systèmes de fichiers, codes de démarrage, en lecture seule — assistant : Identifier un disque ou une image — disktype | 🟢 vert | assistant graphique, terminal | [fiche](fiches/disktype.md) |
| **fsapfsmount** 🔒 | monte un conteneur APFS macOS en lecture seule via FUSE ; -f n° de volume, -p mot de passe, -r clé de secours si chiffré — assistant : Monter APFS en lecture seule | 🟢 vert | assistant graphique, terminal |  |
| **fsntfsinfo** 🔒 | analyse bas niveau d'un NTFS : MFT, arborescence, journal USN ; lecture seule — assistant : Analyser les métadonnées NTFS | 🟢 vert | assistant graphique, terminal |  |
| **fsntfsmount** 🔒 | monter un NTFS ou son image par FUSE, en lecture seule — assistant : NTFS via FUSE en lecture seule | 🟢 vert | assistant graphique, terminal |  |
| **Okteta** | éditeur hexadécimal graphique ; enregistrer écrase le fichier ouvert : travailler sur une copie | 🔴 rouge | fenêtre |  |
| **plaso-log2timeline** 🔒 | chronologie forensique d'une image ou d'un disque, écrit un fichier .plaso sur la destination — assistant : Créer une chronologie Plaso | 🟠 orange | assistant graphique, terminal |  |
| **plaso-pinfo** 🔒 | résumé d'un fichier .plaso, lecture seule — assistant : Examiner un fichier Plaso | 🟢 vert | assistant graphique, terminal |  |
| **plaso-psort** 🔒 | trie et exporte une chronologie .plaso en CSV ou texte — assistant : Exporter une chronologie Plaso | 🟠 orange | assistant graphique, terminal |  |
| **vshadowinfo, vshadowmount** 🔒 | clichés VSS Windows, lecture seule — assistant : Clichés VSS Windows en lecture seule | 🟢 vert | assistant graphique, terminal |  |
| **wimlib** | images WIM de Windows : wiminfo lit ; wimapply et wimextract écrivent sur la destination — assistant : Explorer et extraire une image WIM | 🟠 orange | assistant graphique, terminal | [fiche](fiches/wimlib-imagex.md) |

## Partitions et volumes

| Outil | Ce qu'il fait | Risque | S'ouvre | Fiche pratique |
|---|---|---|---|---|
| **APFS : fsapfsinfo, fsapfsmount** 🔒 | lecture seule — assistant : APFS en lecture seule | 🟢 vert | assistant graphique, terminal |  |
| **bdeinfo, bdemount** 🔒 | BitLocker, lecture seule — assistant : Métadonnées BitLocker — bdeinfo | 🟢 vert | assistant graphique, terminal |  |
| **bdemount** 🔒 | montage FUSE d'un volume BitLocker en lecture seule, avec -p mot de passe ou -r clé de récupération — assistant : Ouvrir BitLocker — bdemount | 🟢 vert | assistant graphique, terminal |  |
| **cfdisk** 🔒 | éditeur plein écran de tables de partitions, rien n'est écrit avant « Écrire » — assistant : Éditeur de partitions — cfdisk | 🔴 rouge | assistant graphique, terminal plein écran |  |
| **cgdisk** 🔒 | partitionnement GPT plein écran, rien n'est écrit avant Write — assistant : Éditeur GPT — cgdisk | 🔴 rouge | assistant graphique, terminal plein écran |  |
| **cryptsetup : luksDump, open --readonly** 🔒 | LUKS — assistant : LUKS en lecture seule — cryptsetup | 🟢 vert | assistant graphique, terminal | [fiche](fiches/cryptsetup.md) |
| **dislocker** 🔒 | BitLocker — assistant : BitLocker en lecture seule — dislocker | 🟢 vert | assistant graphique, terminal | [fiche](fiches/dislocker.md) |
| **dislocker-metadata** 🔒 | métadonnées BitLocker : protecteurs, chiffrement, sans déchiffrer — assistant : Métadonnées BitLocker — dislocker | 🟢 vert | assistant graphique, terminal |  |
| **dmsetup** 🔒 | mappages device-mapper : ls --tree, info, table pour examiner ; remove, wipe_table et create modifient — assistant : Examiner et retirer une carte — dmsetup | 🔴 rouge | assistant graphique, terminal |  |
| **ecryptfs-recover-private** 🔒 | ouvre en lecture seule le dossier personnel chiffré eCryptfs d'une ancienne Ubuntu, avec son mot de passe — assistant : Dossier chiffré eCryptfs | 🟢 vert | assistant graphique, terminal |  |
| **fdisk, cfdisk** 🔒 | tables de partitions — assistant : lire ou créer une table GPT ou MBR vide | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/fdisk.md) |
| **findmnt** | montages en cours et leurs options, vérifier le mode ro — assistant : Vérifier les montages — findmnt | 🟢 vert | assistant graphique, terminal |  |
| **fixparts** 🔒 | réparation interactive de tables MBR corrompues, retrait de restes GPT — assistant : Réparer une MBR — fixparts | 🔴 rouge | assistant graphique, terminal |  |
| **fvdeinfo** 🔒 | FileVault 2 / CoreStorage : informations sur le volume chiffré — assistant : Métadonnées FileVault 2 — fvdeinfo | 🟢 vert | assistant graphique, terminal |  |
| **fvdemount** 🔒 | FileVault 2 / CoreStorage : déverrouillage et montage FUSE en lecture seule — assistant : Ouvrir FileVault 2 — fvdemount | 🟢 vert | assistant graphique, terminal |  |
| **gdisk** 🔒 | éditeur interactif de table GPT, conversion MBR vers GPT ; gdisk -l pour lister sans écrire, rien n'est écrit avant la commande w — assistant : examiner et convertir une table sur le clone | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/gdisk.md) |
| **gdisk, sgdisk** 🔒 | tables GPT — assistant : vérifier, sauvegarder et restaurer une GPT | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/sgdisk.md) |
| **gpart** 🔒 | devine une table de partitions perdue en lisant tout le disque ; n'écrit qu'avec -W — assistant : Rechercher les partitions — gpart | 🟡 jaune | assistant graphique, terminal |  |
| **GParted** 🔒 | partitions, interface graphique | 🔴 rouge | fenêtre |  |
| **growpart** 🔒 | agrandir une partition jusqu'à l'espace libre qui la suit, sans toucher au système de fichiers ; --dry-run pour simuler — assistant : Agrandir une partition — growpart | 🔴 rouge | assistant graphique, terminal |  |
| **HFS+ sans montage : hpmount, hpls, hpcopy** 🔒 | HFS+ sans montage système | 🟢 vert | assistant graphique, terminal |  |
| **KDE Partition Manager** 🔒 | partitions, interface graphique KDE ; rien n'est écrit avant « Appliquer » | 🔴 rouge | fenêtre |  |
| **ldmtool** 🔒 | disques dynamiques Windows : ldmtool scan pour lister ; create expose les volumes en device-mapper, à monter ensuite en lecture seule — assistant : Examiner les disques dynamiques Windows | 🟢 vert | assistant graphique, terminal |  |
| **LVM : pvs, vgs, lvs** 🔒 | examiner — assistant : Examiner LVM — pvs, vgs, lvs | 🟢 vert | assistant graphique, terminal | [fiche](fiches/pvs.md) |
| **mdadm --examine** 🔒 | RAID logiciel ; ne rien assembler de force — assistant : examiner les membres RAID sans assemblage | 🟢 vert | assistant graphique, terminal | [fiche](fiches/mdadm.md) |
| **multipath -ll** 🔒 | chemins multiples SAN/SAS, lecture ; sans option, crée les cartes device-mapper — assistant : Examiner les chemins multiples | 🟢 vert | assistant graphique, terminal |  |
| **ntfsresize** 🔒 | redimensionner un NTFS ; --info et --no-action pour simuler sans écrire — assistant : Taille du système NTFS — ntfsresize | 🔴 rouge | assistant graphique, terminal |  |
| **parted** 🔒 | tables de partitions — assistant : lire ou créer une table GPT ou MBR vide | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/parted.md) |
| **partprobe** 🔒 | faire relire au noyau la table de partitions, -d pour simuler, -s pour un résumé — assistant : Relire la table — partprobe | 🟢 vert | assistant graphique, terminal |  |
| **pvck** 🔒 | vérifier les métadonnées LVM d'un volume physique, sans rien écrire ; --dump -f les extrait vers un fichier de destination — assistant : Vérifier et réparer un PV — pvck | 🔴 rouge | assistant graphique, terminal |  |
| **rescue-mount** 🔒 | monte en lecture seule sans rejouer de journal ; ouvre LUKS, BitLocker, LVM, RAID, ZFS et les images ; --ecriture pour une destination — assistant : Ouvrir en lecture seule — rescue-mount | 🟢 vert | assistant graphique, terminal | [fiche](fiches/rescue-mount.md) |
| **rescue-ro** 🔒 | remet un disque en lecture seule ; --liste, --tous — assistant : Remettre en lecture seule — rescue-ro | 🟢 vert | assistant graphique, terminal | [fiche](fiches/rescue-ro.md) |
| **rescue-rw** 🔒 | autorise l'écriture sur un disque : nom retapé, journalisé ; jamais sur un disque à récupérer — assistant : autoriser l'écriture sur une destination | 🟠 orange | assistant graphique, terminal | [fiche](fiches/rescue-rw.md) |
| **rescue-umount** 🔒 | démonte et referme ce que rescue-mount a ouvert ; --tous — assistant : Refermer les volumes — rescue-umount | 🟢 vert | assistant graphique, terminal | [fiche](fiches/rescue-umount.md) |
| **sfdisk --dump** 🔒 | sauvegarder une table de partitions — assistant : lire et sauvegarder une table en texte | 🟢 vert | assistant graphique, terminal | [fiche](fiches/sfdisk.md) |
| **thin_check** 🔒 | vérifier les métadonnées d'un pool LVM-thin, sans rien écrire — assistant : Vérifier et corriger LVM-thin | 🔴 rouge | assistant graphique, terminal |  |
| **thin_dump** 🔒 | exporter les métadonnées LVM-thin en XML, vers un fichier avec -o — assistant : Exporter les métadonnées LVM-thin | 🟠 orange | assistant graphique, terminal |  |
| **thin_repair** 🔒 | réparer les métadonnées LVM-thin, écrit sur la cible -o — assistant : Réparer vers une cible LVM-thin | 🔴 rouge | assistant graphique, terminal |  |
| **vgcfgbackup** 🔒 | sauvegarder les métadonnées d'un groupe de volumes, -f fichier vers une clé externe — assistant : Sauvegarder les métadonnées LVM | 🟠 orange | assistant graphique, terminal |  |
| **vgcfgrestore** 🔒 | restaurer les métadonnées LVM, --test pour simuler sans écrire — assistant : Restaurer les métadonnées LVM | 🔴 rouge | assistant graphique, terminal |  |
| **vslvminfo** 🔒 | métadonnées LVM d'un disque ou d'une image, lecture seule — assistant : Métadonnées LVM sans activation | 🟢 vert | assistant graphique, terminal |  |
| **vslvmmount** 🔒 | expose les volumes logiques LVM via FUSE, lecture seule, sans activer LVM — assistant : Volumes LVM via FUSE | 🟢 vert | assistant graphique, terminal |  |
| **zpool, zfs, zdb** 🔒 | ZFS : importer à la main avec zpool import -o readonly=on — assistant : ZFS en lecture seule — zpool | 🟢 vert | assistant graphique, terminal | [fiche](fiches/zpool.md) |

## Systèmes de fichiers

| Outil | Ce qu'il fait | Risque | S'ouvre | Fiche pratique |
|---|---|---|---|---|
| **APFS : apfsck** 🔒 | vérification seule — assistant : Vérifier un conteneur APFS | 🟢 vert | assistant graphique, terminal |  |
| **btrfs** 🔒 | Btrfs : btrfs check --readonly pour vérifier, btrfs restore pour extraire vers un autre disque — assistant : Vérifier ou extraire un volume Btrfs | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/btrfs.md) |
| **debugfs** 🔒 | explorer un ext2/3/4 et extraire des fichiers avec rdump ; lecture seule sans -w — assistant : Explorer ou extraire un volume ext | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/debugfs.md) |
| **debugreiserfs** 🔒 | outil de débogage ReiserFS : sans option, affiche le superbloc ; -u et les modes de corruption écrivent sur le périphérique — assistant : Lire le superbloc ReiserFS | 🔴 rouge | assistant graphique, terminal |  |
| **dump.exfat** 🔒 | affiche les informations exFAT du disque : secteur de démarrage, entrées de répertoire ; lecture seule — assistant : Examiner les structures exFAT | 🟢 vert | assistant graphique, terminal |  |
| **dump.f2fs** 🔒 | lecture des métadonnées F2FS : NAT, SIT, SSA, inodes ; extraction d'un fichier par numéro d'inode vers ./lost_found du dossier courant, sans écrire sur le disque source — assistant : Exporter les structures F2FS | 🟠 orange | assistant graphique, terminal |  |
| **e2ls** 🔒 | lister un volume ou une image ext2/3/4 sans le monter, ex. e2ls -l /dev/sdb1:/home — assistant : Lister les fichiers ext sans montage | 🟢 vert | assistant graphique, terminal |  |
| **EROFS : dump.erofs** 🔒 | superbloc, statistiques, inodes et fichiers, lecture seule — assistant : Examiner les métadonnées EROFS | 🟢 vert | assistant graphique, terminal |  |
| **EROFS : fsck.erofs** 🔒 | vérification d'intégrité sans réparation ; --extract=DOSSIER extrait le contenu vers un dossier — assistant : Vérifier ou extraire un volume EROFS | 🟠 orange | assistant graphique, terminal |  |
| **exFAT : fsck.exfat** 🔒 | -n pour vérifier sans écrire — assistant : Vérifier un volume exFAT | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/fsck.exfat.md) |
| **exfatlabel** 🔒 | lit le nom ou le numéro de série d'un volume exFAT ; l'écrit si une valeur est donnée — assistant : Lire le nom du volume exFAT | 🔴 rouge | assistant graphique, terminal |  |
| **ext2/3/4 : dumpe2fs, debugfs** 🔒 | examiner — assistant : Lire les métadonnées ext | 🟢 vert | assistant graphique, terminal | [fiche](fiches/dumpe2fs.md) |
| **ext2/3/4 : e2fsck** 🔒 | -fn pour vérifier sans écrire — assistant : Vérifier un volume ext2, ext3 ou ext4 | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/e2fsck.md) |
| **F2FS : fsck.f2fs** 🔒 | Vérifier un volume F2FS | 🔴 rouge | assistant graphique, terminal |  |
| **FAT : fsck.fat** 🔒 | -n pour vérifier sans écrire — assistant : Vérifier un volume FAT | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/fsck.fat.md) |
| **fatlabel** 🔒 | lit ou change le nom de volume FAT ; sans nouveau nom, lit seulement — assistant : Lire le nom du volume FAT | 🔴 rouge | assistant graphique, terminal |  |
| **HFS+ : fsck.hfsplus** 🔒 | -n pour vérifier sans écrire — assistant : Vérifier un volume HFS+ | 🔴 rouge | assistant graphique, terminal |  |
| **JFS : fsck.jfs** 🔒 | Vérifier un volume JFS | 🔴 rouge | assistant graphique, terminal |  |
| **jfs_debugfs** 🔒 | éditeur JFS bas niveau interactif, peut écrire sur le disque : consulter seulement — assistant : Consulter les structures JFS protégées | 🔴 rouge | assistant graphique, terminal |  |
| **jfs_tune** 🔒 | réglages JFS : -l affiche le superbloc ; -L, -U, -J modifient étiquette, UUID, journal — assistant : Lire le superbloc JFS | 🔴 rouge | assistant graphique, terminal |  |
| **lsbtr** 🔒 | lister les sous-volumes Btrfs et leurs points de montage, lecture seule — assistant : Lister les sous-volumes Btrfs montés | 🟢 vert | assistant graphique, terminal |  |
| **mdir** 🔒 | lister un volume FAT sans le monter, ex. mdir -i /dev/sdX1 -/ :: — assistant : Lister les fichiers FAT sans montage | 🟢 vert | assistant graphique, terminal |  |
| **minfo** 🔒 | paramètres d'un volume FAT sans le monter, ex. minfo -i /dev/sdX1 :: — assistant : Lire les paramètres FAT sans montage | 🟢 vert | assistant graphique, terminal |  |
| **mkfs** 🔒 | formater : mkfs.ext4, mkfs.vfat, mkfs.exfat, mkfs.ntfs, mkfs.xfs, mkfs.btrfs — assistant : Formater une copie en ext4 | 🔴 rouge | assistant graphique, terminal |  |
| **NILFS2 : chcp** 🔒 | fige un point de reprise en instantané « ss », montable ensuite avec -o ro,cp=N ; « cp » le rend effaçable — assistant : Conserver un point de reprise NILFS2 | 🔴 rouge | assistant graphique, terminal |  |
| **NILFS2 : lscp** 🔒 | liste les points de reprise et instantanés d'un volume monté, pour retrouver d'anciennes versions — assistant : Lire les points de reprise NILFS2 | 🟢 vert | assistant graphique, terminal |  |
| **NILFS2 : nilfs-tune** 🔒 | -l pour lire le superbloc sans écrire ; les autres options modifient — assistant : Lire le superbloc NILFS2 | 🔴 rouge | assistant graphique, terminal |  |
| **NTFS : ntfsfix** 🔒 | correctifs limités, pas un chkdsk — assistant : Contrôler les correctifs NTFS limités | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/ntfsfix.md) |
| **NTFS : ntfsinfo, ntfsls** 🔒 | examiner sans monter — assistant : Examiner un volume NTFS | 🟢 vert | assistant graphique, terminal |  |
| **ntfscluster** 🔒 | quels fichiers occupent une plage de secteurs ou de clusters, lecture seule — assistant : Rechercher les fichiers d’une plage NTFS | 🟢 vert | assistant graphique, terminal |  |
| **ReiserFS : reiserfsck** 🔒 | Vérifier un volume ReiserFS | 🔴 rouge | assistant graphique, terminal |  |
| **rescue-fsck** 🔒 | vérification sans écriture du guide 09, partition par partition ; --reparer sur une copie de travail seulement, nom retapé : rouge — assistant : Vérifier les systèmes de fichiers | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/rescue-fsck.md) |
| **tune2fs** 🔒 | réglages ext2/3/4 ; -l pour lire le superbloc sans écrire — assistant : Lire les réglages ext | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/tune2fs.md) |
| **UDF : mkudffs, udflabel** 🔒 | formater ou renommer un volume UDF — assistant : Formater une copie en UDF | 🔴 rouge | assistant graphique, terminal |  |
| **UDF : udfinfo** 🔒 | lire étiquette, révision et espace d'un volume UDF, DVD ou disque — assistant : Lire les paramètres UDF | 🟢 vert | assistant graphique, terminal |  |
| **XFS : xfs_info** 🔒 | géométrie et paramètres d'un système de fichiers XFS — assistant : Lire la géométrie XFS | 🟢 vert | assistant graphique, terminal |  |
| **XFS : xfs_metadump** 🔒 | copie des métadonnées XFS vers un fichier image, -o pour ne pas masquer les noms — assistant : Exporter les métadonnées XFS | 🟠 orange | assistant graphique, terminal |  |
| **XFS : xfs_repair** 🔒 | -n pour vérifier sans écrire — assistant : Vérifier une copie XFS | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/xfs_repair.md) |
| **XFS : xfs_scrub** 🔒 | inutilisable dans Saint-Bernard : le noyau Debian n'a pas la vérification en ligne XFS ; utiliser xfs_repair -n — assistant : Vérifier la disponibilité du contrôle XFS en ligne | 🔴 rouge | assistant graphique, terminal |  |
| **zdb** 🔒 | diagnostic bas niveau d'un pool ZFS, lecture seule ; -e pour un pool non importé — assistant : Examiner les étiquettes ZFS | 🟡 jaune | assistant graphique, terminal |  |
| **zfs** 🔒 | jeux de données ZFS : zfs list et zfs get pour inventorier ; destroy et rollback modifient — assistant : Inventorier les jeux de données ZFS | 🔴 rouge | assistant graphique, terminal |  |

## Sauvegarde

| Outil | Ce qu'il fait | Risque | S'ouvre | Fiche pratique |
|---|---|---|---|---|
| **BorgBackup** 🔒 | sauvegarde dédupliquée et chiffrée vers un dépôt : borg init, borg create, borg extract ; --dry-run pour simuler create et extract — assistant : Sauvegarder et relire un dépôt Borg | 🟠 orange | assistant graphique, terminal | [fiche](fiches/borg.md) |
| **btrbk** 🔒 | instantanés et sauvegardes incrémentales Btrfs ; supprime les anciens selon la rétention ; crée un instantané sur la source : jamais sur un disque à sauver ; btrbk dryrun pour simuler — assistant : Sauvegarder des sous-volumes Btrfs sur des copies | 🔴 rouge | assistant graphique, terminal |  |
| **par2create** | crée des fichiers de parité PAR2 à côté d'une image ou d'une sauvegarde, -r10 pour 10 % — assistant : Créer une parité PAR2 sur une autre destination | 🟠 orange | assistant graphique, terminal |  |
| **par2repair** | répare des fichiers endommagés grâce à la parité PAR2, travailler sur une copie — assistant : Réparer une copie avec sa parité PAR2 | 🔴 rouge | assistant graphique, terminal |  |
| **par2verify** | vérifie des fichiers avec leurs blocs de parité PAR2, sans rien écrire — assistant : Vérifier des fichiers avec la parité PAR2 | 🟡 jaune | assistant graphique, terminal |  |
| **rclone** | copier les fichiers récupérés vers un stockage distant ou un cloud ; « copy » plutôt que « sync », --dry-run pour simuler — assistant : Copier sans synchronisation destructive avec Rclone | 🟠 orange | assistant graphique, terminal | [fiche](fiches/rclone.md) |
| **restic** 🔒 | sauvegarde chiffrée et dédupliquée vers un dépôt, snapshots/check pour vérifier — assistant : Sauvegarder et relire un dépôt Restic | 🟠 orange | assistant graphique, terminal | [fiche](fiches/restic.md) |
| **Syncoid** 🔒 | réplication d'un jeu de données ZFS vers un autre pool, local ou SSH ; la cible est ramenée au dernier instantané commun sauf --no-rollback ; --no-sync-snap pour ne pas créer d'instantané sur la source — assistant : Répliquer des instantanés ZFS locaux | 🔴 rouge | assistant graphique, terminal |  |
| **xfsdump** 🔒 | sauvegarde complète ou incrémentale d'un système de fichiers XFS vers un fichier, la source n'est que lue — assistant : Sauvegarder un volume XFS | 🟠 orange | assistant graphique, terminal |  |
| **xfsrestore** 🔒 | restauration d'une sauvegarde xfsdump vers un répertoire de destination, -t pour lister sans écrire — assistant : Lire et restaurer une sauvegarde XFS | 🟠 orange | assistant graphique, terminal |  |

## Démarrage et Windows

| Outil | Ce qu'il fait | Risque | S'ouvre | Fiche pratique |
|---|---|---|---|---|
| **chntpw** 🔒 | vider ou débloquer le mot de passe d'un compte Windows, avec l'accord du propriétaire ; ne peut pas en définir un nouveau — assistant : Lire un SAM ou éditer une copie avec Chntpw | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/chntpw.md) |
| **efibootdump** | décode les entrées de démarrage UEFI Boot####, lecture seule — assistant : Décoder un fichier d’entrée UEFI | 🟢 vert | assistant graphique, terminal |  |
| **efibootmgr** 🔒 | entrées de démarrage UEFI — assistant : Examiner et choisir le prochain démarrage UEFI | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/efibootmgr.md) |
| **extlinux, syslinux** 🔒 | amorçage — assistant : Installer Extlinux sur une copie Linux | 🔴 rouge | assistant graphique, terminal |  |
| **GRUB : grub-install** 🔒 | réinstaller le démarrage — assistant : Installer GRUB sur une copie identifiée | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/grub-install.md) |
| **grub-mkconfig** 🔒 | régénérer grub.cfg dans un chroot ; sans -o, affiche seulement — assistant : Lire ou régénérer GRUB dans la copie d’un Linux | 🔴 rouge | assistant graphique, terminal |  |
| **grub-mount** 🔒 | monter une partition en lecture seule avec les pilotes de GRUB — assistant : Monter un volume en lecture seule avec GRUB | 🟢 vert | assistant graphique, terminal |  |
| **grub-probe** 🔒 | identifier disque, système de fichiers et UUID vus par GRUB — assistant : Identifier un volume avec les pilotes GRUB | 🟢 vert | assistant graphique, terminal |  |
| **hivexsh, hivexget** 🔒 | lire le registre Windows — assistant : Lire une ruche du registre Windows | 🟢 vert | assistant graphique, terminal |  |
| **install-mbr** 🔒 | code du MBR — assistant : Installer le code MBR Linux sur une copie | 🔴 rouge | assistant graphique, terminal |  |
| **Installer Saint-Bernard sur un disque** | assistant : choix du disque, confirmations, BIOS et UEFI | 🔴 rouge | assistant graphique |  |
| **ms-sys** 🔒 | codes d'amorçage Microsoft : MBR, secteurs FAT et NTFS ; « ms-sys /dev/sdX » seul ne fait que lire — assistant : Lire ou réécrire le code MBR Microsoft sur une copie | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/ms-sys.md) |
| **os-prober** 🔒 | chercher les systèmes installés ; monte les partitions — assistant : Chercher les systèmes sans autoriser d’écriture disque | 🟡 jaune | assistant graphique, terminal | [fiche](fiches/os-prober.md) |
| **rescue-boot-repair** 🔒 | diagnostic du démarrage en lecture seule ; sauvegarde du MBR et de la table ; GRUB réinstallé en BIOS, après sauvegarde et nom retapé — assistant : Diagnostiquer et réparer le démarrage avec Rescue | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/rescue-boot-repair.md) |
| **rescue-chroot** 🔒 | entrer dans un Linux installé pour le réparer : disque ouvert par rescue-rw, racine, /boot et EFI montés en écriture, chroot ; tout est démonté en sortant | 🔴 rouge | terminal |  |
| **rescue-install** 🔒 | installe Saint-Bernard sur un disque interne vide, avec RESCUE-DATA ; --mise-a-jour remplace le système et garde RESCUE-DATA | 🔴 rouge | terminal | [fiche](fiches/rescue-install.md) |

## Effacement

| Outil | Ce qu'il fait | Risque | S'ouvre | Fiche pratique |
|---|---|---|---|---|
| **blkdiscard** 🔒 | TRIM de tout un SSD — assistant : Envoyer TRIM au disque choisi | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/blkdiscard.md) |
| **fstrim** 🔒 | TRIM de l'espace libre d'un SSD monté, rend les fichiers effacés irrécupérables ; -n pour simuler — assistant : Simuler ou lancer TRIM sur un volume choisi | 🔴 rouge | assistant graphique, terminal |  |
| **hdparm --security-erase** 🔒 | effacement ATA | 🔴 rouge | terminal | [fiche](fiches/hdparm.md) |
| **nvme format** 🔒 | effacement NVMe | 🔴 rouge | terminal | [fiche](fiches/nvme.md) |
| **nwipe** 🔒 | effacement sécurisé de disques entiers ; ne brancher que le disque à effacer ; le rapport PDF va dans le dossier courant, en mémoire : le copier ensuite — assistant : Effacer uniquement le disque choisi avec Nwipe | 🔴 rouge | assistant graphique, terminal plein écran | [fiche](fiches/nwipe.md) |
| **openSeaChest_Erase** 🔒 | effacement matériel sécurisé, sanitize, DÉTRUIT les données — assistant : Consulter ou lancer un effacement matériel | 🔴 rouge | assistant graphique, terminal |  |
| **rescue-wipe** 🔒 | efface un disque entier : une passe de zéros puis relecture complète, trois confirmations, rapport d'effacement HTML — assistant : Effacer et vérifier un disque avec Rescue | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/rescue-wipe.md) |
| **shred** 🔒 | écraser un fichier ou un disque — assistant : Écraser intégralement un disque identifié | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/shred.md) |
| **wipefs** 🔒 | effacer les signatures de systèmes de fichiers — assistant : Lire ou effacer les signatures d’un disque | 🔴 rouge | assistant graphique, terminal | [fiche](fiches/wipefs.md) |

## Antivirus

| Outil | Ce qu'il fait | Risque | S'ouvre | Fiche pratique |
|---|---|---|---|---|
| **clamscan** | analyser des fichiers ; lit chaque fichier en entier : sur une copie ou un disque sain | 🟡 jaune | assistant graphique, terminal | [fiche](fiches/clamscan.md) |
| **freshclam** 🔒 | mettre à jour les signatures ; réseau | ⚪ aucun | assistant graphique, terminal | [fiche](fiches/freshclam.md) |

## Réseau

| Outil | Ce qu'il fait | Risque | S'ouvre | Fiche pratique |
|---|---|---|---|---|
| **Configurer le réseau** 🔒 | nmtui | ⚪ aucun | assistant graphique, terminal plein écran |  |
| **Connexions réseau** | icône près de l'horloge : choisir et configurer une connexion filaire ou Wi-Fi | ⚪ aucun | fenêtre |  |
| **curl, wget** | télécharger | 🟠 orange | assistant graphique, terminal |  |
| **ethtool** 🔒 | carte réseau : lien, vitesse | ⚪ aucun | assistant graphique, terminal |  |
| **Grsync** | rsync en interface graphique : copier ou synchroniser des dossiers ; « Supprimer à la destination » efface des fichiers, simulation conseillée | 🟠 orange | fenêtre |  |
| **ip** | adresses et routes | ⚪ aucun | assistant graphique, terminal | [fiche](fiches/ip.md) |
| **iperf3** | débit réseau | ⚪ aucun | assistant graphique, terminal |  |
| **mtr** | route et pertes vers une adresse, en continu | ⚪ aucun | assistant graphique, terminal |  |
| **Navigateur web** |  | ⚪ aucun | fenêtre |  |
| **nbd-client** 🔒 | attacher en /dev/nbdX un disque ou une image exporté par un serveur NBD, par exemple comme destination d'image ; -d pour détacher | 🟠 orange | assistant graphique, terminal |  |
| **Partage réseau Samba** | rend un dossier visible depuis Windows, macOS et Linux ; lecture seule par défaut, mot de passe obligatoire ; désactivé au démarrage | 🟠 orange | fenêtre |  |
| **Partages : mount.cifs** 🔒 | SMB), mount.nfs (NFS | 🟠 orange | assistant graphique, terminal | [fiche](fiches/mount.cifs.md) |
| **ping** | tester une réponse ICMP bornée | ⚪ aucun | assistant graphique, terminal | [fiche](fiches/ping.md) |
| **Rclone Browser** | rclone en interface graphique : stockages en ligne et distants ; configurer d'abord un « remote » | 🟠 orange | fenêtre |  |
| **rescue-net** 🔒 | état du réseau ; connexion Wi-Fi ; destination de sauvegarde montée en écriture par Samba, NFS ou sshfs | 🟠 orange | assistant graphique, terminal | [fiche](fiches/rescue-net.md) |
| **rescue-pxe** | servir Saint-Bernard aux autres PC par le réseau, démarrage PXE BIOS et UEFI ; arrêté au démarrage, off coupe tout | 🟠 orange | terminal | [fiche](fiches/rescue-pxe.md) |
| **rescue-ssh** | accès à distance par SSH : éteint au démarrage ; on fait choisir un mot de passe, off coupe tout ; aussi dans les Réglages | 🟠 orange | assistant graphique, terminal | [fiche](fiches/rescue-ssh.md) |
| **rsync** | copier vers une autre machine | 🟠 orange | assistant graphique, terminal | [fiche](fiches/rsync.md) |
| **smbclient** | copier vers ou depuis un partage Windows sans le monter | 🟠 orange | assistant graphique, terminal | [fiche](fiches/smbclient.md) |
| **ssh, scp, sshfs** | accès distant | 🟠 orange | assistant graphique, terminal | [fiche](fiches/ssh.md) |
| **traceroute** | route vers une adresse | ⚪ aucun | assistant graphique, terminal |  |

## Bureau

| Outil | Ce qu'il fait | Risque | S'ouvre | Fiche pratique |
|---|---|---|---|---|
| **Afficher ou masquer le suivi** | Conky | ⚪ aucun | fenêtre |  |
| **Fichiers** |  | ⚪ aucun | fenêtre |  |
| **Menu de secours en mode texte** | rescue-menu : disques, SMART, montage, clonage, récupération, effacement | 🟢 vert | assistant graphique, terminal plein écran | [fiche](fiches/rescue-menu.md) |
| **Midnight Commander** | fichiers, en console | ⚪ aucun | assistant graphique, terminal plein écran | [fiche](fiches/mc.md) |
| **Procédure type de récupération** | rescue-help : ne rien écrire, SMART, cloner, travailler sur l'image, rapport | 🟢 vert | assistant graphique, terminal plein écran | [fiche](fiches/rescue-help.md) |
| **Réglages** | aide à l'ouverture des outils, suivi Conky, clavier, date et heure, fuseau, écran, réseau | ⚪ aucun | fenêtre |  |
| **Terminal** |  | ⚪ aucun | fenêtre |  |
| **tmux** | plusieurs consoles dans un terminal | ⚪ aucun | assistant graphique, terminal plein écran | [fiche](fiches/tmux.md) |
| **Éditeur de texte** |  | ⚪ aucun | fenêtre |  |

---

[Retour à la présentation](README.md)
