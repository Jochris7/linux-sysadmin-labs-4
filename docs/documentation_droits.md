# Documentation des droits d'accès — Serveur de fichiers

## Arborescence

/srv/entreprise/
├── direction/   → groupe: direction   | permissions: 770
├── rh/          → groupe: rh          | permissions: 770
└── public/      → groupe: root        | permissions: 775

## Groupes et membres

| Groupe    | Membres        |
|-----------|----------------|
| direction | alice, bob     |
| rh        | carol, dave    |
| (aucun)   | stagiaire      |

## Règles d'accès

| Dossier   | direction | rh  | stagiaire     | autres |
|-----------|-----------|-----|---------------|--------|
| direction | ✅ R/W    | ❌  | ❌            | ❌     |
| rh        | ❌        | ✅ R/W | ✅ R seul (ACL) | ❌  |
| public    | ✅ R      | ✅ R | ✅ R          | ✅ R   |

## Commandes utilisées

# Permissions standards
chmod 770 /srv/entreprise/direction
chown root:direction /srv/entreprise/direction

# ACL — accès temporaire lecture seule
setfacl -m u:stagiaire:r-x /srv/entreprise/rh

# Révoquer l'accès
setfacl -x u:stagiaire /srv/entreprise/rh

# Consulter les ACL
getfacl /srv/entreprise/rh
