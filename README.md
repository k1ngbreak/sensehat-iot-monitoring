# Monitoring IoT environnemental — LoRaWAN, MQTT & Node-RED

Projet réalisé en équipe dans le cadre du M2 SECIL (Univ. Paul Sabatier, 2024) :
chaîne IoT complète, de l'acquisition des mesures jusqu'à leur visualisation,
avec une étude de l'impact du Spreading Factor LoRaWAN sur les performances.

## Architecture

Sense HAT → Raspberry Pi (Python) → encodage CayenneLPP → LoRaWAN (module RN2483)
→ réseau neOCampus → LNS → MQTT (Mosquitto) → Node-RED (dashboard)

## Étapes du projet

1. **Acquisition** : température, humidité, pression via le Sense HAT ;
   affichage sur la matrice LED et dans le terminal.
2. **Encodage CayenneLPP** : payload binaire compact, adapté aux contraintes
   LoRaWAN (vs JSON).
3. **Transmission LoRaWAN** : module Microchip RN2483 piloté en UART,
   activation OTAA, envois confirmés toutes les 5 minutes.
4. **Visualisation Node-RED** : décodage des trames et dashboard temps réel.
5. **Analyse de performance** : 30 trames capturées par Spreading Factor
   (SF7 à SF12) ; influence du SF sur le RSSI, le SNR et le taux de réception
   par gateway.

## Technos

- Raspberry Pi + Sense HAT, Python
- LoRaWAN (RN2483), CayenneLPP
- MQTT (Mosquitto), Node-RED
- Jupyter Notebook (analyse des trames)

## Contenu du dépôt

- [`TP_SenseHat.ipynb`](./TP_SenseHat.ipynb) : récupération des mesures
  (température, humidité, pression) depuis le Sense HAT, affichage sur la
  matrice LED et encodage des données au format CayenneLPP.
- [`TP_LoRaWAN.ipynb`](./TP_LoRaWAN.ipynb) : configuration du module
  LoRa RN2483 (OTAA, UART), fonction d'envoi des trames et vérification de
  la réception sur le broker MQTT.
- [`TP_Performances_LoRaWAN.ipynb`](./TP_Performances_LoRaWAN.ipynb) : analyse des trames capturées
  (30 par Spreading Factor, SF7 à SF12) — graphiques RSSI, SNR et taux de
  réception par gateway.
- [`Rapport.pdf`](./Rapport.pdf) : rapport complet
  du projet (M2 SECIL).


## Résultats

- Données reçues et affichées correctement sur le dashboard Node-RED.
- L'analyse montre qu'un SF élevé élargit la portée (les gateways distantes
  captent davantage) au prix d'un débit réduit — conforme à la théorie LoRaWAN.

