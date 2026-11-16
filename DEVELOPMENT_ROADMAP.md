# DEVELOPMENT_ROADMAP.md — Sacrifice Inc.

> Hoja de ruta realista. Ritmo declarado por el owner: **20+ h/semana**. Las duraciones son estimaciones honestas para un proyecto en solitario con curva de aprendizaje y hardware modesto; se recalibran al cerrar cada milestone.

## Estado actual: M0 — Preparación
**Objetivo:** entorno funcional, repo limpio, proyecto Unity creado con URP, docs en su sitio.

### Tareas
- [x] Análisis de entorno y hardware (2026-11-16)
- [x] Estructura de carpetas y convenciones
- [x] Git init + `.gitignore` + `.gitattributes` (LFS)
- [x] Docs iniciales (README, AGENTS, GDD, Arquitectura, Roadmap, Changelog)
- [x] Unity Hub 3.22.6 (MSIX) + Unity **6.3 LTS (6000.3.28f1)** instalado vía Hub en `E:\Nueva carpeta (2)\6000.3.28f1` (ruta no estándar conservada; el Hub la conoce)
- [x] Blender **4.5.10 LTS** en `E:\Tools\Blender`
- [x] Proyecto Unity creado en `E:\Sacrifice Inc` (proyecto aplanado desde anidado) + **URP 17.3.0** verificado en `Packages/manifest.json`, proyecto compila en modo batch (exit 0)
- [x] Git LFS instalado (`git lfs install`) + primer commit M0
- [ ] Push del hito M0 (solo con autorización del owner)

> Nota: el componente *Windows Build Support (IL2CPP)* quedó instalado vía Hub; el componente *Microsoft Visual Studio Community 2026* falló a propósito y se ignoró (no es necesario; Mono basta para builds de prototipo).

### Criterios de aceptación
- Unity abre el proyecto sin errores de consola.
- Play en escena vacía, URP activo (pipeline asset asignado).
- `git status` limpio tras commit.

---

## M1 — Greybox y controles
**Objetivo:** Sujeto #049 se mueve por una escena de prueba; cámara y HUD mínimos.

- Blockout ProBuilder de sala de pruebas industrial (pasillo + 1 sala + puerta).
- Cápsula de personaje (placeholder SM) + `LocomotionController` (perfil `Normal`).
- Cámara Cinemachine over-shoulder; Input System; 1 `IInteractable` de prueba.
- Escena `Test_Gym`. HUD mínimo (prompt de interacción).
- **Aceptación:** caminar, girar cámara, interactuar con un objeto; 60 fps en el equipo del owner; commit + tag `m1-greybox`.

## M2 — Sistema corporal v1
**Objetivo:** restaurar presencia de mecánica núcleo.

- `BodyState` + `BodyPartDefinition` + `BodySystem` + `AmputationService` (amputación por comando de debug: tecla/log).
- Props físicos de brazos/piernas con pickup/throw.
- Perfiles `Limp` / `Crawl` + máscaras de animación; 1 animación stand-in por perfil.
- Serialización básica de `BodyState` (prueba en EditMode).
- **Aceptación:** amputar brazo izquierdo y pierna derecha vía debug; prop aparece, se puede recoger; locomoción cambia en consecuencia; tests EditMode verdes; tag `m2-body-v1`.

## M3 — Primer puzle completo
**Objetivo:** bucle núcleo completo en una sala: amputar → transportar → encajar → avanzar.

- 1 sala greybox con narrativa ambiental mínima (1 memo, 1 cartel de "Procedimiento 49-A").
- `MechanismSocket` + `WeightPlate` + `PuzzleGoal` (abre puerta de salida).
- Feedback corporativo del mecanismo (mensaje de intranet / sello "TRÁMITE ACEPTADO").
- **Aceptación:** la sala se resuelve usando una extremidad propia; todo el flujo sin herramientas de debug; playtest completo en < 10 min; tag `m3-first-puzzle`.

## M4 — Verificación y build
**Objetivo:** milestone verificable fuera del editor.

- Medición de rendimiento (stats, frame debugger) y correcciones.
- Build Windows (Development Build) + corrección de errores de empaquetado.
- Revisión GDD/Arquitectura; changelog.
- **Aceptación:** .exe arranca en limpio (sin Unity), escena de puzle jugable, 30–60 fps, tag `m4-prototype`.

---

## Fases posteriores (no comprometidas aún)
- **Fase 4 — Identidad visual:** modelos definitivos low-poly del Sujeto #049 y escenario, materiales, iluminación Integrity Corp.
- **Fase 5 — Experiencia de juego:** niveles, narrativa ambiental completa, audio, UI, progresión, dificultad.
- **Fase 6 — Pulido:** optimización, QA, primera versión distribuible.

## Calendario estimado (20+ h/sem)
M1: ~2 semanas · M2: ~3–4 semanas · M3: ~2–3 semanas · M4: ~1 semana → **prototipo jugable en ~8–10 semanas** tras completar M0. Se confirmará al cerrar cada hito.

## Reglas del roadmap
- Un milestone roto no se commitea; primero se arregla o se revierte.
- Ningún hito se adelanta a petición de scope; nuevas ideas → backlog/GDD pendiente de aprobación.
- Push de cada tag solo con autorización del owner.
