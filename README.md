# ansble_kali

Projet Ansible pour la gestion de configuration d'hôtes locaux et distants.

## Structure

```
.
├── ansible.cfg                    # Configuration Ansible (inventaire, vault, SSH)
├── inventory/
│   ├── hosts.ini                  # Inventaire (groupe [local] + modèle pour hôtes distants)
│   └── group_vars/
│       └── all/
│           ├── vars.yml           # Variables en clair (référence les secrets du vault)
│           └── vault.yml          # Variables sensibles, chiffrées avec ansible-vault
└── playbooks/
    └── ping.yml                   # Playbook de test de connectivité
```

## Prérequis

- Ansible (`ansible-core`)
- Accès SSH aux hôtes distants (clé configurée dans `inventory/hosts.ini` si besoin)
- Le fichier `.vault_pass.txt` à la racine du projet (non versionné, à créer localement)

## Utilisation

Tester la connectivité :

```bash
ansible all -m ping
ansible-playbook playbooks/ping.yml
```

## Gestion des secrets (Ansible Vault)

Les secrets sont stockés chiffrés dans `inventory/group_vars/all/vault.yml` et référencés
depuis `inventory/group_vars/all/vars.yml`.

```bash
ansible-vault edit inventory/group_vars/all/vault.yml    # éditer un secret
ansible-vault view inventory/group_vars/all/vault.yml    # visualiser
ansible-vault rekey inventory/group_vars/all/vault.yml   # changer le mot de passe du vault
```

Le mot de passe du vault est lu depuis `.vault_pass.txt` (chemin défini dans `ansible.cfg`,
fichier ignoré par git). Il doit être recréé/partagé de façon sécurisée sur chaque machine
utilisée pour exécuter les playbooks.

## Ajouter des hôtes distants

Décommenter et adapter le groupe `[webservers]` dans `inventory/hosts.ini`.
