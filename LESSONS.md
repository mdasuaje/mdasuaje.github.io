# LESSONS.md: Registro de Mejora Continua (1% Diario)

## Principios de Evolución
Este documento rastrea los aprendizajes, correcciones y decisiones tácticas tomadas durante el desarrollo del ecosistema web. Actúa como nuestra memoria a largo plazo.

## Registro de Lecciones

### 1. Desacoplamiento de Assets Documentales
- **Observación:** Inicialmente, el CV en PDF se trataba como parte del repositorio web.
- **Lección:** El archivo `cv_main.pdf` es una base de datos documental dinámica, mientras que la web es la interfaz estática. Deben mantenerse separados. La web solo debe apuntar a la ruta esperada.

### 2. Estricta Privacidad (Zero-Trust)
- **Observación:** El contenido previo incluía referencias a proyectos específicos (IKU) que no debían exponerse públicamente de forma permanente.
- **Lección:** Implementar validación cruzada antes de hacer commits. La "Erradicación Histórica" es una regla activa.

### 3. Tono de Comunicación (Axial Trade Lab)
- **Observación:** La descripción inicial del laboratorio de trading empleaba términos como "extracción de rentabilidad".
- **Lección:** Adoptar un enfoque estoico y científico. Sustituir jerga financiera por terminología de ingeniería de sistemas y análisis cuantitativo.