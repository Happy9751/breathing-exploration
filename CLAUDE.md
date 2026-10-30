# Breathing Exploration

Una pequeña herramienta web para explorar qué ritmo de respiración te sienta mejor. Proyecto personal de exploración, hecho para la Clase 4 de Automatizaciones avanzadas (Misión IA) y para compartir con su comunidad.

## Qué es
Un solo archivo `index.html`. Cada persona prueba 4 ritmos de respiración guiados (~1 min cada uno), puntúa cómo se siente después de cada uno y elige su favorito. Al final copia su resultado y lo pega en los comentarios del post de Skool.

No es un producto ni una app de salud: es una exploración. No menciones marcas, empresas ni startups en ningún texto.

## Sensación que buscamos
Calma, estar presente, cuidarse a unx mismx durante cinco minutos. Nada que conseguir, nada que optimizar: solo seguir el círculo. Si una decisión de diseño añade ruido, fuera.

## Diseño: minimalista y nórdico
- **Mucho aire.** Una sola cosa protagonista por pantalla. Márgenes generosos, nada pegado a los bordes.
- **Paleta**: fondo blanco roto cálido (tipo arena muy clara), texto gris tinta suave (no negro puro), un único acento apagado (gris azulado de fiordo o verde salvia muy desaturado). Sin degradados llamativos, sin sombras duras, sin neón.
- **Modo oscuro** (`prefers-color-scheme`): azul noche muy apagado, texto hueso. Pensado para hacerlo antes de dormir.
- **Tipografía del sistema**, pesos ligeros/regulares, tamaños grandes y pocos. Texto base de 18px como mínimo. Sin mayúsculas gritonas.
- **Líneas finas** en vez de cajas. Bordes redondeados suaves. Sin iconos ni emojis.
- **Movimiento lento y suave**: fundidos entre pantallas, nada que rebote o parpadee.
- Contraste AA siempre, también en modo oscuro.

## Flujo
1. **Inicio**: una frase que invite, no que explique (EN: "Take five minutes for yourself. Nothing to achieve, just follow the circle."). Debajo, en pequeño: 4 ritmos, unos 5 minutos. Aviso de bienestar. Interruptores discretos de sonido (apagado por defecto) y vibración (solo si el navegador la soporta). Botón "Begin".
2. **Prepárate (3 s)**: círculo en reposo y una frase suave que cambia cada vez ("Let your shoulders drop", "Notice where you are", "Soften your jaw").
3. **Los 4 ritmos, en orden aleatorio y a ciegas**: "Rhythm A / B / C / D". La letra va fija a cada patrón (tabla de abajo); lo aleatorio es el orden. El nombre real no se ve hasta el final.
4. **Después de cada ritmo**: "How calm do you feel right now?" con 5 opciones grandes y etiqueta solo en los extremos (not at all / very calm). Feedback visual suave al tocar y paso automático tras 0,5 s.
5. **Final**: tarjeta limpia con una barra fina por ritmo (su nota) y el favorito destacado; "Which one felt best?" antes de revelar los nombres. Botón grande "Copy my result" con confirmación visible ("Copied - paste it in the post"). Una última frase de cierre amable ("Thank you for taking this moment.").

Formato exacto del resultado copiado (una línea, igual en todos los idiomas):
`breathing exploration | fav: B | A3 B5 C2 D4 | orden: C-A-D-B | idioma: en`

## Guía de respiración (lo más importante)
- El círculo se mueve de forma continua durante TODA la fase: crece durante los segundos de inhalar y encoge durante los de exhalar, con curvas suaves, como unos pulmones. Nunca salta.
- En "Hold", el círculo queda quieto con un halo muy tenue que late despacio, para que se note que el tiempo pasa.
- La palabra de la fase es lo grande; la cuenta atrás va pequeña y secundaria. Las palabras cambian con fundido.
- Un anillo fino de progreso alrededor del círculo (sin barra aparte).
- Cambio de tono muy sutil entre fases, siempre dentro de la paleta.
- Sonido opcional (Web Audio): un tono suave y grave al cambiar de fase, para poder hacerlo con los ojos cerrados. Vibración opcional: un pulso corto al cambiar de fase.
- Wake lock para que la pantalla no se apague mientras dura un ritmo (si el navegador no lo soporta, no pasa nada).
- Botón "Skip" discreto.

## Los 4 ritmos (segundos)
| Letra | Inhala | Mantén | Exhala | Mantén |
|---|---|---|---|---|
| A | 5 | 0 | 5 | 0 |
| B | 4 | 0 | 6 | 0 |
| C | 4 | 4 | 4 | 4 |
| D | 4 | 7 | 8 | 0 |

- Las fases de 0 s se saltan.
- Ciclos completos: `ciclos = Math.round(DURACION_OBJETIVO / segundos_del_ciclo)`, con `DURACION_OBJETIVO = 60` arriba del script (A 6, B 6, C 4, D 3).
- Patrones en un array fácil de editar.

## Idiomas (EN / ES / DA / PL)
- Inglés por defecto, siempre. Selector discreto arriba en todas las pantallas: `EN · ES · DA · PL`. Cambiar de idioma no reinicia el test.
- Todos los textos en un único objeto `TEXTOS`; `lang` del `<html>` según el idioma.
- En español: x inclusiva (tranquilx) y sin signos de apertura (¿ ¡).
- Si dudas de una traducción, márcala con `// REVISAR DA` o `// REVISAR PL`.

| Clave | EN | ES | DA | PL |
|---|---|---|---|---|
| Fases | Breathe in / Hold / Breathe out | Inhala / Mantén / Exhala | Ånd ind / Hold / Ånd ud | Wdech / Zatrzymaj / Wydech |
| A | Coherent breathing | Respiración coherente | Kohærent vejrtrækning | Oddychanie koherentne |
| B | Long exhale | Exhalación larga | Lang udånding | Długi wydech |
| C | Box breathing | Respiración en caja | Boksvejrtrækning | Oddychanie kwadratowe |
| D | 4-7-8 | 4-7-8 | 4-7-8 | 4-7-8 |

Aviso de bienestar (inicio, en pequeño):
- EN: "An informal wellbeing exploration, not medical advice. If you feel dizzy or uncomfortable, stop and breathe normally."
- ES: "Una exploración informal de bienestar, no un consejo médico. Si te mareas o te notas incómodx, para y respira normal."
- DA: "En uformel udforskning af velvære, ikke medicinsk rådgivning. Hvis du bliver svimmel eller føler dig utilpas, så stop og træk vejret normalt."
- PL: "Nieformalna eksploracja samopoczucia, a nie porada medyczna. Jeśli poczujesz zawroty głowy lub dyskomfort, przerwij i oddychaj normalnie."

## Reglas técnicas
- Un solo `index.html` con HTML, CSS y JS. Sin frameworks, sin librerías ni fuentes externas, sin backend, sin build.
- No guardar ni enviar nada: sin cookies, analytics, formularios ni localStorage.
- Mobile-first, usable con una mano, sin scroll horizontal a 375 px.
- Copiar con `navigator.clipboard.writeText`; si falla, mostrar el texto seleccionado para copiar a mano.
- `prefers-reduced-motion`: sin escala del círculo, solo palabra, cuenta atrás y anillo.
- `aria-live` para anunciar las fases a lectores de pantalla.
- Sin claims de eficacia: solo el nombre y cómo se hace cada ritmo.

## Cómo trabajar con Javier
- Antes de tocar archivos, dile en pocas frases qué vas a hacer.
- Cuando acabes, cuéntale las decisiones de diseño que tomaste y por qué.
- Si algo no se puede, dilo claro y no lo simules.
- Explica cada término técnico en una línea la primera vez que salga.
