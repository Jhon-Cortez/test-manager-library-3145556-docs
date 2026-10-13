# Convención de commits — Manager Library

Aplica a los **seis repositorios** del reto (`docs`, `api`, `app`, `page`, `infra`, `tool`). Es una convención
técnica: no cambia el alcance ni las reglas de negocio de [`spec-laravel/`](spec-laravel/) ni de [`spec-python/`](spec-python/).

## Formato

```text
<tipo>(<ámbito>): <resumen> [(referencias)]
```

- **Una sola línea. Sin cuerpo ni pies:** la motivación vive en el spec, el código y las pruebas.
- **Resumen**: imperativo, minúscula inicial, sin punto final.
- **Referencias** opcionales al final, entre paréntesis y separadas por comas: `(HU-06, T-09)`.
  Use solo las que apliquen: `T-xx`, `HU-xx`, `CA-xx.x`, `RN-x`, `RNF-x`, `ADR-xxx`, `Issue #n`.
- **Idioma: inglés** (tipo, ámbito y resumen). La documentación del producto y los mensajes al
  usuario siguen en español (artículo XI de la constitución).

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
3. **La evidencia no se promete en el mensaje: se ejecuta** (artículo XII). Cada tarea cerrada
   tiene una prueba o comando en el repositorio que la demuestra.
4. **Ramas:** el trabajo sube a `develop`; `main` solo recibe entregas consolidadas.
5. **Prohibido:** secretos (`.env` real, claves, hashes precalculados), resúmenes tipo `wip` o
   `fix stuff`, y commits de formato que de paso cambien lógica.
6. Un `fix` que corrija una tarea ya cerrada reabre su evidencia: añada o corrija la prueba.

## Ejemplos

```text
build(api): bootstrap Laravel 12 application skeleton (T-01)
feat(health): expose GET /api/v1/health (T-01)
docs(data-model): declare the book version witness (ADR-002, Issue #1)
feat(loans): register loans with limit of 3 and overdue checks (HU-06, T-09)
test(health): cover GET /api/v1/health (T-01)
```
