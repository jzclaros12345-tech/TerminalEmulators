# Validación de tmux — Fase 3A

Este documento existe para dejar verificable qué garantiza la base mínima antes
de añadir capacidad. Las pruebas automatizadas usan un servidor temporal y no
leen ni modifican `~/.tmux.conf`.

## Checklist de configuración

- [x] Inspección: `Ctrl+a` es el único prefijo declarado y `Ctrl+b` se
  desasigna.
- [x] Inspección: `Ctrl+a |` y `Ctrl+a -` declaran las dos divisiones.
- [x] Inspección: `Ctrl+a h`, `j`, `k` y `l` declaran la navegación contigua.
- [x] Inspección: `Ctrl+a r` recarga el único destino previsto de instalación.
- [x] Inspección: el ratón y el historial de 50 000 líneas están declarados.
- [x] Inspección: no se reemplazan los bindings predeterminados para crear o
  cambiar ventanas.
- [x] Inspección: no declara plugins, scripts, TPM, temas, iconos, truecolor
  ni dependencias externas.
- [x] Inspección: no contiene una opción ligada a GNOME Terminal, Alacritty,
  Ghostty, Kitty, WezTerm o XFCE Terminal.

## Checklist de ejecución pendiente

Estas comprobaciones requieren un cliente tmux real. El entorno de automatización
no permite crear ni conectar sockets Unix de tmux, incluso en un directorio
temporal, por lo que sería incorrecto marcarlas como superadas.

- [ ] `Ctrl+a` funciona en una sesión interactiva.
- [ ] Dividir paneles y navegar entre ellos funciona.
- [ ] Recargar funciona desde `Ctrl+a r` después de instalar el archivo en
  `~/.config/tmux/tmux.conf`.
- [ ] Abrir una ventana nueva y cambiar de ventana con los bindings
  predeterminados funciona.
- [ ] La copia y pegado mediante el buffer interno de tmux funciona.
- [ ] tmux 3.4 carga el archivo sin warnings ni errores.

## Copia y pegado

- [x] Inspección: la configuración no altera los bindings predeterminados del
  buffer interno de tmux (`Ctrl+a [`, `Enter`, `Ctrl+a ]`).
- [ ] La integración con el portapapeles del sistema se validará por emulador
  en la fase de terminales. No se fuerza ahora con `xclip`, OSC 52 ni plugins,
  porque esas soluciones son dependientes del entorno y violarían el alcance de
  esta fase.

El portapapeles del sistema no bloquea la Fase 3A: corresponde a cada adaptador
de terminal. La lista de ejecución sí bloquea el cierre de la fase hasta que se
pruebe en una sesión tmux real.
