# VITAL-MR_Game

**V.I.T.A.L. — Experiencia Dual Arcade y Realidad Mixta (v2)**

Aplicación interactiva 3D / WebXR en un único archivo (`index.html`) para el puesto de
triaje médico sin contacto **V.I.T.A.L.** (*Voice Integrated Triage & Assessment Local*),
ambientada dentro de una carpa médica de campaña.

## Modos de experiencia

- **Modo Arcade 3D Interactivo (predeterminado):** escena 3D con `OrbitControls`,
  jugable con ratón o táctil.
- **Modo Realidad Mixta / Merged Reality:** botón
  *“Entrar a Realidad Mixta / AR”* que inicia una sesión espacial WebXR
  (`immersive-ar` con respaldo `immersive-vr`) con controladores de rayo.

## Entorno

Carpa de campaña modelada con primitivas de Three.js: paredes y techo de lona con
textura procedural, camilla plegable, poste de suero, caja de suministros, cruz médica,
mesa de trabajo, lámpara colgante, polvo en suspensión y un rayo de sol que atraviesa
la entrada siguiendo la órbita solar.

## Mecánicas v2

- **Radar mmWave con proximidad automática:** detecta al paciente que se acerca,
  despierta la estación y entrega distancia + frecuencia respiratoria con onda en el OLED.
- **Sensor IR:** temperatura sin contacto. El calor de la carpa desplaza la línea base;
  el botón **“Calibrar Temp Ambiental”** (también físico, en la cara superior del equipo)
  restablece la medición exacta.
- **Diálogo de voz conversacional (español):** el micrófono inicia 3 preguntas de triaje;
  el jugador selecciona (y escucha) la respuesta del paciente. El análisis acústico
  estima la **disnea** y una confianza. El hardware no tiene sensor de SpO2: no se generan
  lecturas de saturación.
- **Ruido ambiental:** picos periódicos de generador/viento (WebAudio, ruido marrón).
  Con ruido alto el análisis de voz se bloquea hasta activar **“Anular Ruido”**
  (filtro pasa-bajos + atenuación).
- **3 LEDs (Verde / Amarillo / Rojo):** resultado del triaje
  (Estable / Monitoreo / Alerta Crítica) según temperatura + disnea + respuestas.
- **Alas solares duales:** el sol completa su órbita en 105 s. La carga es estrictamente
  angular (`eficiencia = alineación²`) y por panel; sin seguimiento activo la batería
  18650 se agota.
- **Cola de mensajes:** cada mensaje del OLED permanece mínimo 3,5 s y la voz sintetizada
  hace cola sin cortarse ni solaparse.
- **Sistema arcade:** puntuación (triaje + aciertos de diálogo + bono de velocidad),
  cola de 5 pacientes, medidor de batería, alineación solar e informe final de guardia.

Toda la interfaz, diálogos, voces y HUD están en español. El dispositivo y el entorno se
generan de forma procedimental con primitivas básicas de Three.js
(cajas, cilindros, toroides, círculos, conos y grupos).

## Arquitectura

- Archivo único `index.html` con CSS y JavaScript embebidos.
- Three.js r160 + `OrbitControls`, `ARButton` y `VRButton` vía CDN (unpkg, *import map*).
- Sin proceso de construcción ni dependencias locales.

## Despliegue en GitHub Pages

1. Sube `index.html` a la rama del repositorio.
2. En **Settings → Pages**, selecciona la rama y la carpeta raíz (`/`).
3. Abre la URL publicada: `https://<usuario>.github.io/<repositorio>/`.

> La WebXR inmersiva requiere HTTPS (GitHub Pages lo incluye por defecto) y un
> navegador/dispositivo compatible (Chrome Android para AR, visores WebXR para VR).
> El Modo Arcade 3D funciona en cualquier navegador moderno.

## Ejecución local

```bash
python3 -m http.server 8000
# abre http://localhost:8000
```
