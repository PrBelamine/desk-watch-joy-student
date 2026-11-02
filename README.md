# Desk Watch JOY STUDENT

**Français** | [English](README_EN.md)

Une console de bureau pour les élèves, basée sur un **Arduino UNO R3 et des modules Grove**, pilotée avec un joystick : température et humidité, minuteur Pomodoro, compteur, chronomètre, réveil, dé, pendule d'échecs et mélodies. Les modules se branchent avec des câbles Grove, sans soudure.

**[MiniTech Club : présentation, montage, guides et installation USB](https://minitech.club/desk-watch-joy-student/)**

## Installer depuis MiniTech Club

Ouvre la [section « Installer et tester »](https://minitech.club/desk-watch-joy-student/#programme) dans **Chrome ou Edge sur ordinateur**.

1. Choisis **Français** ou **English** en haut de la page : ce choix détermine aussi la langue du programme installé.
2. Branche ton **Arduino UNO R3 (ATmega328P)** avec un câble USB qui transmet les données. Ferme l'IDE Arduino et son moniteur série.
3. Clique sur **Installer JOY STUDENT**, puis sélectionne le port USB de ta carte.
4. Garde le câble branché jusqu'à la fin de l'installation et de la vérification.
5. Au redémarrage, **laisse le joystick au repos** pendant le calibrage de sa position centrale.
6. Teste l'écran, le joystick, les mesures du capteur SHT, l'heure du RTC et le buzzer avant de fermer le boîtier.

Cette méthode ne demande ni IDE Arduino ni installation de bibliothèque. Elle remplace le programme présent sur la carte. L'installateur vise l'**UNO R3**, pas l'UNO R4. Firefox, Safari et les navigateurs sur téléphone ne sont pas pris en charge par cette page.

## Modifier le programme avec l'IDE Arduino

Pour lire ou modifier le code, utilise l'un des deux croquis de ce dépôt :

- [Programme français](Desk_Watch_JOY_STUDENT_Edition_FR/Desk_Watch_JOY_STUDENT_Edition_FR.ino)
- [Programme anglais](Desk_Watch_JOY_STUDENT_Edition_EN/Desk_Watch_JOY_STUDENT_Edition_EN.ino)

Installe la bibliothèque **Grove - LCD RGB Backlight**, ouvre le croquis dans son dossier du même nom, sélectionne **Arduino Uno** et le bon port, puis téléverse. Aucune autre bibliothèque externe n'est nécessaire. Ne touche pas le joystick au démarrage.

## Guides et liens du projet

| Ressource | Français | English |
|---|---|---|
| Guide de montage | [PDF](docs/FR_Desk_Watch_JOY_STUDENT_Guide_de_montage.pdf) | [PDF](docs/EN_Desk_Watch_JOY_STUDENT_Assembly_Guide.pdf) |
| Mode d'emploi | [PDF](docs/FR_Desk_Watch_JOY_STUDENT_Mode_d_emploi.pdf) | [PDF](docs/EN_Desk_Watch_JOY_STUDENT_User_Guide.pdf) |
| Schéma de câblage | [Image](docs/wiring_FR.png) | [Image](docs/wiring_EN.png) |

- [MiniTech Club : tutoriel et installateur USB](https://minitech.club/desk-watch-joy-student/)
- [Support : formulaire en bas de la page du projet](https://minitech.club/desk-watch-joy-student/#support)
- [MakerWorld : boîtier à imprimer et profils d'impression](https://makerworld.com/models/3490181)
- [Hackster : présentation du projet](https://www.hackster.io/Pr_Belamine_Makerlab/desk-watch-joy-student-arduino-uno-joystick-console-dcf03f)

## Firmware et notes techniques

Deux sketchs, un par langue : `Desk_Watch_JOY_STUDENT_Edition_FR` et `Desk_Watch_JOY_STUDENT_Edition_EN` (le dossier porte le nom du sketch, comme l'exige l'IDE Arduino).

Dérivé de `TEACHER_BMP280_JOY` (22/10/2026), sans le baromètre et sans le mode examen. Tout le reste est identique : joystick, pages et réglages.

## Matériel
Arduino UNO + Grove Base Shield, écran Grove LCD RGB V4.0, SHT31 ou SHT40 (détection automatique, voir ci-dessous), buzzer D3, Grove Thumb Joystick (X sur A1, Y sur A2), RTC DS1307 ou DS3231 obligatoire (I2C 0x68) : il fournit l'heure, le réveil et le mode nuit automatique. Bibliothèque nécessaire : « Grove - LCD RGB Backlight ». Ne pas toucher le joystick à la mise sous tension (le centre est mesuré à ce moment).

## Pages
Temp et Hum, Minuteur (Pomodoro), Compteur, Chrono, Réveil, Dé, Pendule d'échecs, Mélodie, Paramètres, Mode veille (10 entrées). Le favori n'est pas une entrée du menu : il se choisit dans Paramètres. Écran de démarrage : « JOY STUDENT ».

Temp et Hum (5 pages, haut / bas pour changer, flèches affichées à gauche de l'horloge) : 1 mesures, 2 minimum, 3 maximum, 4 moyenne (sur les 30 dernières mesures), 5 « AUT » qui fait défiler les pages 1 à 4 toutes les 3 s. L'heure occupe les colonnes 4 à 11.

Dé : la ligne 1 rappelle les gestes (↑↓ faces, OK=relance) et la ligne 2 affiche D + faces à gauche, texte ou résultat entre crochets à droite.

Paramètres (8) : luminosité (85 % par défaut), volume (cinq niveaux : Min, Bas, Moyen, Fort, Max ; Moyen par défaut), son de démarrage, veille automatique, mode nuit, régler l'heure, favori, réglage usine. Le son de démarrage est désactivé par défaut (carte neuve ou après un réglage usine ; une carte déjà configurée garde son réglage).

## Gestes (réglage par défaut, logique verticale)
| Geste | Effet |
|---|---|
| Bas / haut | Défiler le menu, changer une valeur (maintenu : répétition, plus rapide après 1,5 s) |
| Droite, ou clic sur la tête | OK |
| Droite (ou clic) deux fois en moins de 0,4 s | Double clic |
| Gauche | Retour (menu, annuler) |
| Gauche maintenu 2,5 s | Veille |
| Pendule d'échecs en cours : n'importe quel mouvement | Changement de joueur ; maintien 1,2 s = pause ; clic = pause |

Réglages au début du bloc joystick : `NAV_VERTICAL`, `INV_DIAL`, `SWAP_XY`, `INV_X`, `INV_Y` (orientation confirmée pour la carte montée dans le plateau JOY, le 22/10).

## Retiré par rapport à TEACHER_BMP280_JOY
- BMP280 : pression, altitude et QNH, tendance sur 3 h (adresses I2C 0x76 / 0x77 plus utilisées ; la zone EEPROM du QNH n'est plus lue).
- Mode examen (entrée de menu, réglage, compte des copies).
- L'entrée de menu « Temp et Hum » reprend son nom d'origine (c'était « Meteo » avec le baromètre).

## Taille (IDE Arduino 2.3.10, Arduino UNO, compilation du 27/10/2026)
FR : 28 266 octets de programme (87 % de 32 256) et 694 octets de RAM globale (33 % de 2 048). EN : 28 180 octets (87 %) et 694 octets de RAM (33 %). Il reste environ 4 000 octets de programme ; les chiffres du 22/10 (25 154 octets) ne sont plus valables.

Après le passage du volume à cinq niveaux (28/10), le programme grossit d'environ 100 octets (estimation avr-gcc : FR 28 420 octets, EN 28 334 octets, soit 87 à 88 %). La valeur exacte est à relever dans l'IDE Arduino.

## Vérifié sur la carte
- 25/10/2026 : une première console a été imprimée, montée et testée sur une vraie carte avec le firmware de l'époque : tout a fonctionné comme prévu.
- 27/10/2026 : la version actuelle (commentaires mis à jour, son de démarrage désactivé par défaut) est compilée et téléversée sur la carte FR. Aucun autre changement de logique n'a été fait ; un essai complet reste à refaire.

## Vérifié sur PC
- Compilation FR et EN.
- Le code ne diffère de TEACHER_BMP280_JOY que par des suppressions (blocs BMP280 et examen), quelques textes (titre, menu, écran de démarrage, commentaires) et la lecture du capteur (SHT31 ou SHT40).
- Détection SHT31 / SHT40 : fonction de lecture extraite et essayée sur PC avec un faux bus I2C : SHT31 (25,0 °C, 50 % lus correctement), SHT40 (idem), capteur absent, capteur débranché puis remplacé par l'autre type, lectures à CRC faux (valeurs conservées deux fois, panne à la troisième), bornes d'humidité 0 et 100 %.

## Non vérifié
- Les tests de logique joystick faits pour TEACHER_BMP280_JOY n'ont pas été rejoués ici.
- Cohérence de la mémoire EEPROM avec une carte qui avait déjà TEACHER_BMP280_JOY : les réglages sont conservés, la zone du QNH est simplement ignorée.
- SHT40 sur la carte : non essayé. Les commandes et formules viennent de la fiche Sensirion SHT4x (V7.3) : adresse 0x44 pour le SHT40-AD1B (le Grove SHT40 est supposé de cette variante, non vérifié ; les variantes BD1B et CD1B répondent à 0x45 et 0x46 et ne seraient pas détectées), commande 0xFD, T = -45 + 175 x S / 65535, HR = -6 + 125 x S / 65535, même CRC que le SHT31. L'hypothèse que le SHT31 refuse la commande 0xFD et que le SHT40 refuse 0x2400 (base de la détection) n'est pas vérifiée sur le matériel ; en cas d'échec, la lecture retombe sur « Capteur absent ».
