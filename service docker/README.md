# Fitnova - Services Docker

## Vue d'ensemble

Ce document décrit l'ensemble des services Docker déployés sur la VM Docker (`10.100.151.1`).  
Ces services assurent la gestion des conteneurs, la planification, la base de données, la supervision et le reverse proxy.

---

## Architecture des services

```text
VM Docker (10.100.151.1)
│
├── Portainer          → Gestion centralisée des conteneurs
├── Booked Scheduler   → Planification de ressources
├── MariaDB            → Base de données relationnelle
├── Zabbix             → Supervision complète
└── Nginx              → Reverse proxy & serveur web
