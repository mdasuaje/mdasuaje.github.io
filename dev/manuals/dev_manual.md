# Manual de Desarrollo (Dev Manual)

## Arquitectura y Filosofía
Este proyecto no utiliza frameworks complejos (React, Vue, Tailwind) intencionalmente. El objetivo es la máxima velocidad de carga, la simplicidad estructural y la demostración de dominio de los fundamentos web (Vanilla CSS/JS).

## Estructura de Directorios
- `/`: Archivos raíz de configuración e IA (`AGENT.md`, `SKILLS.md`, etc.) y el `index.html` principal.
- `/dev/`: Cerebro y documentación del proyecto.
  - `/dev/sessions/`: (Logs) de sesiones de trabajo importantes.
  - `/dev/adrs/`: Architecture Decision Records.
  - `/dev/manuals/`: Este directorio.

## Flujo de Trabajo (Git Flow)
1. **Nunca** desarrollar directamente en `main`.
2. Crear ramas `experimental/` para pruebas de concepto (como el rediseño minimalista) o `feature/` para implementaciones concretas.
3. El proceso de commit debe ser precedido por un chequeo cruzado de privacidad (Zero-Trust).
4. Al consolidar, se realiza un push manual a `origin/main` (GitHub requiere passphrase SSH).

## Mantenimiento de la Identidad Visual
- Los estilos están embebidos en el `<head>` del `index.html` para reducir requests HTTP.
- Modificar las variables `:root` para ajustar la paleta global.
- Evitar clases redundantes. Mantener el DOM lo más plano posible.