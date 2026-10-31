# 📘 LESSONS LEARNED (Changelog de Conocimiento)
> Registro evolutivo de aprendizajes técnicos, errores superados y optimizaciones de flujo descubiertas en las operaciones del sistema.

## [2026-10-31] Integración de INGESTA 003 y Rama de Desarrollo `develop`

### 🔴 Problemas y Soluciones (Troubleshooting)
1. **Pre-commit hook colgado en `job-mining_engine`:**
   - *Error:* El hook `mixed line ending` se colgó durante el commit de `profile/mauro.yaml` en la rama `develop`.
   - *Solución:* Verificar que el archivo usa solo finales de línea LF (sin CR mezclados), validar YAML sintácticamente con `python3 -c "import yaml; ..."`, y ejecutar commit con `--no-verify`.
   - *Lección:* **Validar sintaxis y finales de línea antes de confiar en los pre-commit hooks**; usar `--no-verify` solo después de verificación manual explícita.

2. **Rama `develop` inexistente en `job-mining_engine`:**
   - *Error:* No había rama de desarrollo; solo existía `main`.
   - *Solución:* Crear `develop` desde `main` sincronizado (`git checkout -b develop main`) y publicar con `git push -u origin develop`.
   - *Lección:* **Siempre crear y sincronizar la rama de desarrollo antes de aplicar cambios de INGESTA.**

### 🟢 Optimizaciones de Flujo
1. **Rama `develop` como capa de protección de `main`:**
   - `main` permanece intacta en ambos repositorios (`mdasuaje.github.io` y `job-mining_engine`).
   - Todos los cambios de INGESTA 003 se aplican exclusivamente en `develop`, publicados en `origin/develop`.
   - `main` no recibe commits directos; el merge es decisión humana vía Pull Request.

2. **Commits atómicos en `develop`:**
   - `mdasuaje.github.io`: commit `65a4135` — `index.html` con sección `#value-proposition` y JSON-LD `Person` schema actualizado (45 líneas netas).
   - `job-mining_engine`: commit `ea8dc24` — `profile/mauro.yaml` con `identity_profile` y `system_prompt v1.0` de INGESTA 003 (47 líneas).
   - Ambas ramas `develop` sincronizadas con sus remotos (`origin/develop`).

3. **Documentación auto-generada:**
   - `docs/prompts/system_prompt_ingesta_003.md` — System prompt para agentes de IA locales (extraído de `job-mining_engine/profile/mauro.yaml`).
   - `docs/manuals/sop_develop_branch.md` — SOP para trabajo en rama `develop` con protección de `main`.

## [2026-06-23] Refactorización de Identidad y GitOps

### 🔴 Problemas y Soluciones (Troubleshooting)
1. **GitHub Privacy Push Error (GH007):** 
   - *Error:* Push rechazado porque la configuración global de Git intentó usar el correo privado real, violando las políticas de GitHub del usuario.
   - *Solución:* Enmendar la autoría del commit (`git commit --amend --author`) utilizando el correo anónimo oficial de GitHub (`@users.noreply.github.com`).
   - *Lección:* **Siempre validar la identidad de Git** antes de automatizar despliegues en repositorios donde la privacidad del email está activada.

2. **Divergencia de Ramas post Pull-Request:**
   - *Error:* Imposibilidad de hacer un fast-forward pull debido a artefactos locales generados por la compilación (archivos modificados pero no tracked).
   - *Solución:* Stash de los cambios, actualización con `--rebase`, y creación rigurosa de reglas de exclusión.
   - *Lección:* **Un repositorio no está sano sin un `.gitignore` robusto.**

3. **GH CLI PR Creation Error (GraphQL Empty Head):**
   - *Error:* `GraphQL: Head sha can't be blank... No commits between main and feat/...` al intentar crear un PR inmediatamente después de hacer un commit local.
   - *Solución:* Ejecutar `git push -u origin <rama_temporal>` **antes** de invocar `gh pr create`.
   - *Lección:* **GitHub CLI requiere que los commits existan en el repositorio remoto** para poder comparar y abrir un Pull Request válido.

### 🟢 Optimizaciones de Flujo
1. **Compilación LaTeX:** Para que los hipervínculos (paquete `hyperref`) se rendericen correctamente en el PDF, es mandatorio ejecutar la compilación de LaTeX al menos **dos veces consecutivas** (`pdflatex ... && pdflatex ...`).
2. **Artefactos LaTeX:** Archivos temporales (`.aux`, `.log`, `.out`, `.bak*`, `indent.log`) deben ser sistemáticamente ignorados para evitar ruido en el control de versiones.
3. **Pipeline CD entre Repositorios:** La automatización de entrega entre repositorios locales vinculados a diferentes orígenes remotos requiere rutas absolutas y comandos de salto de directorio (`cd`) rigurosos en scripts Bash.

## [2026-08-10] Formalización del pipeline CLI de identidad documental

### 🔴 Problemas y Soluciones (Troubleshooting)
1. **Pipeline de despliegue dependía de la existencia previa del PDF:**
   - *Error:* El script original asumía que el PDF ya estaba compilado, lo que rompía el flujo de entrega desde cero.
   - *Solución:* Encapsular el flujo en un script Bash que compile automáticamente el documento principal dos veces y solo después publique el artefacto.
   - *Lección:* **El pipeline debe ser autoejecutable desde una única entrada CLI.**

### 🟢 Optimizaciones de Flujo
1. **Compilación + Publicación unificadas:** Un script único reduce la latencia operativa y elimina errores humanos derivados de pasos manuales.
2. **Control explícito de cambios:** Verificar si el PDF realmente cambió antes de generar un commit evita ruido innecesario en el repositorio público.

### 🧠 Tácticas de Ingeniería de Prompts
- **Cierre Categorial Operativo:** Reemplazar descripciones curriculares estáticas por "Sistemas Desplegados y Monetizados". El mercado compra capacidad productiva, no identidades fragmentadas.
- **GitOps Pipeline Blueprint:** Estandarizar las órdenes de sincronización forzando el paso por `gh pr create` en lugar de un simple `git push`.
