# Standard Operating Procedure (SOP)
## Manual de Operador: Despliegue de Identidad Pública

**Propósito:** Publicar la última versión compilada del Resumen Curricular hacia el dominio web `mdasuaje.github.io` sin requerir intervención manual sobre el repositorio público.

### Prerrequisitos
- Haber modificado y guardado los cambios en el código fuente (`.tex`) en `/home/masua/cv-asuaje-0825`.
- Haber ejecutado la compilación de Ingeniería Documental (LaTeX) localmente, asegurando que `cv_main.pdf` esté actualizado.

### Procedimiento Estándar

1.  Abre la terminal CLI (entorno WSL2).
2.  Navega al repositorio maestro de identidad:
    ```bash
    cd /home/masua/cv-asuaje-0825
    ```
3.  Invoca el pipeline de Entrega Continua:
    ```bash
    ./scripts/deploy_to_public.sh
    ```

### Códigos de Salida del Sistema
Durante la ejecución, el monitor de terminal reportará los siguientes estados:
-   `❌ [ERROR]`: Fallo crítico. Usualmente significa que olvidaste compilar el LaTeX o que la ruta del repositorio cambió.
-   `⚡ [SKIP]`: Flujo exitoso pero redundante. Significa que el PDF recién compilado es idénticamente igual al que ya está en línea. No se gastaron recursos.
-   `🎉 [SUCCESS]`: Despliegue exitoso. Tu perfil en línea ha sido actualizado con los nuevos datos.