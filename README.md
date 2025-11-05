# ansible_lab1
Lab 7 : Automatización de Infraestructura con Ansible

Este laboratorio utiliza **Ansible** para configurar automáticamente un entorno con dos contenedores Docker:
- `web01`: servidor **Nginx**
- `db01`: servidor **MariaDB**

> *Nota:* El cambio de `MySQL` por `MariaDB` se debe a que intenté instalarlo pero debido a la cantidad de probamas derivador de l que no inicia con systemd los cotnendores decidí cambiarlo

## Configuración SSH

Para permitir que Ansible se conecte automáticamente a los contenedores sin confirmar las claves SSH (necesario porque los contenedores se regeneran y cambian su huella), se debe editar el archivo `~/.ssh/config` y añadir:

```bash
Host 172.18.*
    StrictHostKeyChecking no
    UserKnownHostsFile=/dev/null
```

Esto evita errores del tipo:
```
WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!
```

> *Nota:* Esta configuración desactiva la verificación de seguridad SSH para las direcciones `172.18.*`, por lo que solo debe usarse en entornos de laboratorio o desarrollo.

##  Pasos para ejecutar el laboratorio

1. Levantar los contenedores:
   ```bash
   docker compose up -d
   ```

2. Ejecutar el playbook:
   ```bash
   ansible-playbook -i inventory.ini site.yml
   ```

3. Comprobar que Nginx está accesible desde el host:
   - Navegador: [http://localhost:8080](http://localhost:8080)
   - O con `curl`:
     ```bash
     curl http://localhost:8080
     ```
