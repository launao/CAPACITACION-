# Curso: Levantamiento y optimización de procesos + fundamentos de IA

Curso interno para los analistas que levantan procesos en campo. Un solo archivo HTML, sin dependencias, sin compilación y sin servidor.

## Contenido

**Parte I — Procesos**

| # | Módulo | Tema |
|---|--------|------|
| 0 | Cómo usar este curso | Método de estudio y advertencias |
| 1 | Qué es un proceso | SIPOC, niveles, indicadores, ley de Little, los ocho desperdicios |
| 2 | Cómo se levanta | Cinco fases, cinco fuentes, captura en campo, siete errores |
| 3 | La entrevista | Preparación, estructura de la hora, tipos de pregunta, situaciones difíciles |
| 4 | Documentar | Ficha de proceso, diagramas de carriles, símbolos, RACI, validación |
| 5 | Optimizar | Valor agregado, ESCA, cuello de botella, poka-yoke, priorización, PDCA |

**Parte II — Inteligencia artificial**

| # | Módulo | Tema |
|---|--------|------|
| 6 | Fundamentos | IA vs. software tradicional, tipos de aprendizaje, entrenamiento, sobreajuste, sesgo |
| 7 | Generativa y agentes | Modelos de lenguaje, prompts, alucinaciones, RAG, qué es un agente |
| 8 | IA en procesos | Usos reales, minería de procesos, riesgos, datos sensibles, cómo evaluar proveedores |
| 9 | Herramientas | Listas de chequeo de campo |
| ★ | Examen final | 20 preguntas de caso |

## Herramientas interactivas

1. Calculadora de eficiencia de ciclo
2. Armador de ficha SIPOC
3. Generador de guion de entrevista
4. Detector de cuello de botella
5. Priorizador de oportunidades
6. Constructor y evaluador de instrucciones para IA
7. Listas de chequeo de campo

Todas exportan texto listo para pegar en la aplicación de levantamiento.

## Publicar en GitHub Pages

1. Cree un repositorio nuevo (puede ser privado si su plan lo permite).
2. Suba `index.html`, `README.md` y `.nojekyll` a la rama `main`.
3. Vaya a **Settings → Pages**.
4. En *Source* elija **Deploy from a branch**, rama `main`, carpeta `/ (root)`.
5. Guarde. En uno o dos minutos el curso queda en `https://USUARIO.github.io/REPOSITORIO/`.

El archivo `.nojekyll` evita que GitHub procese el sitio con Jekyll. Sin él, todo funciona igual en este caso, pero es buena práctica dejarlo.

### Desde la terminal

```bash
git clone https://github.com/USUARIO/REPOSITORIO.git
cd REPOSITORIO
# copie aquí index.html, README.md y .nojekyll
git add .
git commit -m "Curso de levantamiento de procesos e IA"
git push origin main
```

## Cómo se mantiene

Todo está en `index.html`, en este orden:

1. `<style>` con las variables de color al inicio (`:root`).
2. Secciones `<section class="mod" id="mN">`, una por módulo.
3. Un `<script>` al final con el objeto `Q`, que contiene todos los tests.

**Para editar un texto:** busque el título del módulo y edite el HTML directamente.

**Para agregar una pregunta a un test:** busque `const Q=` y agregue un objeto al arreglo del módulo:

```js
{q:"Texto de la pregunta",
 o:["Opción a","Opción b","Opción c","Opción d"],
 a:1,                       // índice de la respuesta correcta, empezando en 0
 e:"Explicación que se muestra al calificar."}
```

Las opciones se barajan solas con una mezcla fija, para que la respuesta correcta no caiga siempre en la misma letra.

**Para agregar un módulo:** copie una `<section class="mod">` completa, cámbiele el `id`, agregue el enlace en `<nav class="side">` y, si lleva test, una entrada nueva en `Q`.

## Notas técnicas

- Sin dependencias. Solo carga las tipografías Bitter y Public Sans desde Google Fonts; si no hay internet, usa las fuentes del sistema.
- Modo claro y oscuro, con botón para cambiarlo.
- Responsive hasta 390 px de ancho.
- El avance en los tests y en las listas de chequeo se guarda en `localStorage`: es por navegador y por dispositivo, no se comparte ni se envía a ningún servidor.
- Imprimible: cada módulo empieza en página nueva y las respuestas de los tests salen visibles.
- Accesibilidad: navegación por teclado, foco visible, contraste alto y `prefers-reduced-motion` respetado.

## Advertencias de contenido

- Los ejemplos usan una clínica que opera con Arthemis. Adapte los ejemplos si el curso se usa en otro contexto.
- El módulo 8 recuerda que los datos de salud son datos sensibles bajo la Ley 1581 de 2012. Este curso es formativo y no reemplaza la política de tratamiento de datos de la institución.
