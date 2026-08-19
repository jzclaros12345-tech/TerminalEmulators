# Tmux

Esta carpeta contiene la configuración versionada de tmux, independiente del
emulador de terminal. Existe para centralizar sesiones, ventanas, paneles y
atajos sin absorber responsabilidades de la shell o del terminal.

`tmux.conf` es la base de la Fase 3A. Su destino de instalación previsto es
`~/.config/tmux/tmux.conf`; hasta que exista el bootstrap no se enlaza ni se
carga automáticamente. No usa TPM, plugins, scripts, temas, iconos ni ajustes
de color de un terminal específico.

La validación de esta fase está en [validation.md](validation.md).
