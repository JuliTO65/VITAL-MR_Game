# VITAL-MR_Game

**V.I.T.A.L. — Experiencia Dual Arcade y Realidad Mixta**

Aplicación interactiva 3D / WebXR en un único archivo (`index.html`) para el puesto de
triaje médico sin contacto **V.I.T.A.L.** (*Voice Integrated Triage & Assessment Local*).

## Modos de experiencia

- **Modo Arcade 3D Interactivo (predeterminado):** escena 3D con `OrbitControls`,
  jugable con ratón o táctil.
- **Modo Realidad Mixta / Merged Reality:** botón
  *“Entrar a Realidad Mixta / AR”* que inicia una sesión espacial WebXR
  (`immersive-ar` con respaldo `immersive-vr`) con controladores de rayo.

## Mecánicas

- **Radar mmWave:** distancia y frecuencia respiratoria animadas en el OLED.
- **Sensor IR:** lectura de temperatura corporal en tiempo real.
- **Micrófono MEMS / altavoz:** análisis de voz, *prompts* hablados en español
  (Web Speech API) y pitos WebAudio, con texto en el OLED.
- **3 LEDs (Verde / Amarillo / Rojo):** estado del triaje
  (Estable / Monitoreo / Alerta Crítica).
- **Alas solares duales:** arrastra y gira los paneles para alinearlos con el sol
  virtual en movimiento y recargar la batería 18650.
- **Sistema arcade:** puntuación, cola de 5 pacientes, medidor de batería,
  alineación solar e informe final de misión.

Toda la interfaz, diálogos, voces y HUD están en español. El dispositivo V.I.T.A.L.
se genera de forma procedimental con primitivas básicas de Three.js
(cajas, cilindros, toroides, círculos y grupos).

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
