# Standard Operating Procedure (SOP)
## Trabajo en Rama de Desarrollo (`develop`) — Protección de `main`

> Propósito: Estandarizar el flujo de trabajo en la rama `develop` del repositorio `mdasuaje.github.io`, garantizando que `main` permanezca intacta como muestra profesional del portafolio público y que todos los cambios se integren mediante commits atómicos sincronizados con el remoto.

---

## 1. POLÍTICA DE RAMAS

| Rama | Propósito | Estado |
|------|-----------|--------|
| `main` | Rama de producción y portafolio público. **Sin cambios directos.** | Protegida |
| `develop` | Rama de desarrollo e integración de cambios. | Activa |
| `feature/*` | Ramas temporales para funcionalidades específicas (opcional). | Temporal |

**Regla de oro:** Nunca commitear directamente sobre `main`. Todo cambio pasa por `develop` primero.

---

## 2. FLUJO ESTÁNDAR DE TRABAJO

### Paso 1 — Sincronizar antes de iniciar
```bash
git checkout develop
git pull origin develop
```

### Paso 2 — Crear rama de feature (opcional, para cambios mayores)
```bash
git checkout -b feature/<nombre> develop
```

### Paso 3 — Verificar estado antes del primer write
```bash
git status --short
git log --oneline -3
git rev-parse develop
git rev-parse origin/develop
```

### Paso 4 — Implementar cambios (task by task)
- Modificar solo los archivos necesarios.
- Mantener cada cambio enfocado en una sola responsabilidad.
- No incluir archivos de sesión, runtime o artifacts privados (ver `.gitignore`).

### Paso 5 — Commit atómico
```bash
git add <archivos_modificados>
git commit -m "<tipo>(<scope>): <descripción>

- Detalle del cambio 1
- Detalle del cambio 2
- Mantener Honestidad Radical: sin títulos no poseídos, sin 'Senior'/'Architect' sin evidencia"
```

**Convención de commits (Conventional Commits):**
- `feat:` nueva funcionalidad
- `fix:` corrección de error
- `docs:` documentación solamente
- `refactor:` reestructuración sin cambio de comportamiento
- `style:` formato, sin cambio de lógica
- `test:` pruebas
- `chore:` mantenimiento, dependencias, build

### Paso 6 — Push a remoto
```bash
git push origin develop
```

### Paso 7 — Verificar sincronización
```bash
git rev-parse develop
git rev-parse origin/develop
# Ambas SHA deben coincidir
```

---

## 3. PROTECCIÓN DE `main`

- `main` se sincroniza con `origin/main` y nunca recibe commits directos.
- Para promover cambios de `develop` a `main`, el humano debe abrir un Pull Request desde GitHub y revisar los cambios antes del merge.
- El agente no ejecuta `git push origin main` ni merge directo a `main`.

---

## 4. HONESTIDAD RADICAL EN DOCUMENTACIÓN

- No atribuir títulos universitarios no poseídos.
- No atribuir experiencia comercial no demostrable.
- No declarar ingresos no recibidos.
- No usar "Senior" ni "Architect" sin evidencia.
- Inglés presentado con precisión.

---

## 5. ARCHIVOS RELACIONADOS

- `/home/masua/mdasuaje.github.io/index.html` — Perfil público principal (modificado en rama develop)
- `/home/masua/mdasuaje.github.io/README.md` — Documentación del repositorio
- `/home/masua/mdasuaje.github.io/AGENT.md` — Identidad y directivas del agente
- `/home/masua/mdasuaje.github.io/CONTEXT.md` — Contexto de negocio
- `/home/masua/job-mining-engine/profile/mauro.yaml` — Perfil candidato (source of truth para job-mining-engine)

---

## 6. CÓDIGOS DE SALIDA

| Código | Significado | Acción |
|--------|-------------|--------|
| `0` | Éxito | Continuar con siguiente paso |
| `1` | Error general | Revisar salida de Git, corregir y reintentar |
| `128` | Rama no encontrada | Verificar nombre de rama, hacer `git fetch` |
| `non-zero` en push | Rechazo remoto | Hacer `git pull --rebase origin develop` y resolver conflictos |
