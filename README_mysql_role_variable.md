# 🐬 Ansible Role: MySQL

## 📋 Descripción
Este rol instala y configura **MySQL Server** automáticamente en sistemas Linux (Debian/Ubuntu o RHEL/CentOS).  
Evita prompts interactivos durante la instalación y asegura que el servicio quede activo con una contraseña de root definida.

---

## 📁 Estructura del rol
```
roles/
└── mysql/
    ├── tasks/main.yml        # Tareas principales
    └── defaults/main.yml     # Variables por defecto (sobrescribibles)
```

---

## ⚙️ Funcionalidad

1. Instala dep```encias necesarias (`python3-pymysql`, `debconf-utils`).
2. Preconfigura la contraseña de root para evitar prompts.
3. Instala MySQL Server con `apt` (Debian/Ubuntu) o `yum` (RHEL/CentOS).
4. Inicia y habilita el servicio MySQL.
5. Configura la contraseña de `root` de forma idempotente.

✅ **Resultado:**  
MySQL instalado, corri```o y con una contraseña conocida, sin intervención manual.

---

## 🔐 Variables

### `mysql_root_password`
- Definida en `defaults/main.yml`
- Valor por defecto:
```
mysql_root_password: "StrongPassword123"
```
- Puede sobrescribirse desde fuera del rol (inventario, playbook o CLI).

### 📘 ¿Por qué está en `defaults`?
Porque las variables en `defaults` **pueden sobrescribirse**, mientras que las de `vars` **no**.  
Esto permite adaptar la contraseña según el entorno (dev, test, prod).

---

## 🧩 Formas de sobrescribir la variable

### 1️⃣ En el playbook
```
roles:
  - role: mysql
    vars:
      mysql_root_password: "MyCustomPass"
```

### 2️⃣ En el inventario
```
[db_servers]
db01 mysql_root_password=Root123
```

### 3️⃣ En `group_vars/` o `host_vars/`
```
mysql_root_password: "GroupPassword"
```

### 4️⃣ Desde la línea de comandos
```
ansible-playbook playbook.yml -e "mysql_root_password=Test123"
```

---

## 🧠 Prioridad de variables

| Ubicación | Prioridad | Sobrescribible |
|------------|------------|----------------|
| `defaults/main.yml` | 🔽 Baja | ✅ Sí |
| `vars/main.yml` | 🔼 Alta | ❌ No |
| Inventario / group_vars / playbook / `-e` | 🔝 Muy alta | ✅ Sí |

---

## 🚀 Uso

Ejemplo de ejecución:
```
ansible-playbook -i inventory playbook.yml
```

MySQL quedará instalado, configurado y listo para usarse.
