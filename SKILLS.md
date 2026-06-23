# SKILLS.md: Ecosistema Tecnológico y Restricciones

## Stack Principal
- **HTML5:** Semántico y estructurado.
- **CSS3 (Vanilla):** Sin frameworks externos (No Tailwind, No Bootstrap) a menos que se justifique arquitectónicamente. Uso de variables CSS (`:root`) para consistencia de diseño.
- **JavaScript (Vanilla):** Solo si es estrictamente necesario para interactividad que CSS no pueda resolver.

## Tipografía y Diseño
- **Estilo Visual:** Dark Mode Minimalista (Fondo: `#050505` a `#121212`).
- **Fuentes:** 
  - Primaria/Código: `JetBrains Mono` o similar (Courier Prime).
  - Secundaria/Lectura: Sans-Serif limpia (Inter, Geist, o fuentes del sistema).
- **Acentos Visuales:** Sutiles, orientados a evocar un entorno de ingeniería técnica.

## Infraestructura y Despliegue
- **Control de Versiones:** Git. Estricta separación de ramas (`main` para producción, `experimental/*` o `feature/*` para desarrollo).
- **Hosting:** GitHub Pages.
- **Archivos Externos:** El CV descargable reside fuera del control de este repositorio durante el desarrollo local (`/home/masua/cv-asuaje-0825/cv_main.pdf`), asegurando que la interfaz esté desacoplada de la base de datos documental.