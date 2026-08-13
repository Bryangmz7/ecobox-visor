# HANDOFF — Diseño físico del EcoBox (el tacho)

> Para la IA que retome el diseño del tacho. Esto es un hilo de trabajo separado del Company OS en Notion — aquí se diseña el producto físico, no se gestiona el negocio. Si necesitas contexto de negocio (equipo, OKRs, mercado), ve primero a `../EcoPoint 2026/HANDOFF.md`.
> Última actualización: 11 de agosto de 2026 — sesión de esqueleto visual + arquitectura interna + modelado 3D.

---

## 0. Léeme primero — estado en una línea

**Exterior (Paso 2 del proceso): cerrado y aprobado**, con una excepción sin resolver (puerta de depósito, ver §5). **Arquitectura interna: bosquejada en 2D y modelada en 3D interactivo**, referencial — Hames la valida. **Paso 3 (render final en color): no iniciado**, espera el diseño del vinilo de fachada.

Todos los entregables de esta sesión — planos y modelos 3D — están listados con sus links en **§8**. Si vienes a continuar el trabajo, empieza por ahí y por los pendientes de **§5**.

---

## 1. Tu rol

Eres el diseñador industrial/producto asesorando a Bryan en el diseño del EcoBox. Bryan da la dirección y decide; tú produces el trabajo (texto → wireframe → render) y asesoras con fundamento (ergonomía, fabricabilidad), no solo ejecutas. **El handoff no es un contrato rígido** — Bryan prefiere que reacomodes con criterio propio antes que seguir al pie de la letra algo que ya no tiene sentido; ver `../../memory` del asistente, memoria `ecopoint-diseno-tacho-criterio`.

**El proceso acordado, en orden, sin saltarse pasos:**
1. Especificación en texto (zonas, medidas, qué va dónde y por qué) — ✅ cerrado
2. Esqueleto visual — bloques y proporciones, sin color — ✅ cerrado (§4, §8)
3. Render final en color, con la paleta e identidad de marca de EcoPoint — ⏳ no iniciado, espera vinilo de fachada
4. Esa propuesta se entrega a **Hames** (dueño de Producto/Tecnología), quien la afina a 3D real y valida fabricabilidad — parcialmente adelantado: ya existe un 3D interactivo referencial (§8) que Hames puede tomar como punto de partida, no como versión final

**Nota sobre la regla original de "primero el exterior completo, el interior se resuelve después en el modelado 3D":** Bryan pidió explícitamente adelantar el interior en esta sesión (embudo/rampa, compuerta, sensores, cableado) como bosquejo referencial, antes de la entrega formal a Hames. Sigue siendo referencial — los componentes exactos, calibres de cable y factibilidad real quedan a criterio de Hames — pero ya no es un espacio en blanco.

---

## 2. Dimensiones confirmadas

**80cm ancho × 70cm profundidad × 175cm alto.** Sin cambios esta sesión.

---

## 3. Las 4 zonas verticales

| Zona | Altura | Contenido (estado actual) | Notas |
|---|---|---|---|
| **1. Zócalo** | 0–15cm | Anclaje, patas niveladoras, alimentación 220V + respaldo | No decorativo — evita que el tacho se tambalee |
| **2. Depósito** | 15–100cm | Bolsa de botellas removible (**206 L ≈ 93 botellas**) + bandeja de tapas separada | Bolsa dimensionada al volumen real de la zona; ver §5 conflicto con la puerta |
| **3. Interacción** | 100–140cm | Boca circular ~11cm Ø + buzón de tapas + rampa cerrada con barrera IR y sensor de material | Reemplaza al "embudo + sensor HC-SR04" del diseño original — ver §4 |
| **4. Cabezal** | 140–175cm | Pantalla táctil vertical + wordmark **"Ecopoint"** (solo, sin "El Nodo" en esta etapa) + antena 4G | Pantalla pegada al límite inferior del cabezal, no al tope |

---

## 4. Decisiones de diseño cerradas esta sesión

Además de las ya cerradas antes (pantalla recta, logo en cabezal, puertas al mismo costado, seguridad diferenciada — siguen vigentes):

1. **Boca circular horizontal, ~11cm Ø**, no una compuerta rectangular — la botella entra acostada y de punta; el diámetro mismo resuelve la orientación sin mecanismo. Dimensionada para botella personal: 1L holgado, 1.5L justo.
2. **Rampa continua a 50–60°, no un embudo con codo de 90°.** Una botella de 30cm no puede girar 90° dentro de un ducto de 11cm — se atoraría siempre. La rampa es una sola superficie sin esquinas.
3. **Rampa cerrada con tapa (ducto), no un canal abierto.** Sin tapa, una mano entra por la boca y alcanza los sensores y el cableado — como el conteo es el producto que se vende, eso es un hueco de fraude.
4. **Barrera infrarroja reemplaza al HC-SR04 para contar.** El HC-SR04 mide distancia, no cuenta objetos discretos con precisión. El HC-SR04 se **reubicó** a medir nivel de llenado de la bolsa, donde sí sirve.
5. **Sensor de material** (inductivo o celda de carga) — nuevo, no existía en la lista original. Es el componente que cumple la promesa de "solo PET": descarta lata y vidrio del conteo.
6. **Sensor de puerta abierta** — nuevo. Pausa el conteo durante el vaciado para que un mantenimiento no se registre como depósitos.
7. **Tapas separadas de botellas.** Buzón propio junto a la boca, ducto vertical independiente (pendiente ≥75°, no puede ir casi horizontal o la tapa no desliza), bandeja aparte en la franja frontal del depósito.
8. **Bolsa removible con marco rectangular** (no aro circular) — dimensionada al volumen real de la zona 2: **206 L ≈ 93 botellas**, ~3kg llena. La primera versión de este modelo tenía 81L / 35 botellas, insuficiente para que el cliente la vacíe sin visitas frecuentes.
9. **Gabinete estanco IP65 con tapa de policarbonato**, no un "compartimento sellado" genérico — así lo monta un instalador real: gabinete normado atornillado a la trasera, con prensaestopas, no media máquina sellada.
10. **Canaleta ranurada** para todo el cableado — troncal del zócalo a la zona de control, más ramales cortos. Ningún conductor cruza el aire ni el camino de la botella.
11. **El ESP32 dispara el POST a Supabase, no el kiosko.** Corregido en `01-estrategia/CONTEXTO-TACHO-ECOBOX.md` y `ecopoint/docs/HARDWARE.md` — ver §9. El kiosko le pasa el DNI al ESP32 por serial; el conteo nunca pasa por una interfaz web.
12. **Antena 4G física** agregada al modelo — no existía; el cable de conectividad terminaba en el aire.
13. **Cabezal: solo "Ecopoint"** en el wordmark, sin "El Nodo" (a diferencia del handoff original) — decisión explícita de Bryan para esta etapa del diseño exterior.

---

## 5. Pendientes — ninguno bloquea seguir trabajando, pero hay que cerrarlos

| # | Pendiente | Detalle | Quién decide |
|---|---|---|---|
| 1 | **Puerta de depósito muy angosta** | La bolsa mide 76cm de alto; la puerta lateral solo 41cm. La bolsa no sale sin deformarse. Recomendación: agrandar la puerta a ~75cm. **No se tocó** porque modifica la Fase 1 ya aprobada — decisión de Bryan. | Bryan |
| 2 | **Ubicación del módulo 4G** | ¿Cuelga del ESP32 (SIM7600) o vive en el kiosko con su propia SIM? El fix del POST (§4.11) inclina la balanza hacia el ESP32, pero no está cerrado. Marcado en rojo en el 3D (Fase 2). | Hames + Nikolas |
| 3 | **Riesgo de sensado: PET transparente** | La barrera IR podría no cortarse de forma fiable con botella transparente — **a probar en banco, no dar por hecho**. Plan B: paleta mecánica con microswitch (inmune a transparencia, más barata, se desgasta). | Hames (banco de pruebas) |
| 4 | **Antecámara con esclusa vs. desviador a bin de rechazo** | Dos alternativas para "impedir físicamente" materiales no-PET, evaluadas con su costo (motor/servo adicional) pero no implementadas — el piloto v2 valida sin rechazo físico por ahora. | Hames |
| 5 | **Sensor de nivel de llenado** | Idea evaluada (HC-SR04 reubicado ya lo permite), no comprometida como requisito. | Bryan / Hames |
| 6 | **Cierre de sesión: ¿por compuerta o por timeout?** | Pregunta original de `HARDWARE.md`, sigue sin responder — define cuándo dispara el POST el ESP32. | Nikolas |
| 7 | **RTC y memoria de cola offline** | ¿Tiene el ESP32 hora de red confiable? ¿Cuántos depósitos aguanta la cola sin señal? Sin responder desde el documento original. | Nikolas |
| 8 | **PR sin mezclar en el repo privado** | Rama `diseno/visor-3d-fase1` con el visor de Fase 1 y el fix de `HARDWARE.md`, esperando revisión de Bryan. Link en §8. | Bryan |
| 9 | **Paso 3 — render final en color** | Sin iniciar. Necesita el diseño del vinilo de fachada (plano, PNG o SVG) — no el manual de marca completo, ya se usó metal desnudo a propósito en el 3D para no asumir colores. | Bryan |

---

## 6. Cómo esto conecta con el resto del proyecto

- **Ficha técnica del producto** (Notion, tarea de Hames) — depende de que el exterior esté cerrado; el pendiente #1 de §5 es lo único que falta para eso.
- **Estructura de Costos** (Drive → Finanzas → `Estructura_de_Costos_EcoBox_v2.xlsx`) — necesita las medidas finales de cada panel.
- **Brochure y Landing page** — usarán el render del Paso 3.
- **`ecopoint/docs/HARDWARE.md`** y **`01-estrategia/CONTEXTO-TACHO-ECOBOX.md`** — corregidos esta sesión, ver §9.
- Contexto de negocio completo: `../EcoPoint 2026/HANDOFF.md`.

---

## 7. Documentos viejos relacionados (contexto histórico)

- `../02-legado/Eco Point Pitch Deck Kaman 2025.pdf` — pitch del EcoBox v1, solo referencia histórica.
- `../01-estrategia/PRODUCTO.md` — arquitectura de producto completa (3 superficies), vigente en lo funcional.

---

## 8. Entregables de esta sesión — todos los links

### Visores 3D — públicos, para todo el equipo

Repo aparte y público (el repo principal es privado; ver por qué en la memoria `ecobox-visor-publico` del asistente). Se actualizan solos con cada push.

| Qué es | Link |
|---|---|
| **Índice** | https://bryangmz7.github.io/ecobox-visor/ |
| **Fase 1 — Vista exterior** (estructura sin acabado, puertas, exporta GLB/STL) | https://bryangmz7.github.io/ecobox-visor/fase1-exterior.html |
| **Fase 2 — Vista interna** (27 componentes, despiece, cableado, **simulación del flujo de depósito**) | https://bryangmz7.github.io/ecobox-visor/fase2-interior.html |
| Repositorio del visor | https://github.com/Bryangmz7/ecobox-visor |

### Planos 2D — públicos, mismo repo que el 3D

Originalmente publicados como artifacts de Claude; se movieron aquí el 12-ago-2026 porque los artifacts son privados por defecto y romper el acceso del equipo (404 al abrir el link) no vale la comodidad de publicarlos ahí.

| Qué es | Link |
|---|---|
| Esqueleto visual (exterior, wireframe a escala) | https://bryangmz7.github.io/ecobox-visor/planos/esqueleto-visual.html |
| Arquitectura interna (primer bosquejo referencial, previo al 3D) | https://bryangmz7.github.io/ecobox-visor/planos/arquitectura-interna.html |
| Recorrido de la botella + despiece de componentes (con tabla de 14 componentes) | https://bryangmz7.github.io/ecobox-visor/planos/componentes.html |

### Repo privado — pendiente de mezclar

| Qué es | Link |
|---|---|
| Rama `diseno/visor-3d-fase1` (visor Fase 1 + fix de HARDWARE.md) | https://github.com/Bryangmz7/ecopoint/pull/new/diseno/visor-3d-fase1 |

### Este documento

Este handoff también existe como página pública, con tarjetas clicables: https://bryangmz7.github.io/ecobox-visor/handoff.html

---

## 9. Documentos corregidos esta sesión

Los dos tenían una contradicción real sobre quién dispara el POST de depósito — se resolvió a favor del **ESP32**, porque la regla de oro del propio proyecto ("el conteo nace en el sensor y muere en el reporte, ninguna interfaz web lo genera") lo exige: si el kiosko (que corre una web app) posteara, el número pasaría por sus manos antes de la nube.

- **`01-estrategia/CONTEXTO-TACHO-ECOBOX.md`** — §4 y §5, ahora dicen que el ESP32 postea con `dni` opcional recibido del kiosko por serial.
- **`ecopoint/docs/HARDWARE.md`** — nueva sección "Quién dispara el POST", body actualizado con `dni`, ejemplo en C++ corregido para manejar `dni == NULL`.
