# TECHNICAL_ARCHITECTURE.md — Sacrifice Inc.

> Derivada del GDD (`GAME_DESIGN_DOCUMENT.md`) y de las decisiones aprobadas por el owner. Se actualiza en cada hito que toque arquitectura.
>
> Última actualización: 2026-11-16 (Fase 0)

## 1. Pila técnica
- **Motor:** Unity 6 LTS + URP (Universal Render Pipeline), Forward simple, SRP Batcher.
- **Lenguaje:** C# (estándar .NET de Unity).
- **Paquetes oficiales justificados:** Universal RP · Input System (reemplaza al Input Manager clásico) · Cinemachine (cámara over-shoulder) · ProBuilder (blockout/greybox) · TextMeshPro (UI/fuentes) · Test Framework (editmode/playmode). Nada más sin aprobación.
- **Modelado:** Blender 4.x LTS → export FBX/GLB con escala métrica, pivotes correctos, nombres PascalCase (SM_/SK_/M_/T_/A_).
- **Versionado:** Git + Git LFS (`.gitattributes`). Docs en raíz del repo; código bajo `Assets/_SacrificeInc/`.

## 2. Restricciones de rendimiento (hardware del owner = mínimo objetivo)
- Intel G4560 · GTX 750 2 GB · 8 GB RAM · Windows 10.
- Presupuesto de escena (objetivo): ≤ 60–80k tris visibles, ≤ 150 draw calls en la vista típica, GI horneada, sombras ≤ 30 m, texturas ≤ 1024 (excepcionalmente 2048 en héroes), sin reflexión/screen-space caros, fog volumétrica solo si rinde.
- Assembly Definitions por sistema → recompilación incremental en CPU lenta.
- Sin sistemas de pooling genéricos hasta que haga falta; sí pooling de props de partes (se instancian/destruyen raramente: ciclo de amputación).
- Pruebas de rendimiento en CADA milestone (stats overlay + frame debugger).

## 3. Principios
1. Módulos cohesivos con responsabilidad única; comunicación por eventos/interfaces, no por referencias duras.
2. Datos de configuración en ScriptableObjects; estado de partida en estructuras serializables.
3. MonoBehaviours finos: lógica de juego en clases puras cuando sea razonable y testeable.
4. Nada de singletons globales salvo `GameState`/servicios explícitos y documentados.
5. Determinismo de estado corporal: `BodyState` es la única fuente de verdad.

## 4. Sistemas y responsabilidades

### 4.1 Core (`SacrificeInc.Core`)
- `GameState`: partida actual (progreso, `BodyState`, flags narrativos). Serializable a JSON para guardado futuro.
- `EventChannel` (SO) o eventos C# in-place: `OnBodyPartLost`, `OnPartEnteredSocket`, `OnPuzzleSolved`, `OnSubjectDied`.
- `SceneFlow`: Boot → Menú → Test/Levels. Carga aditiva solo si rinde.

### 4.2 Body (`SacrificeInc.Body`) — núcleo del juego
- `BodyPartId` enum: `Head, Torso, ArmLeft, ArmRight, LegLeft, LegRight`.
- `BodyState` (struct serializable): partes presentes (flags), partes "gastadas"/consumidas opcionalmente en puzles, timestamp de última amputación. Fuente única de verdad.
- `BodyPartDefinition` (SO): id, etiqueta, masa, volumen, prioridad de locomoción, prefab de prop, icono UI.
- `BodySystem`: registra el esqueleto/jerarquía del Sujeto #049; suscripción a eventos de daño/amputación; aplica `BodyState` (activa/desactiva partes del cuerpo instanciado).
- `AmputationService.Detach(BodyPartId, Cause)`:
  1. Valida (parte presente, no Torso/Head salvo muerte especial).
  2. `BodySystem` desactiva/oculta la parte del personaje.
  3. Instancia prop físico: `Rigidbody` + collider convexo simple + `BodyPartProp` + `ISocketable` + `IWeightCarrier`.
  4. Dispara `OnBodyPartLost(partId, cause, propInstance)`.
  5. Locomoción relee `BodyState` y cambia de perfil (ver §4.3).
- `BodyPartProp`: interactuable físico (agarrable/lanzable). No conoce puzles; solo implementa interfaces.
- Interfaces: `ISocketable` (id, masa, volumen, lado), `IWeightCarrier`, `IInteractable`. Puzles consumen interfaces, nunca tipos concretos de extremidad.
- Cabeza: `Head` solo admite `Detach(cause: Fatal)` → muerte especial + fin de partida. Sin prop usable.

### 4.3 Locomotion (`SacrificeInc.Locomotion`)
- `LocomotionController`: lectura de `BodyState` → `LocomotionProfile` activo.
- Perfiles: `Normal` · `Limp` (1 pierna) · `Crawl` (sin piernas o tren inferior incompleto) · `OneArm`/`NoArms` como modificadores de acción (alcance, aguante).
  - Extensión prevista sin reescritura: perfiles por número/combinación de partes vía tabla en `LocomotionProfiles.asset` (SO).
- Animator: base layer + **Avatar Masks por región** (brazos/piernas/torso) para evitar explosión combinatoria 2^N; transiciones suaves; blend por parámetro de perfil.
- CharacterController o cápsula + resolución de suelos simple; escalones y pendientes limitados por diseño de nivel (sin parkour).

### 4.4 Interaction (`SacrificeInc.Interaction`)
- `InteractionSystem`: raycast/icono contextual desde cámara (over-shoulder), distancia ≤ 2 m, resalte por emisivo barato.
- `IInteractable`: `Focus`, `Unfocus`, `Interact(Interactor)`.
- Grab/throw de props (fuerza desde perfil de brazos); capacidad de carga limitada por BodyState.

### 4.5 Puzzles (`SacrificeInc.Puzzles`)
- `MechanismSocket`: acepta `ISocketable` (filtros: lado, minMasa, volumen). Al encajar: evento + enclavamiento del prop (kinematic, parenting o destrucción según config — ver GDD §4 sobre "partes consumidas").
- `WeightPlate`: acepta `IWeightCarrier`; umbral de masa (`minKg`); mantiene pulsado por tiempo o hasta retirar.
- `TriggerOnPartPresent` / lógica de combinación: producto cartesiano de señales (sin FSM compleja; SO `PuzzleRule` declara condiciones + resultado).
- Un puzle completo = greybox de sala + N mecanismos + `PuzzleGoal` (abre puerta / alimenta máquina / revela vano).
- Reutilización estricta: los puzles no referencian `ArmLeft` etc., siempre interfaces.

### 4.6 UI (`SacrificeInc.UI`)
- HUD mínimo: salud opcional (posiblemente NO hay barra de vida tradicional — **PENDIENTE GDD**), prompts de interacción (estilo intranet), sello de "SUJETO #049".
- Menús: arranque Boot → Menú → partida. Texto en español; fuentes del pack URP/TMP oficial.

### 4.7 Testing (`Tests/`)
- EditMode: `BodyState` (amputar/restaurar/serializar), evaluación de `PuzzleRule`, filtros de socket.
- PlayMode: amputación end-to-end (prop instanciado, locomoción cambia), puzle de referencia (socket + placa), muerte por cabeza.

## 5. Arquitectura de datos y guardado
- `BodyState` y flags de progreso serializables a JSON en `Application.persistentDataPath` (Fase 5). Checkpoints por escena de nivel. Nunca guardar partes como refs de escena.

## 6. Convenciones
- Código C#: PascalCase tipos/métodos, camelCase locales, `_camelCase` campos privados serializados, `[SerializeField] private` siempre (nada público por inspector).
- asmdef por sistema + referencias unidireccionales (Puzzles → Interaction → Body → Core; nunca al revés salvo eventos).
- Prefabs de sistema: `P_<Dominio>_<Nombre>`; modelos `SM_`, rigs `SK_`, materiales `M_`, texturas `T_`, animaciones `A_`.
- Escenas: `Boot`, `Menu`, `Test_*`, niveles en `Environments/Facility_xx`.

## 7. Flujo Blender → Unity
- Unidades métricas; apply scale; pivotes en la base/articulación según corresponda; normales suavizadas coherentes con Low Poly (flat shading donde toque).
- Rig humanoide compatible con Unity Avatar para el Sujeto #049; partes separables vinculadas al mismo esqueleto.
- Export FBX 7.4 · escala 1 · sin animaciones embebidas si son grandes (archivos separados).

## 8. Riesgos abiertos (ver AGENTS/GDD)
Combinatoria de animaciones (mitigada con máscaras) · reptar sin piernas (animación difícil) · física de props (colliders convexos simples + solver por defecto) · editor lento (asmdefs) · dependencia del propietario en Blender (guías paso a paso).

## 9. Registro de decisión
| Fecha | Decisión | Autor |
|---|---|---|
| 2026-11-16 | Tercera persona over-shoulder | Owner |
| 2026-11-16 | Híbrido modular desmembramiento (BodyState + props con interfaces) | Owner |
| 2026-11-16 | MVP: brazos+piernas; cabeza = fatal | Owner |
| 2026-11-16 | Unity 6 LTS + URP forward simple | Owner |
| 2026-11-16 | Textos en español | Owner |
