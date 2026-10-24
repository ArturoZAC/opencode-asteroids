# AGENTS.md

Clon de Asteroids en canvas HTML5. JS puro, sin dependencias, sin bundler, sin `package.json`, sin tests ni linter. No agregues tooling ni módulos ES: `game.js` se carga con `<script>` clásico y comparte scope global.

## Correr / verificar

No hay build. Verificación = probar en el navegador:

```bash
npx serve .
```

Abrir `http://localhost:3000` (o `index.html` con doble clic). No existe suite de tests; si tocás lógica de colisiones o estados, jugá al menos un nivel y una muerte.

## Estructura

- `index.html` — shell y estilos; define el canvas.
- `game.js` — todo el juego (~420 líneas, un solo archivo).
- `favicon.svg`.

## Gotchas

- **800×600 duplicado**: `const W/H` en `game.js` y los atributos `width`/`height` del `<canvas>` en `index.html`. Cambiá ambos.
- **Estado global**: `ship, bullets, asteroids, particles, score, lives, level, state, deadTimer` se declaran juntos (sección "Estado del juego"). `initGame()` es el único reset completo.
- **Máquina de estados**: `state` ∈ `'playing' | 'dead' | 'gameover'`. `update()` retorna temprano en `dead`/`gameover`; respetá qué se actualiza en cada uno.
- **Entrada**: `keys[code]` para tecla mantenida; `pressed(code)` para acción única y **consume** el flag. Llamalo una sola vez por frame.
- **Tamaños de asteroide invertidos**: `size 3 = grande`, `2 = mediano`, `1 = pequeño`. `RADII`, `SPEEDS` y `POINTS` están indexados desde 1 con un `0` de relleno en el índice 0. `split()` corta en `size 1`.
- **`wrap()` mueve, `dist()` no**: el espacio es toroidal para el movimiento, pero las colisiones no cruzan el borde. Es comportamiento conocido, no un bug a "arreglar" sin pedirlo.
- **Render inmediato**: cada clase dibuja contra el `ctx` global; no devuelve nada. Mantené ese patrón en vez de introducir un sistema de dibujo.
- `dt` se limita a 0.05 s en `loop()`; no uses deltas sin clampear.

## Convenciones

- Código en inglés; comentarios y textos de UI en español (`SCORE`, `NIVEL`, `GAME OVER`).
- El README menciona power-ups y "estrella fugaz": **no están implementados**. No los asumas al leer código ni documentación.
