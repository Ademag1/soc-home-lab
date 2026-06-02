Documentation du Projet – Home Lab SOC / Cybersécurité

Objectif du laboratoire

L’objectif de ce laboratoire est de construire un environnement cybersécurité segmenté permettant :

- de simuler des attaques depuis une machine Kali Linux ;
- de détecter les activités malveillantes avec Suricata IDS/IPS sur OPNsense ;
- de centraliser et corréler les logs avec Wazuh et Splunk ;
- de reproduire un environnement réaliste de SOC (Security Operations Center).

---

Problème initial

Au départ, les machines suivantes étaient placées sur le même réseau virtuel :

- Kali Linux
- DVWA
- Wazuh
- Splunk

Problèmes observés

- les alertes IDS n’apparaissaient pas correctement ;
- le trafic d’attaque contournait OPNsense ;
- Suricata ne voyait pas les scans internes ;
- les communications restaient au niveau Layer 2 sans passer par le firewall.

Le trafic ne traversait donc pas le moteur IDS/IPS.

---

Architecture réseau segmentée

Une architecture segmentée a ensuite été mise en place avec VMware et OPNsense.

Réseau interne / supervision

Contient :

- DVWA (serveur vulnérable)
- Wazuh Manager
- Serveur Splunk
- Interface LAN d’OPNsense

Sous-réseau :

- 192.168.xxx.0/24

---

Réseau attaquant

Contient :

- Kali Linux / Red Team VM
- Interface OPT1 d’OPNsense

Sous-réseau :

- 192.168.xxx.0/24

---

Routage avec OPNsense

OPNsense assure le routage entre :

- le réseau attaquant ;
- le réseau interne.

Cela force tout le trafic d’attaque à traverser :

- le firewall ;
- Suricata IDS/IPS.

Cette architecture améliore :

- la visibilité réseau ;
- l’inspection du trafic ;
- la détection des menaces.

---

Configuration OPNsense

Interfaces configurées

WAN

- accès Internet (DHCP)

LAN

- réseau interne / supervision

OPT1

- réseau attaquant / Red Team

---

Configuration Firewall

Une règle firewall a été créée sur l’interface OPT1 :

- Action : Pass
- Source : réseau attaquant
- Destination : any

Cette configuration a permis :

- la connectivité de Kali Linux ;
- le routage inter-réseaux ;
- l’accès Internet via OPNsense.

---

Configuration Kali Linux

Configuration IP statique :

- IP : masquée
- Gateway : interface OPT1 d’OPNsense

Tests validés :

- ping vers OPNsense ;
- accès Internet ;
- communication inter-réseaux.

---

Configuration DVWA

Configuration réseau manuelle :

- IP statique ;
- gateway via interface LAN d’OPNsense ;
- DNS configuré.

DVWA communique correctement avec :

- OPNsense ;
- Wazuh ;
- Splunk.

---

Intégration Wazuh

Wazuh Manager

Le serveur Wazuh a été configuré pour recevoir les événements des systèmes du laboratoire.

Agent Wazuh

L’agent Wazuh installé sur DVWA a été configuré et connecté avec succès.

Statut confirmé :

- active (running)
- connexion établie

Les événements remontent correctement dans le dashboard Wazuh.

---

Intégration Splunk

Splunk a été intégré afin de centraliser :

- les logs firewall ;
- les logs IDS/IPS ;
- les événements de sécurité.

Transmission des logs réalisée via syslog distant depuis OPNsense.

Connectivité validée avec succès.

---

Configuration Suricata IDS/IPS

Suricata a été activé sur OPNsense.

Fonctionnalités activées

- mode IDS ;
- alertes syslog ;
- logs EVE JSON ;
- règles ET Open.

Fichier de logs

/var/log/suricata/eve.json

---

Catégories de règles activées

- emerging-scan.rules
- emerging-exploit.rules
- emerging-malware.rules

---

Validation IDS

Tests réalisés avec succès :

- génération d’alertes Suricata ;
- événements écrits dans eve.json ;
- alertes visibles dans OPNsense.

Exemples d’événements détectés :

- GPL ATTACK_RESPONSE ;
- événements SSH ;
- activités réseau suspectes.

---

Découverte importante

Une problématique réseau majeure a été identifiée :

Lorsque Kali Linux et DVWA étaient sur le même sous-réseau :

- le trafic ne traversait pas OPNsense ;
- Suricata ne pouvait pas inspecter les scans internes.

Solution appliquée

- séparation du réseau attaquant et du réseau victime ;
- routage obligatoire via OPNsense.

Cette étape a permis de mieux comprendre :

- la segmentation réseau ;
- le routage ;
- les communications Layer 2 ;
- la visibilité IDS/IPS.

---

État actuel du laboratoire

Fonctionnalités opérationnelles

- segmentation réseau ;
- routage OPNsense ;
- réseau attaquant Kali ;
- communication DVWA ;
- agent Wazuh connecté ;
- intégration Splunk ;
- génération d’alertes Suricata ;
- logs EVE JSON ;
- syslog distant.

---

Travaux restants

Validation IDS finale

Objectifs :

- générer des alertes Nmap ;
- visualiser les alertes dans Suricata ;
- intégrer les alertes dans Wazuh ;
- corréler les événements dans Splunk.

---

Évolutions prévues

Simulations d’attaque

- Nmap
- Nikto
- SQLMap
- Hydra

Développements futurs

- intégration complète Suricata → Wazuh ;
- dashboards Splunk ;
- exercices SOC / Blue Team ;
- détection et investigation d’incidents ;
- scénarios Red Team / Blue Team.

---

Compétences travaillées

Ce laboratoire a permis de pratiquer :

- VMware Networking ;
- segmentation réseau ;
- configuration firewall ;
- administration OPNsense ;
- déploiement IDS/IPS ;
- configuration Suricata ;
- réseau Linux ;
- configuration IP statique ;
- intégration Wazuh ;
- forwarding Splunk ;
- architecture SOC ;
- inspection du trafic ;
- troubleshooting réseau et firewall.

---

Conclusion

Un environnement cybersécurité segmenté réaliste a été conçu et partiellement opérationnel.

Le laboratoire permet désormais :

- la simulation d’attaques ;
- l’inspection du trafic réseau ;
- la centralisation des logs ;
- l’intégration SIEM ;
- la génération d’événements IDS/IPS.

Ce projet constitue une excellente base pour :

- la préparation CompTIA Security+ ;
- les postes SOC Analyst ;
- le Blue Teaming ;
- le Detection Engineering ;
- la constitution d’un portfolio cybersécurité professionnel.
