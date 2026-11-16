# AGENTS.md — Sacrifice Inc. (Spec para agentes en este repo)

Este archivo define cómo trabajan los agentes (OpenCode) en este repositorio. Complementa el GDD y la arquitectura técnica; no los reemplaza.

## Proyecto
- **Sacrifice Inc.** · Dark Comedy / Puzzle Horror · Unity 6 LTS + URP · Low Poly · Blender → Unity.
- Director creativo y único "owner": lautarolopez748-wq (Cuervo0o). Los textos del juego van en **español**.
- Idioma de trabajo con el owner: español.

## Hardware del owner (restricción dura)
- Intel Pentium G4560 (2c/4h) · GTX 750 2 GB · 8 GB RAM · Windows 10.
- Implicaciones: Low Poly siempre, URP Forward simple, GI horneada, sombras < 30 m, texturas 512–1024, escenas pequeñas, Assembly Definitions, Editor lento → compilaciones y bakes espaciados. **Probar rendimiento en este equipo en cada milestone.**

## Discos
- **C: NO se toca.** D: es de solo lectura para el usuario (Admins). Todo en **E:\Sacrifice Inc**.
- Unity/Blender/cachés también en E:.

## Decisiones aprobadas (2026-11-16)
| Tema | Decisión |
|---|---|
| Motor | Unity 6 LTS (6000.x que ofrezca Hub) + URP |
| Cámara | Tercera persona sobre el hombro |
| Arquitectura desmembramiento | Híbrido modular: `BodyState` como fuente de verdad + props físicos con interfaces |
| Alcance MVP amputación | Brazos + piernas. Cabeza = muerte especial (cinemática/fail), no puzle |
| Idioma textos del juego | Español |
| Ritmo | 20+ h/semana |
| Git | Remoto privado `origin` = `lautarolopez748-wq/Sacrifice-Inc.` (el repo se llama así, **con punto final**) |
| Docs | GDD manda; TECHNICAL_ARCHITECTURE deriva de aquí |

## Reglas obligatorias
1. Inspección primero: estructura y docs antes de cambiar nada.
2. Propuesta antes de modificar; cambios de diseño requieren aprobación del owner y actualización del GDD.
3. Commits solo en milestones probados. **Nunca push sin autorización explícita del owner.**
4. No se eliminan funcionalidades ni archivos importantes sin autorización.
5. Paquetes: solo oficiales Unity y justificados. Sin Asset Store sin aprobación.
6. Sistemas modulares y reutilizables; nada de parches temporales con vocación de permanentes.
7. Comunicación directa y concreta; pasos manuales para el owner = numerados, con ruta exacta, esperando confirmación.
8. El owner no programa: automatiza lo posible, explica lo demás en lenguaje simple.
9. Verificar que compila + pruebas antes de dar por terminado un cambio.

## Docs (no duplicar)
- `GAME_DESIGN_DOCUMENT.md` — diseño y decisiones de juego (fuente de verdad).
- `TECHNICAL_ARCHITECTURE.md` — arquitectura técnica.
- `DEVELOPMENT_ROADMAP.md` — milestones y criterios de aceptación.
- `CHANGELOG.md` — historial de releases/milestones.
- `docs/` — decisiones puntuales si hicieran falta (no duplicar lo anterior).

## Convenciones
- Namespaces: `SacrificeInc.<Sistema>` (ej. `SacrificeInc.Body`).
- Código en `Assets/_SacrificeInc/Scripts/<Sistema>/`; asmdef por sistema.
- Nombres de assets: PascalCase, prefijos por tipo (SM_, SK_, M_, T_, A_, P_…).
- LFS para binarios (ver `.gitattributes`). Sin binarios grandes en commits de código.
