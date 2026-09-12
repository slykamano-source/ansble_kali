# Rôle `webserver`

Installe et configure un serveur web **Nginx** sur des hôtes Debian/Ubuntu :
installation du paquet, configuration d'un site virtuel, page d'accueil de test,
ouverture du port dans UFW (si présent), démarrage et activation du service.

## Variables (defaults/main.yml)

| Variable                    | Défaut                              | Description                                  |
|------------------------------|--------------------------------------|-----------------------------------------------|
| `webserver_package`         | `nginx`                             | Paquet à installer                            |
| `webserver_service`         | `nginx`                             | Nom du service systemd                        |
| `webserver_port`            | `80`                                 | Port d'écoute HTTP                            |
| `webserver_server_name`     | `_`                                  | `server_name` nginx (nom de domaine ou `_`)   |
| `webserver_document_root`   | `/var/www/html`                     | Racine des fichiers servis                    |
| `webserver_index_message`   | `Bienvenue - déployé par Ansible`   | Message affiché sur la page d'accueil de test |
| `webserver_manage_firewall` | `true`                               | Ouvre le port dans UFW si UFW est installé    |

## Utilisation

```yaml
- hosts: webservers
  become: true
  roles:
    - role: webserver
      vars:
        webserver_server_name: mon-site.example.com
        webserver_index_message: "Bienvenue sur mon-site.example.com"
```

## Prérequis

- Hôtes Debian/Ubuntu avec `apt`
- Privilèges root (via `become: true`)
