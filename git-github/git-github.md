# Guía Completa de Git y GitHub

## 1. Configuración Inicial
```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tuemail@example.com"
git config --global core.editor "code --wait"
```

Ver configuración:
```bash
git config --list
```

---

## 2. Crear Repositorio

### Nuevo repositorio local
```bash
git init
```

### Clonar repositorio remoto
```bash
git clone https://github.com/usuario/repositorio.git
```

---

## 3. Flujo Básico de Trabajo

Ver estado:
```bash
git status
```

Agregar archivos:
```bash
git add archivo.txt
git add .
```

Guardar cambios:
```bash
git commit -m "mensaje del commit"
```

Ver historial:
```bash
git log
git log --oneline
```

---

## 4. Ramas (Branches)

Crear rama:
```bash
git branch nombre-rama
```

Cambiar de rama:
```bash
git checkout nombre-rama
```

Crear y cambiar:
```bash
git checkout -b nombre-rama
```

Ver ramas:
```bash
git branch
```

Eliminar rama:
```bash
git branch -d nombre-rama
```

---

## 5. Trabajo con Ramas

Cambiar entre ramas:
```bash
git checkout main
git checkout develop
```

Fusionar ramas:
```bash
git checkout main
git merge nombre-rama
```

Resolver conflictos:
- Editar archivos
- Luego:
```bash
git add .
git commit -m "conflicto resuelto"
```

---

## 6. Conexión con GitHub

Agregar repositorio remoto:
```bash
git remote add origin https://github.com/usuario/repositorio.git
```

Ver remotos:
```bash
git remote -v
```

---

## 7. Subir Cambios (Push)

Primer push:
```bash
git push -u origin main
```

Siguientes pushes:
```bash
git push
```

Subir rama:
```bash
git push -u origin nombre-rama
```

---

## 8. Obtener Cambios (Pull / Fetch)

Traer cambios y fusionar:
```bash
git pull
```

Solo traer cambios:
```bash
git fetch
```

Actualizar rama específica:
```bash
git pull origin main
```

---

## 9. Sincronizar Ramas

Actualizar rama con main:
```bash
git checkout nombre-rama
git merge main
```

O usando rebase:
```bash
git checkout nombre-rama
git rebase main
```

---

## 10. GitHub Pull Requests

1. Subir rama:
```bash
git push origin nombre-rama
```

2. Crear Pull Request en GitHub
3. Revisar y hacer merge

---

## 11. Deshacer Cambios

Descartar cambios no guardados:
```bash
git checkout -- archivo.txt
```

Eliminar cambios en staging:
```bash
git reset archivo.txt
```

Deshacer último commit (manteniendo cambios):
```bash
git reset --soft HEAD~1
```

Deshacer commit completamente:
```bash
git reset --hard HEAD~1
```

---

## 12. Stash (Guardar cambios temporales)

Guardar cambios:
```bash
git stash
```

Ver stashes:
```bash
git stash list
```

Recuperar cambios:
```bash
git stash apply
```

Eliminar stash:
```bash
git stash drop
```

---

## 13. Buenas Prácticas

- Hacer commits pequeños y claros
- Usar ramas para nuevas funcionalidades
- Actualizar tu rama antes de hacer merge
- Escribir mensajes de commit descriptivos

Ejemplo:
```bash
git commit -m "feat: agregar login de usuarios"
```

---

## 14. Flujo de Trabajo Recomendado

```bash
git checkout -b feature/nueva-funcionalidad
# trabajar
git add .
git commit -m "feat: nueva funcionalidad"
git push origin feature/nueva-funcionalidad
# crear PR en GitHub
```

---

## 15. Comandos Útiles Extra

Ver diferencias:
```bash
git diff
```

Ver quién modificó líneas:
```bash
git blame archivo.txt
```

Renombrar rama:
```bash
git branch -m nuevo-nombre
```

Eliminar rama remota:
```bash
git push origin --delete nombre-rama
```
