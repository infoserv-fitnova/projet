# Projet Fitnova - Infrastructure virtualisée

## Vue d'ensemble

Ce projet décrit l’infrastructure virtualisée basée sur **Proxmox VE** pour l’environnement **Fitinova**.  
L’architecture repose sur plusieurs VLANs segmentant les rôles (administration, utilisateurs, services, supervision).

---

## Hyperviseur

- **Solution** : Proxmox VE  
- **Pool** : `fitnova`

---

## Détail des machines virtuelles

### VM Docker
| Propriété | Valeur |
|-----------|--------|
| Rôle      | Conteneurisation & supervision |
| IP        | `10.100.151.1/24` |
| VLAN      | `151` |
| Services  | - Portainer <br> - Booked Scheduler <br> - MariaDB <br> - Zabbix |

### VM Active Directory
| Propriété | Valeur |
|-----------|--------|
| Rôle      | Annuaire et authentification |
| IP        | `10.100.151.2/24` |
| VLAN      | `151` |

### VM Salarié
| Propriété | Valeur |
|-----------|--------|
| Rôle      | Poste utilisateur standard |
| IP        | `10.100.153.1/24` |
| VLAN      | `153` |

### VM Admin
| Propriété | Valeur |
|-----------|--------|
| Rôle      | Administration |
| IP        | `10.100.152.1/24` |
| VLAN      | `152` |

### VM WireGuard
| Propriété | Valeur |
|-----------|--------|
| Rôle      | VPN sécurisé |
| IP        | À définir |

### VM pfSense
| Propriété | Valeur |
|-----------|--------|
| Rôle      | Pare-feu / routeur |
| IP        | `10.3.0.198` |

---

## Schéma réseau simplifié

```text
Proxmox VE (fitnova)
├── VLAN 151 (10.100.151.0/24)
│   ├── 10.100.151.1  → VM Docker (Portainer, Booked, MariaDB, Zabbix)
│   └── 10.100.151.2  → VM Active Directory
├── VLAN 153 (10.100.153.0/24)
│   └── 10.100.153.1  → VM Salarié
└── Réseau dédié
    └── 10.3.0.198    → VM pfSense (pare-feu)
