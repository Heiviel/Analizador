# Analizador de Canciones

App standalone de una sola página (`index.html`, sin build, sin dependencias externas, sin servidor) que analiza audio real en el navegador: detecta tonalidad (algoritmo de Krumhansl-Schmuckler sobre croma extraído con una FFT propia) y progresión de acordes por segmentos (template matching por similitud coseno). Incluye reproductor con resaltado sincronizado de acordes, un mini-diapasón horizontal (mismo estilo visual que el proyecto hermano [Teoria-guitarristica](https://github.com/Heiviel/Teoria-guitarristica)) que suena al pulsar un acorde (síntesis Karplus-Strong), y captura de audio opcional desde archivo, micrófono o pestaña del navegador.

El usuario trabaja en este proyecto desde varios equipos (PC, iPad, Android). Reglas de flujo de trabajo:

## Antes de empezar a trabajar
Siempre `git fetch origin` y comparar con `origin/main` antes de tocar nada. Si el local está por detrás, `git pull` (fast-forward) antes de editar — el usuario puede haber hecho cambios desde otro equipo.

## Al terminar
Antes de dar por cerrada una sesión de trabajo, comprobar que todo está subido: `git status` debe estar limpio y `git push` hecho. No dejar cambios sin commitear ni commits sin pushear.

## Durante el trabajo
- Subir los cambios a GitHub en cuanto están probados, sin pedir confirmación cada vez.
- Probar cualquier cambio de interfaz en viewport móvil (375px, tipo Android) antes de darlo por bueno — ya ha habido bugs reales (desbordamiento horizontal, elementos invisibles) que solo aparecían ahí y no en escritorio.
- Las APIs de solo-escritorio (como `getDisplayMedia`, usada en la captura de pestaña) deben detectarse por *feature detection* y ocultar el control en navegadores sin soporte (Android no lo soporta), en vez de mostrar algo que falla siempre.
- Sin frameworks ni librerías externas: todo el motor (FFT, síntesis de audio, digitaciones de guitarra) está escrito a mano en el propio archivo, en la misma línea que el proyecto hermano de teoría musical.

## Estado / próximos pasos conocidos
- Pendiente de confirmar en un navegador real que el sonido de los acordes (síntesis Karplus-Strong) funciona al pulsarlos en la lista — no se pudo verificar en el entorno de pruebas automatizado por una limitación del sandbox de audio, aunque la reproducción de archivos reales sí está confirmada.
- Próximo paso hablado: extracción de tablatura completa (no solo acordes sueltos). Separar instrumentos (voz/batería/bajo) queda descartado por ahora — necesitaría modelos de IA entrenados, no solo DSP.
