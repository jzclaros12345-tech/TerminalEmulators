# Arquitectura

Este documento existe para definir el diseño objetivo del entorno. Es la
referencia arquitectónica canónica para las decisiones de implementación; los
documentos históricos de la raíz se conservan como antecedentes, no como una
segunda especificación activa.

## Principios

- Simplicidad antes que compatibilidad con configuraciones heredadas.
- Una responsabilidad y un propietario por componente y ajuste.
- Las dependencias apuntan hacia abajo: terminal -> tmux -> shell -> Starship
  y aplicaciones. Ninguna capa inferior depende de una superior.
- Cambiar de emulador no cambia tmux, shell, Starship, Git ni scripts.
- Nada se configura dos veces.
- Los secretos nunca se versionan.
- Cada archivo explica por qué existe, además de qué hace.

## Capas y propiedad

| Capa | Propietario | Responsabilidad |
| --- | --- | --- |
| Terminal | `terminal/<emulador>/` | Renderizado, GPU, fuente, transparencia, ventana y clipboard propio |
| Multiplexor | `tmux/` | Sesiones, ventanas, paneles, atajos, historial y persistencia futura |
| Shell | `shell/` | PATH, variables, aliases, funciones y completion |
| Prompt | `starship/` | Solo el prompt |
| Versionado | `git/` | Solo Git, sin secretos |
| Tipografía | `fonts/` | Inventario e instalación de fuentes |
| Automatización | `scripts/` y `bootstrap/` | Acciones explícitas, repetibles y documentadas |

La carpeta `terminal/` es la propietaria de la selección y configuración de
fuente de cada emulador. `fonts/` solo inventaría y facilita instalar los
archivos de fuente: no contiene decisiones visuales de tmux ni de la shell.

## Reemplazo de terminales

Cada subcarpeta de `terminal/` es un adaptador independiente. Para sustituir
Alacritty por Ghostty solo se instala, selecciona o elimina el adaptador del
terminal. Las demás capas permanecen intactas.

## Legacy

`legacy/` conserva únicamente referencias históricas que se copien de forma
explícita. El árbol nuevo no puede cargar, enlazar, incluir ni ejecutar nada de
esa carpeta. No es una segunda fuente de configuración ni una capa de
compatibilidad.

## Puntos de carga previstos

- tmux leerá exclusivamente `tmux/tmux.conf` cuando se instale.
- Zsh cargará `shell/zshrc`; Bash cargará `shell/bashrc` cuando se instale.
- Cada shell inicializará Starship una vez para su intérprete y ambos usarán
  `starship/starship.toml`.
- Ningún terminal inicializará tmux, la shell o Starship automáticamente como
  parte de su archivo de configuración.
