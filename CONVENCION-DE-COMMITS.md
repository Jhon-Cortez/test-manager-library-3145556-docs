# Convención de commits — Manager Library

Aplica a los **seis repositorios** del reto (`docs`, `api`, `app`, `page`, `infra`, `tool`). Es una convención
técnica: no cambia el alcance ni las reglas de negocio de [`spec-.net/`](spec-.net/) ni de [`spec-python/`](spec-python/).

## Formato

```text
<tipo>(<ámbito>): <resumen>

<cuerpo opcional: por qué, no qué>

<pie opcional>
Refs: T-xx, HU-xx, CA-xx.x, RN-x, RNF-x, ADR-xxx, Issue #n
```

- **Resumen**: imperativo, lowercase start, no trailing period, ≤ 72 characters.
- **Idioma del mensaje: inglés** (tipo, ámbito, resumen, cuerpo y pies). La documentación
  del producto y los mensajes al usuario siguen en español (artículo XI de la constitución).
- **Cuerpo**: explica el porqué, no el qué; se separa del resumen con una línea en blanco.
  Ancho ≤ 72 caracteres.

## Tipos

| Tipo | Cuándo |
|---|---|
| `feat` | Nueva funcionalidad del producto |
| `fix` | Corrección de un comportamiento erróneo |
| `docs` | Solo documentación (spec, ADR, README, esta convención) |
| `test` | Añadir o corregir pruebas sin tocar comportamiento |
| `refactor` | Cambio interno sin cambiar comportamiento observable |
| `perf` | Mejora de rendimiento |
| `build` | Docker, dependencias, empaquetado |
| `ci` | Integración continua |
| `chore` | Mantenimiento (formato, limpieza, tareas sueltas) |

## Ámbitos

`domain`, `application`, `adapters`, `api`, `app`, `page`, `infra`, `tool`, `docs`, `spec`.
En `docs` se prefiere el archivo afectado cuando aporta precisión (p. ej. `docs(data-model)`).

## Reglas

1. **Un commit = un cambio lógico.** No mezclar decisiones de spec con código de otra cosa.
2. **Orden obligatorio cuando el commit nace de una decisión o de una incongruencia del spec:**
   1. commit `docs(...)` con la corrección en el spec (el alcance §2 **nunca** se toca);
   2. `push` de `docs`;
   3. recién entonces el commit de código que implementa esa decisión.
   El cuerpo del commit de código cita el commit de docs que la precede.
3. **Toda tarea terminada cita su evidencia** (artículo XII): prueba, comando o recorrido que lo demuestra.
4. **Referencias** en el pie: use solo las que apliquen (`Refs: T-13, ADR-002, Inc #1`).
5. **Prohibido:** secretos (`.env` real, claves, hashes precalculados), resúmenes tipo `wip` o `fix stuff`,
   y commits de formato que de paso cambien lógica.
6. Un `fix` que corrija una tarea ya cerrada reabre la evidencia: el cuerpo explica qué prueba fallaba.

## Ejemplos

```text
docs(data-model): declare the book version witness (Issue #1)

ADR-002, plan D-04 and T-13 require a version witness on book, but §3
did not declare it and §10 would flag the column as extra. The version
column is documented and its mark in §4 is reclassified.

Refs: ADR-002, T-13, Issue #1
```

```text
feat(loans): register loans with limit of 3 and overdue checks

Implements HU-06 behind LendBooksService. The Quantity (>= 0) decision
was fixed in docs first: 9f3a1c2.

Refs: HU-06, CA-06.4, CA-06.5, T-09
```

```text
test(health): cover GET /api/v1/health (T-01)

Refs: T-01
```
