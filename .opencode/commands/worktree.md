---
description: Crea un git worktree en .worktrees/ con un nombre derivado del contexto dado.
agent: build
---

El usuario invocó `/worktree` con el siguiente argumento:

$ARGUMENTS

Instrucciones:

1. Analiza el argumento (puede contener espacios) y deriva un nombre corto en kebab-case (minúsculas, sin espacios ni acentos) que represente el contexto.
2. Ejecuta exactamente este comando con la tool bash, sin cambiar de directorio y sin pasos adicionales:
   git worktree add .worktrees/<nombre-derivado>
3. No hagas nada más: no uses `cd`, no corras otros comandos, no edites archivos, no confirmes con el usuario, no hagas commit ni push.
4. Reporta únicamente el resultado del comando (stdout/stderr y código de salida).
5. Si los argumentos son muy largos, simplifícalos a un nombre significativo.