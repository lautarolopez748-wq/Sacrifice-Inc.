# GAME_DESIGN_DOCUMENT.md — Sacrifice Inc.

> **Fuente de verdad del diseño.** Nada aquí se cambia sin aprobación del director creativo (Cuervo0o). Las decisiones no tomadas se marcan como **PENDIENTE** y se proponen, nunca se asumen.
>
> Última actualización: 2026-11-16 (Fase 0)

## 1. Identidad
- **Nombre:** Sacrifice Inc.
- **Género:** Dark Comedy / Puzzle Horror.
- **Tagline:** *Your body. Our business.*
- **Premisa:** una corporación, **Integrity Corp.**, experimenta con humanos bajo un envoltorio empresarial profesional. El protagonista, convertido en **SUJETO #049** por un contrato engañoso, descubre que su cuerpo es materia prima y herramienta a la vez.
- **Motor/arte:** Unity 6 LTS + URP · Low Poly · flujo Blender → Unity.
- **Textos del juego:** Español (los nombres/marcas de Integrity Corp. pueden conservar estilo corporativo en inglés como recurso satírico).

## 2. Pilares de diseño
1. **Cuerpo como recurso.** El desmembramiento estratégico es la mecánica central, no un efecto. Las partes del cuerpo son objetos físicos con usos de puzle (peso, presión, encaje, accionamiento) y restricciones de locomoción.
2. **Humor negro corporativo.** La contradicción entre lenguaje empresarial profesional y situaciones grotescas es la fuente principal de comedia. Integrity Corp. presenta todo como "procedimiento estándar", "oportunidad de mejora" y "protocolo de seguridad".
3. **Puzzles ambientales.** Se resuelven entendiendo la instalación y sus procedimientos, no con reflejos.
4. **Narrativa ambiental progresiva.** Se cuenta a través del entorno: carteles, memos internos, contratos, instrucciones, grabaciones, señalización industrial, comunicaciones automáticas.

**Anti-pilares (lo que NO es este juego):** shooter genérico · survival horror de jumpscares · físicas sin dirección · copia de otras obras.

## 3. Cámara y controles (aprobados 2026-11-16)
- **Tercera persona, sobre el hombro.** El jugador debe ver su propio cuerpo y las partes que le faltan: la mecánica exige lectura visual del cuerpo.
- Movimiento a pie; sin parkour ni combate armado como foco. **PENDIENTE:** esquema final de controles (se diseña con el prototipo M1). **PENDIENTE:** si hay salto y en qué contextos.

## 4. Mecánica principal: DESMEMBRAMIENTO ESTRATÉGICO
> Estado: **concepto aprobado; especificación de juego en construcción durante los hitos M2–M3.**

- Las partes pierden estatus funcional al desprenderse, pero **persisten como objetos físicos** interactivos.
- **Alcance MVP:** brazos y piernas (4 partes amputables). La cabeza es un caso especial: **muerte especial** (evento narrativo/derrota), nunca una solución de puzle.
- Efectos jugables previstos (a validar por hitos):
  - Activar mecanismos (palancas, botones con formas compatibles).
  - Introducir extremidades en dispositivos (máquinas de fichaje/implante/calibración).
  - Activar placas de presión o mecanismos de peso.
  - Superar obstáculos que requieren sacrificio corporal (huecos, cuchillas, bloqueos).
  - Alterar la locomoción: cojear (1 pierna), reptar (2 piernas o tren inferior), alcance reducido (brazos).
- **Amputación voluntaria vs. forzada:** el diseño debe distinguir entre perder una parte por evento de sala y "sacrificarla" para resolver un puzle. **PENDIENTE (diseño M2/M3):** cómo se amputa voluntariamente (herramienta, contexto, menú) y si tiene coste/respawn de partes.
- Las partes usadas en un puzle pueden quedar consumidas/bloqueadas en el mecanismo: el juego debe tratar el cuerpo como **presupuesto agotable**. **PENDIENTE:** si existen formas de recuperar partes.
- **Anti-abuso:** los puzles deben depender de la parte correcta en el contexto correcto (peso, tamaño, "lado"), no solo de "algo con física".

## 5. Mundo y narrativa
- **Integrity Corp.** como corporación ficticia global aplicada. Procedimientos con nombre ("Procedimiento 49-A", "Calibración de Excelencia", etc. — **PENDIENTE:** corpus de nombres).
- **SUJETO #049**: identidad del protagonista dentro del sistema; cuestionarios, fichas, formularios obligatorios.
- Tono: profesional, amable y vacío. Mensajes automáticos. Señalización de seguridad absurda. Formularios de consentimiento incomprensibles.
- **Estructura narrativa:** ambiental y progresiva; sin exposición directa ni personajes que "expliquen" la trama. Posible guía "Bienvenida del Facilitador".
- **PENDIENTE (no decidir unilateralmente):** historia completa, arco del protagonista, personajes secundarios (FACILITADORES, etc.), final, motivo de la captura y naturaleza exacta de los experimentos. Se proponerán por escrito para aprobación antes de integrarlos.

## 6. Dirección artística
- **Low Poly 3D**, coherencia antes que detalle. Nada de realismo: siluetas limpias, geometría simple, materiales planos con gradiente sutil.
- **Arquitectura:** brutalista + industrial + quirúrgica + corporativa. Hormigón, chapa, tuberías, cabinas estériles, cartelería de seguridad, pantallas apagadas, maquinaria pesada.
- **Paleta Integrity Corp.:** negro, gris, blanco, rojo (señalización/acento). Frío, artificial, controlado.
- **Iluminación:** emergencia y quirófano; tubos fríos, señales rojas, pasillos en penumbra con focos puntuales. GI horneada (Bake), nunca realtime caro.
- **UI:** estética de intranet corporativa — formularios, sellos, códigos de barras, marcas de agua de "Documento Interno".

## 7. Audiencia y plataforma
- PC, gama baja/media (el hardware de desarrollo es el objetivo mínimo).
- Público: jugadores de puzzle-horror con gusto por el humor negro y la sátira corporativa.
- **PENDIENTE:** clasificación/tono público final y duración objetivo (se definen tras el prototipo).

## 8. Decisiones abiertas (requieren aprobación)
1. Historia completa y arco del Sujeto #049.
2. Personajes secundarios (si los hay).
3. Esquema de controles definitivo y salto.
4. Sistema de amputación voluntaria (cómo, dónde, con qué interfaz).
5. Economía de partes: recuperación, respawn, consumo en puzles.
6. Diagrama de niveles/laberinto de la instalación (Fase 5).
7. Audio: dirección sonora y musical (Fase 5).
8. Duración y estructura de acto/capítulo.

## 9. Estado actual
Fase 0 (Preparación). Ver `DEVELOPMENT_ROADMAP.md`.
