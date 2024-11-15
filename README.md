
# Système Intelligent Contrôlé par le Web

Ce projet met en œuvre un système intelligent contrôlé par le web, permettant de lire les données de capteurs et de contrôler des LEDs à distance. Le système utilise un **STM32F401RE** pour gérer les capteurs et les LEDs, un **ESP32** pour la communication réseau et l'interface de serveur web, et une **interface Qt** pour afficher les données et contrôler les composants depuis un ordinateur.

## Table des matières
- [Aperçu](#aperçu)
- [Architecture du Système](#architecture-du-système)
- [Matériel Requis](#matériel-requis)
- [Prérequis](#prérequis)
- [Installation](#installation)
- [Utilisation](#utilisation)
- [Structure du Code](#structure-du-code)
- [Dépannage](#dépannage)
- [Contributeurs](#contributeurs)
- [Licence](#licence)

## Aperçu
Le système est conçu pour :
- Lire les données de température et d'humidité depuis un capteur **DHT11** connecté au STM32.
- Contrôler des LEDs à distance.
- Afficher les données des capteurs et permettre le contrôle des LEDs via une interface graphique Qt.
- Utiliser l'ESP32 pour transmettre les informations via Wi-Fi et agir comme un serveur web pour accéder aux données et aux commandes de contrôle.

## Architecture du Système

1. **STM32F401RE (Capteurs et LEDs)** :
   - Lit les données du capteur **DHT11**.
   - Contrôle l'état des LEDs.
   - Transmet les données à l'ESP32 via **UART**.

2. **ESP32 (Communication réseau)** :
   - Se connecte au Wi-Fi pour communiquer avec le serveur web.
   - Reçoit les données du STM32 via UART et les envoie au serveur web.
   - Reçoit les commandes de contrôle des LEDs depuis l'interface web et les transmet au STM32.

3. **Interface Qt (Application Desktop)** :
   - Affiche les données de température et d'humidité en temps réel.
   - Permet de contrôler les LEDs via un bouton d'interface.

## Matériel Requis
- [STM32F401RE](https://www.st.com/en/microcontrollers-microprocessors/stm32f401re.html)
- [ESP32](https://www.espressif.com/en/products/socs/esp32)
- Capteur de température et d'humidité **DHT11**
- LEDs (au moins une) et résistances
- Câbles de connexion
- Ordinateur pour exécuter l'interface Qt

## Prérequis

### Logiciels
- **STM32CubeMX** et **STM32CubeIDE** : pour configurer et programmer le STM32.
- **Arduino IDE** ou **PlatformIO** : pour programmer l'ESP32.
- **Qt Creator** : pour créer l'interface graphique Qt.
- **Bibliothèque DHT** : pour lire les données du capteur DHT11 sur le STM32.
- **ESPAsyncWebServer** : pour le serveur web sur ESP32.

## Installation

### Étape 1 : Configuration et Code pour STM32
1. Configurez le projet STM32 dans **STM32CubeMX** en activant **UART** pour la communication et en configurant les GPIO pour le DHT11 et les LEDs.
2. Générez le code, ouvrez-le dans **STM32CubeIDE** et implémentez le code fourni pour lire les données du DHT11 et contrôler les LEDs.
3. Compilez et téléchargez le firmware sur le STM32.

### Étape 2 : Programmation de l'ESP32
1. Ouvrez le code ESP32 dans **Arduino IDE** ou **PlatformIO**.
2. Configurez votre SSID et mot de passe Wi-Fi.
3. Téléchargez le code sur l'ESP32 pour établir la communication UART avec le STM32 et activer le serveur web.

### Étape 3 : Interface Qt
1. Ouvrez le fichier `.qml` dans **Qt Creator**.
2. Compilez et exécutez l'interface Qt pour afficher les données des capteurs et contrôler les LEDs.

## Utilisation
1. **Démarrez le STM32** et assurez-vous qu'il est connecté à l'ESP32 via UART.
2. **Démarrez l'ESP32** et connectez-vous au réseau Wi-Fi.
3. Ouvrez **l'interface Qt** sur votre ordinateur.
4. Utilisez l'interface Qt pour :
   - Lire les données de température et d'humidité.
   - Allumer/éteindre les LEDs.

## Structure du Code

```
📦 Projet_Système_Intelligent
├── 📂 STM32
│   ├── main.c               # Code principal pour STM32
│   ├── stm32f4xx_hal_msp.c  # Fichier de configuration HAL
│   └── ...                  # Autres fichiers générés par STM32CubeMX
├── 📂 ESP32
│   ├── main.ino             # Code principal pour ESP32 (Arduino)
│   └── ...                  # Bibliothèques pour WiFi et serveur web
└── 📂 Qt_Interface
    ├── main.qml             # Interface graphique Qt
    └── main.cpp             # Gestion des requêtes HTTP et de l'interface
```

## Dépannage

- **Problème de connexion Wi-Fi** : Vérifiez le SSID et le mot de passe dans le code ESP32 et assurez-vous que le réseau Wi-Fi est accessible.
- **Pas de données reçues depuis le STM32** : Assurez-vous que les broches UART sont correctement connectées et que les paramètres de baudrate sont identiques entre l'ESP32 et le STM32.
- **LEDs non contrôlables depuis l'interface Qt** : Vérifiez la connectivité réseau entre le Qt et le serveur web de l'ESP32.


## Licence
Ce projet est sous licence MIT. Voir le fichier [LICENSE](LICENSE) pour plus de détails.
