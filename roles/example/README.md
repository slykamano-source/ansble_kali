# Rôle `example`

Rôle de démonstration : déploie un fichier texte généré depuis un template Jinja2,
et illustre la structure standard d'un rôle Ansible (defaults, tasks, templates, handlers).

## Variables (defaults/main.yml)

| Variable          | Défaut                            | Description                          |
|-------------------|------------------------------------|---------------------------------------|
| `example_message` | `"Hello from the example role!"`  | Message écrit dans le fichier de sortie |
| `example_dest`    | `/tmp/example_role_output.txt`    | Chemin du fichier généré              |

## Exemple d'utilisation

```yaml
- hosts: all
  roles:
    - role: example
      vars:
        example_message: "Configuré par Ansible"
```
