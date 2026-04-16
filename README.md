# 🔒 Serveur de Fichiers Sécurisé — Permissions & ACL

> Simulation d'un environnement d'entreprise avec gestion stricte
> des droits d'accès par groupes Linux et ACL (Access Control Lists).

---

## Description

Ce projet configure une arborescence de fichiers d'entreprise avec
trois niveaux d'accès : Direction, RH et Public. Il met en pratique
la gestion des permissions Linux (chmod/chown) et les ACL pour
simuler un cas réel de contrôle d'accès.

---

## Arborescence
/srv/entreprise/
├── direction/   (accès: groupe direction uniquement)
├── rh/          (accès: groupe rh + stagiaire en lecture)
└── public/      (accès: tout le monde en lecture)


---

## Permissions appliquées

| Dossier   | Propriétaire | Groupe    | chmod | Accès effectif              |
|-----------|-------------|-----------|-------|-----------------------------|
| direction | root        | direction | 770   | direction: R/W — autres: ❌ |
| rh        | root        | rh        | 770   | rh: R/W — autres: ❌        |
| public    | root        | root      | 775   | tous: R — root: R/W         |

---

## ACL — Accès temporaire stagiaire

Accorder un accès lecture seule au stagiaire sur le dossier RH :

```bash
setfacl -m u:stagiaire:r-x /srv/entreprise/rh
```

Révoquer l'accès en fin de mission :

```bash
setfacl -x u:stagiaire /srv/entreprise/rh
```

---

## Captures d'écran

| # | Description |
|---|-------------|
| 01 | Arborescence créée (`ls -la`) |
| 02 | Utilisateurs créés (`/etc/passwd`) |
| 03 | Permissions appliquées |
| 04 | Test de refus d'accès (Permission denied) |
| 05 | ACL configurée (`getfacl`) |
| 06 | Test lecture ok / écriture refusée |
| 07 | Révocation de l'accès stagiaire |

---

## Compétences démontrées

- Gestion des groupes et utilisateurs Linux
- Permissions Unix : chmod, chown
- Access Control Lists : setfacl, getfacl
- Simulation d'un environnement d'entreprise réel
- Sécurité par le principe du moindre privilège
