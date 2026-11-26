# Agentes que se pueden auditar

Un molde para construir agentes con Claude Code. Convierte "quiero un agente que…" en un repositorio con
objetivo verificable, contrato de salida, guardrails que fallan cerrado y evals que alguien vio ponerse en rojo.

**Página:** https://drachenjager.github.io/agentes-auditables/

## En corto

- **Primero el objetivo, después el agente.** Trabajo, métrica, valor de hoy, meta con fecha, grupo de
  control, restricción dura y condición de paro. Lo que no se sabe va en `null`.
- **La salida es un contrato.** Sólo JSON, categorías cerradas y un valor explícito para "no sé". Cada
  conclusión cita la frase que la sostiene.
- **Lo que obliga no vive en el prompt.** Permisos y hooks deterministas, cada uno con un eval que lo ve bloquear.
- **El modelo no elige de quién son los datos.** La llave la pone quien orquesta.
- **Un error del servicio nunca es un dato.**
- **Hasta no verlo en rojo, un eval no mira nada.** Cada eval tiene su par y su mutación.

## Lo que aprendí probando Claude Code (noviembre de 2026, versión 2.1)

| Lo que probé | Lo que pasó |
|---|---|
| Un hook previo que sale con código 2 | El comando no corre |
| El mismo hook, pero truena y sale con 1 | El comando sí corre |
| Igual, con `"onFailure": "block"` | El comando no corre |
| Un control en bash con `pipefail` y `grep -q` | En entradas grandes deja pasar lo que debía bloquear |
| Un subagente directo con `--agent` y `--json-schema` | El esquema se ignora sin avisar |
| El hook de inicio de sesión en una corrida sin persona | También se dispara |
| `allowed-tools` en una skill | Preaprueba, no restringe |

## Alcance

Esta página describe una metodología. La implementación y los agentes construidos con ella viven en
repositorios privados.
