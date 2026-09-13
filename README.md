# Centro de formación · Proyecto Arthemis

Dos cursos internos en un solo sitio estático. Sin dependencias, sin compilación y sin servidor: son tres archivos HTML.

| Archivo | Qué es |
|---|---|
| `index.html` | Portada con los dos cursos |
| `normativa-salud.html` | Curso 1: normas para ser prestador de servicios de salud en Colombia |
| `procesos-ia.html` | Curso 2: levantamiento y optimización de procesos + fundamentos de IA |
| `.nojekyll` | Evita que GitHub procese el sitio con Jekyll |

---

## Curso 1 · Normas para ser prestador de salud

Escrito en lenguaje sencillo, con letra grande y ajustable desde la propia página. Actualizado a septiembre de 2026.

| # | Módulo |
|---|---|
| 0 | Cómo estudiar con este cuadernillo |
| 1 | El mapa del sistema de salud colombiano |
| 2 | Qué es un prestador y qué debe cumplir |
| 3 | Secretaría de Salud: habilitación paso a paso |
| 4 | Calidad y obligaciones del día a día |
| 5 | EPS: contratos, facturas, glosas y pagos |
| 6 | ARL: riesgos laborales |
| 7 | SOAT: accidentes de tránsito |
| 8 | El rincón del contador |
| 9 | Ruta práctica para arrancar (lista de chequeo) |
| 10 | Seguridad del paciente, CIE-10, CIE-11, CUPS y registros |
| ★ | Examen final de 24 preguntas |

Incluye glosario y normograma con el estado de cada norma.

## Curso 2 · Levantamiento de procesos e IA

| # | Módulo |
|---|---|
| 0 | Cómo usar este curso |
| 1 | Qué es un proceso y cómo se mide |
| 2 | Cómo se levanta un proceso |
| 3 | La entrevista de levantamiento |
| 4 | Documentar y diagramar |
| 5 | Optimizar el proceso |
| 6 | Fundamentos de inteligencia artificial |
| 7 | IA generativa y agentes |
| 8 | IA aplicada al levantamiento y a los procesos |
| 9 | Las herramientas del analista |
| ★ | Examen final de 20 preguntas |

Trae siete herramientas interactivas: calculadora de eficiencia de ciclo, armador de ficha SIPOC, generador de guion de entrevista, detector de cuello de botella, priorizador de oportunidades, constructor de instrucciones para IA y listas de chequeo de campo. Todas exportan texto listo para pegar en la aplicación de levantamiento.

---

## Publicar en GitHub Pages

1. Suba los cuatro archivos a la raíz del repositorio, en la rama `main`.
2. **Settings → Pages**.
3. *Source*: **Deploy from a branch**. Rama `main`, carpeta `/ (root)`. Guarde.
4. En uno o dos minutos queda publicado en `https://USUARIO.github.io/REPOSITORIO/`.

```bash
git add .
git commit -m "Centro de formación: cursos de normativa y de procesos"
git push origin main
```

**Si sale error 404:** revise que `index.html` esté en la raíz (no dentro de una carpeta), que el nombre sea exactamente `index.html`, y mire la pestaña **Actions** para confirmar que el despliegue terminó.

**Si el repositorio es privado:** GitHub Pages en repositorios privados requiere plan de pago. Con plan gratuito el repositorio debe ser público.

---

## Sobre el progreso

Cada curso guarda en el navegador de quien lo estudia:

- El mejor puntaje de cada test.
- Las listas de chequeo marcadas.
- Lo que se escriba en las herramientas.
- La preferencia de tema claro u oscuro.

Se usa `localStorage`, con estas consecuencias:

- Funciona sin cuentas ni servidor.
- **Es por navegador y por dispositivo.** Quien empiece en el computador y siga en el celular, arranca de cero en el celular.
- **No hay panel de seguimiento.** Nadie puede verificar centralmente quién completó el curso.
- Se pierde si la persona borra los datos de navegación o usa modo incógnito.

Si necesita certificar que el equipo hizo el curso, la opción más coherente es servirlo desde la aplicación de levantamiento (Flask + PostgreSQL), que ya tiene usuarios, roles y auditoría: bastaría una tabla de resultados y una vista de seguimiento.

---

## Cómo se mantiene

Cada curso es un archivo autocontenido con esta estructura:

1. `<style>` con las variables de color al inicio (`:root`).
2. Secciones `<section>`, una por módulo.
3. Un `<script>` al final con el objeto que contiene todos los tests.

**Editar un texto:** busque el título del módulo y edite el HTML.

**Agregar una pregunta:** busque `const Q=` (curso 2) o `const QUIZZES=` (curso 1) y agregue un objeto al arreglo del módulo:

```js
{q:"Texto de la pregunta",
 o:["Opción a","Opción b","Opción c","Opción d"],
 a:1,                      // índice de la respuesta correcta, empezando en 0
 e:"Explicación que se muestra al calificar."}
```

Las opciones se barajan con una mezcla fija para que la respuesta correcta no caiga siempre en la misma letra.

**Agregar un módulo:** copie una sección completa, cámbiele el `id`, agregue el enlace en el índice y, si lleva test, una entrada nueva en el objeto de preguntas.

---

## Notas técnicas

- Solo carga tipografías desde Google Fonts; sin internet usa las del sistema.
- Modo claro y oscuro con botón, y respeta la preferencia del sistema.
- Responsive hasta 390 px.
- Imprimible: cada módulo empieza en página nueva y las respuestas salen visibles.
- Accesibilidad: navegación por teclado, foco visible, contraste alto y `prefers-reduced-motion` respetado.

## Advertencias de contenido

- **Normativa:** las normas de salud cambian con frecuencia. Antes de un trámite real confirme la norma vigente en minsalud.gov.co, supersalud.gov.co o con su Secretaría de Salud. Es material de estudio, no asesoría jurídica ni tributaria.
- **Datos sensibles:** los datos de salud son datos sensibles bajo la Ley 1581 de 2012. El curso 2 lo advierte en el módulo 8, pero la política de tratamiento de datos de la institución es la que manda.
