# EcoBox — visores de diseño

Modelos 3D del EcoBox (EcoPoint) publicados para revisión del equipo.

**Ver:** https://bryangmz7.github.io/ecobox-visor/

## Qué hay aquí

| Archivo | Contenido |
|---|---|
| `index.html` | Índice de visores |
| `fase1-exterior.html` | Vista exterior: estructura en chapa sin acabado, 80 × 70 × 175 cm |
| `fase2-interior.html` | Vista interna: 27 componentes y su cableado, con despiece y simulación del flujo de depósito |

## Qué NO hay aquí

Este repositorio contiene únicamente la geometría del producto físico. La
estrategia, la estructura de costos, el contrato de hardware y el resto de la
documentación viven en el repositorio privado del proyecto.

## Cómo usarlo

Abre el enlace de arriba. No requiere instalación.

Arrastra para girar, rueda para zoom, clic derecho para desplazar.

**Vista exterior**
- **Abrir puertas** — comprueba el despeje de las puertas de mantenimiento
- **Marcar zonas** — superpone las cuatro franjas verticales con sus alturas

**Vista interna**
- **Despiece** — separa los cinco módulos para ver cómo se arma
- **Clic en una pieza** — muestra qué hace y por qué está ahí
- **Aislar** — deja solo la pieza seleccionada
- **Recorrido de la botella** — anima el camino completo, de la boca a la bolsa
- **Reproducir (simulación)** — corre el flujo completo de un depósito: entra, corta
  el haz IR, el sensor de material confirma PET, cae a la bolsa, la compuerta
  cierra, el ESP32 arma el POST y lo envía por 4G. El panel inferior muestra el
  JSON real de cada paso y la latencia aproximada real junto al ritmo lento de
  la demo. **Simular sin señal** fuerza la rama de timeout → cola local →
  reintento con backoff, para ver que el depósito no se pierde.

Ambas exportan **GLB / STL** para abrir el modelo en cualquier CAD.

## Estado

Prototipo estructural. El metal desnudo es intencional: el acabado y el vinilo de
fachada se aplican después sobre esta misma base. Las medidas son las definitivas
hasta que se valide fabricabilidad en el modelado 3D final.
