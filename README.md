# VITAL-MR_Game

**V.I.T.A.L. — Experiencia Dual Arcade y Realidad Mixta (v3)**

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

## Mejoras de soporte VR/MR (v3)

- **Raycasting de controladores WebXR completo:** un `THREE.Raycaster` anclado a la pose
  de cada `XRInputSource` (eje -Z) permite disparar con el gatillo todos los elementos 3D:
  sensores, LEDs de triaje, botones Anular Ruido/Calibrar, alas solares y las tarjetas 3D
  del Q&A conversacional (con resalte por hover).
- **Bucle de triaje sin bloqueos:** el LED físico seleccionado (ratón o gatillo XR) registra
  la decisión, suena una campana de confirmación, el OLED muestra **“TRIAJE GUARDADO”**
  durante 2,5 s con diagnóstico y cuenta regresiva, y la cola avanza sola al siguiente
  paciente (botón 3D/HUD “Siguiente Paciente” para omitir la espera).
- **Audio en VR:** `audioCtx.resume()` explícito al iniciar la sesión y en el primer gatillo,
  más cebado de `speechSynthesis` dentro del gesto de usuario para que la voz sintetizada y
  los pitos se escuchen dentro del visor.
- **Posición ergonómica MR:** la estación se coloca a 1,3 m del usuario
  (`(0, -0.15, -1.3)`, escala 0,42), a la altura del pecho.
- **Etiquetas 3D** flotantes sobre los botones físicos naranja (ANULAR RUIDO) y azul
  (CALIBRAR TEMP); el botón HUD de entrada a MR es un 25% más grande con contorno neón
  pulsante.

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
