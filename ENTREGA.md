---

# Reporte de Evaluación: Micro-tarea y Notas de OpenSpec

---

## Parte 1: Evidencia de que OpenSpec está operativo

```
$ openspec --version
1.4.1
```

```
$ ls -R openspec/
openspec/:
changes  config.yaml  specs

openspec/changes:
archive

openspec/changes/archive:

openspec/specs:
```


## Parte 2: Evaluación de la Micro-tarea

**Objetivo:** Crear una función de formateo de fechas (ISO → "hace X minutos")

### Pilar 1 — Herramienta

* **📋 Guía / Pregunta:** Elección de la herramienta para la realización de la micro-tarea.
* **💡 Respuesta:** Si estuviera trabajando en el contexto de un proyecto más amplio, habría considerado un agente de IDE o CLI, pero en este caso solo necesito una función de forma aislada (en el vacío).

### Pilar 2 — Contexto

* **📋 Guía / Pregunta:** ¿Qué información estás aportando? (lenguaje, framework, restricciones, ejemplos…) ¿Hay algo del contexto que has decidido omitir conscientemente?
* **💡 Respuesta:**
  * **Información incluida en el contexto:**
  * **Lenguaje:** TypeScript
  * **Framework:** Ninguno
  * **Contexto general:** Colección de utilidades reutilizables que se pueden importar en otros proyectos bajo demanda.
  * **Buenas prácticas (*Dos*):** Seguir un diseño limpio, principio de responsabilidad única (SRP) y proporcionar pruebas unitarias.
  * **Prácticas a evitar (*Don'ts*):** Sobrediseñar (*over-engineer*) y utilizar librerías de terceros.

  * **Omitido de prompt inicial conscientemente:** Detalles sobre el framework de pruebas específico.
  * **Olvidado involuntariamente:** Reglas de estilo de código (*linting* / formateo).



### Pilar 3 — Prompt

* **📋 Guía / Pregunta:** ¿Cómo lo estructuras? (estilo, formato de salida, ejemplos…) Pega aquí el prompt final que vas a lanzar.
* **💡 Respuesta (Prompt Final Lanzado):**
> Necesito una función de utilidad que acepte una cadena de marca de tiempo UNIX UTC y devuelva una descripción del intervalo en formato legible para humanos entre el momento actual y dicha marca de tiempo.
> * **Comportamiento por defecto:** Mostrar la unidad de tiempo más significativa (1 unidad).
> * **Argumentos opcionales:** Aceptar un argumento opcional para especificar 1, 2 o 3 unidades de tiempo significativas.
> * **Redondeo:** Utilizar redondeo matemático.
> * **Conversión automática de unidades significativas:**
> * 60 seg -> min
> * 60 min -> h
> * 24 h -> d
> * 7 d -> w (semanas)
> 
> 
> * **Soporte temporal:** Debe soportar intervalos tanto pasados como futuros.
> * **Ejemplos de resultados esperados:**
> * "hace 10 minutos" (*10 minutes ago*)
> * "hace 1 semana, 2 días y 24 minutos" (*1 week, 2 days and 24 minutes ago*)
> 
> 
> * **Entregables:** Especificar archivos de origen/prueba individuales e instrucciones detalladas para ejecutar las pruebas.
> 
> 



### Resultado

* **📋 Guía / Pregunta:** ¿Funcionó a la primera o tuviste que iterar? Una mejora que harías si volvieras a hacerlo.
* **💡 Respuesta:**
  * **Iteración y dificultades:** Tuve que iterar debido a que el contexto no era lo suficientemente claro; inicialmente la IA generó una sola función de gran tamaño. Además, encontré un pequeño problema al ejecutar las pruebas unitarias. Por último, una de las pruebas no pasó de forma automática y tuvo que ser ajustada manualmente.
  * **Resultado final:** Las funciones resultantes terminaron siendo más grandes de lo que había anticipado.
  * **Mejoras para el futuro:**
    1. Si tuviera que hacerlo de nuevo, probablemente usaría un agente de IDE/CLI para evitar tener que copiar y pegar manualmente grandes fragmentos de código, y para contar con una mejor vista de diferencias (*diff view*) de los cambios.
    2. Dado que olvidé mencionar algunos aspectos en el contexto inicial y terminé teniendo que pensar sobre la marcha en las reglas de negocio al definir el prompt, en una próxima ocasión intentaría usar el modo de planificación del agente (*plan mode*) para obtener una ayuda básica que me permita identificar y definir los detalles faltantes desde el principio.

---

## Parte 3: Notas sobre OpenSpec

*(Observaciones y comentarios sobre el sistema)*

1. **Estructura interna:** Los comandos y las habilidades (*skills*) están extremadamente bien descritos y cuentan con una estructura interna muy clara.
2. **Flujo de trabajo de reversión:** En la documentación se menciona la posibilidad de regresar en el flujo de trabajo en cualquier punto para realizar actualizaciones en etapas anteriores. Sin embargo, actualmente no me queda claro cómo "indicarle" o enviarle una señal al agente de que debe volver atrás. Entiendo perfectamente que se utiliza `opsx:continue` para avanzar en el flujo de trabajo, pero no parece haber un equivalente para retroceder a una etapa previa y rehacerla con base en las ediciones del archivo Markdown o en nuevos prompts adicionales.
3. **Redundancia de archivos:** Tanto las habilidades (*skills*) como los comandos parecen contener archivos Markdown casi idénticos. Por ejemplo, al contrastar `.gemini/commands/opsx/propose.md` y `.gemini/skills/openspec-propose/SKILL.md` con una herramienta de diferencias (*diff tool*), algunas discrepancias no son obvias. Sorprende que no se haya realizado un intento de centralizar las instrucciones para reutilizarlas en la definición de habilidades y comandos, evitando así la duplicidad.