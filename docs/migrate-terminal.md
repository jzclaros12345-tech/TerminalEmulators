# Migrar de emulador de terminal

Este documento existe para garantizar que cambiar de emulador sea una operación
local a `terminal/`, no una refactorización del entorno completo.

## Principio

Al migrar entre GNOME Terminal, Alacritty, Kitty, Ghostty, WezTerm o XFCE
Terminal solo cambia su carpeta bajo `terminal/` y la selección de ese
emulador en el sistema. No cambian tmux, shell, Starship, Git ni scripts.

Las instrucciones concretas se añadirán después de crear y probar los
adaptadores de cada terminal.
