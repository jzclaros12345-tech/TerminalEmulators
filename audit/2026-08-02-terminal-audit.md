# Auditoría de entorno de terminal

**Fecha:** 2026-08-02  
**Alcance:** inventario de solo lectura de shell, tmux, Starship, emuladores, fuentes, portapapeles, color y variables de entorno.  
**Cambios realizados:** ninguno en la configuración del sistema. Este archivo es el único artefacto creado para la auditoría.

> Nota de seguridad: se detectó una credencial de API escrita en texto plano dentro de `~/.bashrc`. Su valor se ha omitido deliberadamente de este informe.

## 1. Sistema

| Elemento | Valor |
|---|---|
| Distribución | Linux Mint 22.3 (Zena), base Ubuntu Noble / Debian |
| Kernel | Linux 7.0.0-28-generic x86_64 |
| Escritorio / sesión | XFCE, X11 (`DISPLAY=:0.0`, `XDG_SESSION_TYPE=x11`) |
| Locale | `es_BO.UTF-8` |
| Shell de la cuenta | `/usr/bin/zsh` |

Variables de sesión relevantes observadas:

```text
SHELL=/usr/bin/zsh
TERM=tmux-256color                 # dentro de tmux
COLORTERM=truecolor
TERM_PROGRAM=tmux
TMUX=/tmp/tmux-1000/default,...
DISPLAY=:0.0
XDG_CURRENT_DESKTOP=XFCE
DESKTOP_SESSION=xfce
XDG_SESSION_TYPE=x11
EDITOR=nano
PAGER=cat
```

El proceso padre de tmux conserva `TERM=xterm-256color` y `VTE_VERSION=7600`; por tanto, el emulador real comunica xterm-256color al iniciar tmux.

## 2. Shell

### Shell activo y archivos de inicio

- Shell de inicio de sesión de la cuenta: **zsh 5.9**.
- Archivo zsh existente: `~/.zshrc` (1,268 bytes; 2026-07-30).
- No existen: `~/.zshenv`, `~/.zprofile`, `~/.zlogin` ni `~/.config/zsh/`.
- Bash 5.2.21 permanece instalado y tiene `~/.bashrc` (4,446 bytes) y `~/.profile` (909 bytes).
- No existen: `~/.bash_profile`, `~/.bash_login` ni `~/.bash_aliases`.

### zsh: configuración declarada

`~/.zshrc` configura:

- `EDITOR=nano`.
- Prompt mediante `eval "$(starship init zsh)"`.
- Navegación mediante `eval "$(zoxide init zsh)"`.
- FZF desde los ejemplos del paquete: `/usr/share/doc/fzf/examples/key-bindings.zsh` y `completion.zsh`.
- Historial: `HISTSIZE=100000`, `SAVEHIST=100000`, `HIST_IGNORE_DUPS` y `SHARE_HISTORY`.
- `compinit` para completado.
- NVM desde `~/.nvm/nvm.sh`.

Aliases declarados en zsh:

```text
ll='eza -lah --icons'       ls='eza'          grep='rg'
..='cd ..'                  ...='cd ../..'    gs='git status'
ga='git add'                gc='git commit'   gp='git push'
cls='clear'                 bcat='bat'
```

No se encontraron funciones definidas de forma estática en `~/.zshrc`, `~/.bashrc` o `~/.profile`. No se cargaron los dotfiles para evitar efectos secundarios; este inventario refleja sus declaraciones estáticas.

### Bash: configuración declarada

`~/.bashrc` es mayoritariamente la plantilla de Linux Mint/Debian: historial de 1,000/2,000 entradas, `histappend`, `checkwinsize`, `lesspipe`, prompt Bash estándar y `bash-completion`. Añade además:

- `~/.cargo/env`.
- NVM y su completado.
- Rutas para `.local/bin`, `.npm-global/bin` y `.opencode/bin`.
- Alias estándar de Bash (`ls`, `grep`, `ll`, `la`, `l`, `alert`) y un alias `aiderstart` ligado a una ruta de proyecto concreta.
- Una variable de secreto de API en texto plano (valor omitido).

`~/.profile` carga `~/.bashrc` solo si el intérprete es Bash, incorpora `~/bin`, `~/.local/bin`, `~/.cargo/env` y vuelve a anteponer `.local/bin`.

### PATH observado en la sesión auditada

El `PATH` contiene, en este orden relevante: un shim interno de Codex, Node/NVM v22.22.3, `~/.local/bin`, `~/.cargo/bin`, rutas del sistema y `/snap/bin`. Se observan entradas repetidas de `~/.local/bin` y del shim de Codex. Las rutas declaradas solo en Bash para `~/.npm-global/bin` y `~/.opencode/bin` no aparecen en la sesión zsh auditada.

### Frameworks y plugins de shell

No se detectaron Oh My Zsh, Zinit, Antidote, Zim, Prezto ni otro framework zsh en sus ubicaciones habituales. Los complementos efectivos declarados son Starship, zoxide, fzf, `compinit` y NVM.

Herramientas detectadas:

| Herramienta | Versión / estado |
|---|---|
| fzf | 0.44.1 (Debian) |
| zoxide | 0.9.3 |
| eza | instalado |
| cargo / rustc | 1.94.1 |
| Node / npm (NVM) | v22.22.3 / 10.9.8 |
| direnv, atuin, bat, fd, btop, htop, nvim, vim | no detectados en `PATH` durante la auditoría |

## 3. Starship

- Binario: `/usr/local/bin/starship`.
- Versión: **1.26.0**.
- Inicialización: presente en `~/.zshrc`.
- `STARSHIP_CONFIG`: no definido.
- Archivo estándar `~/.config/starship.toml`: **no existe**.
- No se detectaron módulos ni formatos personalizados por archivo de usuario.

Por no haber archivo de configuración ni variable que apunte a otro, Starship usa su configuración predeterminada compilada (`format = "$all"`, sin `right_format`). La configuración calculada enumera los módulos integrados disponibles; eso no significa que todos se muestren: Starship muestra cada módulo solo cuando se cumple su condición contextual. No hay módulos personalizados definidos por el usuario.

## 4. tmux

### Versión, archivo y servidor

- Versión: **tmux 3.4**.
- Archivo: `~/.tmux.conf` (2,248 bytes; 2026-07-30).
- Servidor activo: socket `/tmp/tmux-1000/default`.
- Sesiones detectadas: `0` (3 ventanas), `3`, `4`, `5` (adjunta) y `trabajo_duro`.
- Shell predeterminado efectivo: `/usr/bin/zsh`.

### Opciones globales y de ventana efectivas

| Opción | Valor |
|---|---|
| Prefix | `C-a` (`C-b` desasignado) |
| `default-terminal` | `tmux-256color` |
| `terminal-overrides` | `*:Tc` |
| `terminal-features` | xterm clipboard, color, cursor-style, focus y title; screen/rxvt con title/ignorefkeys |
| `history-limit` | 100000 |
| `mouse` | on |
| `base-index` / `pane-base-index` | 1 / 1 |
| `escape-time` | 0 |
| `allow-rename` | off |
| `mode-keys` | emacs |
| `status-interval` | 5 segundos |

### Bindings propios

- `C-a C-a`: envía el prefijo.
- `C-a r`: recarga `~/.tmux.conf` y muestra un mensaje.
- `C-a |` y `C-a -`: divisiones horizontal y vertical; se desasignan `%` y `"`.
- `Alt` + flechas: navega entre paneles sin prefijo.
- `C-a C-r` / `C-a C-s`: restaurar / guardar tmux-resurrect.
- `C-a I`, `U` y `M-u`: instalar, actualizar y limpiar plugins con TPM.

Los atajos de copia siguen en modo **emacs**. No hay binding configurado por el usuario que ejecute `xclip`, `xsel`, `wl-copy`, OSC 52 ni un plugin de copia.

### Plugins

| Plugin | Directorio | Revisión local |
|---|---|---|
| TPM | `~/.tmux/plugins/tpm` | `e261deb` (2026-05-17) |
| tmux-resurrect | `~/.tmux/plugins/tmux-resurrect` | `cff343c` (2023-03-06) |
| tmux-continuum | `~/.tmux/plugins/tmux-continuum` | `0698e8f` (2024-01-20) |

TPM está instalado y se ejecuta desde `~/.tmux/plugins/tpm/tpm`. Resurrect está instalado y proporciona las rutas activas de save/restore. Continuum está activo con restauración automática y guardado cada 15 minutos (`@continuum-restore=on`, `@continuum-save-interval=15`).

### Ratón, historial, color y barra de estado

- Ratón: activado globalmente.
- Historial: 100,000 líneas por panel.
- TrueColor: solicitado con `*:Tc`; la sesión además anuncia `COLORTERM=truecolor`.
- Tema: Catppuccin Mocha codificado directamente en `~/.tmux.conf` con bordes `#45475a` / `#cba6f7`.
- Barra: izquierda con icono Nerd Font y nombre de sesión; derecha con hostname, reloj y la llamada de guardado de continuum.
- El carácter/icono `󰭹` requiere una fuente con glifos Nerd Font para verse correctamente.

### Layouts observados

El servidor contiene ventanas con panel único, dos paneles verticales y varios apilamientos horizontales. La sesión `trabajo_duro` tiene una ventana de 9 paneles. Son layouts de estado actual, no una plantilla persistente declarada en el archivo.

### Posibles configuraciones obsoletas

No se halló una directiva inequívocamente eliminada para tmux 3.4. `terminal-overrides=*:Tc` continúa siendo entendido, aunque es un mecanismo amplio y dependiente del emulador; tmux 3.4 ya ofrece `terminal-features` para describir capacidades por familia de terminal. Debe revisarse durante una migración, no corregirse automáticamente.

## 5. Terminal Emulator

### Emulador actualmente usado

El árbol de procesos identifica el emulador actual como **xfce4-terminal**:

```text
xfce4-terminal → zsh → tmux client
```

Su shell padre tiene `TERM=xterm-256color` y `VTE_VERSION=7600`. Dentro de tmux, `TERM` cambia correctamente a `tmux-256color`.

Configuración persistente de XFCE encontrada en `~/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-terminal.xml`:

- Fondo transparente, oscuridad 1.0.
- Fondo negro y paleta clásica de 16 colores.
- Cursor configurado explícitamente.
- Fuente: `Monospace 10`.
- Campana desactivada; menú y bordes por defecto activados.
- Título en modo prepend.

No existe `~/.config/xfce4/terminal/terminalrc`.

### Alacritty

- Instalado: **Alacritty 0.13.2** (`/usr/bin/alacritty`).
- Archivo: `~/.config/alacritty/alacritty.toml`.
- `TERM=xterm-256color` para ventanas Alacritty.
- Padding 10×10, padding dinámico, opacidad 0.96 y arranque en ventana.
- Fuente: `JetBrainsMono Nerd Font`, tamaño 11.5.
- Historial: 100,000 líneas.
- Selección copiada al portapapeles y cursor Beam con parpadeo.

### Otros emuladores

| Emulador | Binario | Configuración encontrada |
|---|---|---|
| WezTerm | no instalado | no |
| Kitty | no instalado | no |
| Ghostty | no instalado | no |
| Foot | no instalado | no |
| Konsole | no instalado | no |
| GNOME Terminal | no instalado | no |
| Xfce Terminal | instalado y activo | XML de xfconf presente |

## 6. Fonts

Familias relevantes detectadas:

| Familia | Disponibilidad | Uso observado |
|---|---|---|
| JetBrainsMono Nerd Font | instalada en `~/.local/share/fonts` (regular, bold, italic y variantes Mono/NL/Propo) | configurada por Alacritty; apta para iconos tmux |
| Fira Code | instalada a nivel de sistema | no configurada explícitamente |
| DejaVu Sans Mono | instalada a nivel de sistema | posible sustituto de `Monospace` |
| Ubuntu Mono | instalada a nivel de sistema | posible sustituto de `Monospace` |
| JetBrains Mono (familia sin Nerd) | no coincide; Fontconfig cae a Noto Sans | no usada |
| Cascadia | no instalada | no usada |
| Meslo | no instalada | no usada |
| Symbols Nerd Font (familia separada) | no instalada | no usada; JetBrainsMono Nerd Font contiene los glifos requeridos |

El archivo de XFCE pide el alias genérico `Monospace 10`, no JetBrainsMono Nerd Font. Por eso la fuente visible en el emulador activo puede diferir de la prevista para Alacritty y de los iconos de tmux.

## 7. Clipboard

| Herramienta | Estado |
|---|---|
| `xclip` | instalada en `/usr/bin/xclip` |
| `xsel` | no instalada |
| `wl-copy` / `wl-paste` | no instaladas |
| `pbcopy` | no instalada |
| tmux-yank / osc52-copy | no detectados |

La sesión es X11, por lo que `xclip` es la única utilidad de portapapeles encontrada. Sin embargo, tmux **no está configurado para invocarla**: no hay `copy-pipe`, binding ni plugin de copia personalizado. La configuración de Alacritty sí activa `selection.save_to_clipboard=true`, pero el emulador activo es Xfce Terminal. tmux declara capacidad de portapapeles para xterm mediante `terminal-features`, aunque la ruta efectiva de copia no está configurada explícitamente en el dotfile.

## 8. Color

- `TERM` del emulador/padre: `xterm-256color`.
- `TERM` dentro de tmux: `tmux-256color`.
- `COLORTERM=truecolor` está presente dentro de la sesión.
- Las entradas terminfo de `xterm-256color`, `tmux-256color` y `screen-256color` anuncian 256 colores (no declaran por sí solas 24-bit).
- La configuración de tmux añade `*:Tc`, que comunica soporte TrueColor/24-bit a los programas internos.
- La configuración activa de Xfce Terminal incluye una paleta explícita de 16 colores; la de Alacritty no define esquema, así que usaría su esquema predeterminado.

## 9. Variables de entorno relevantes

| Variable | Valor / significado |
|---|---|
| `SHELL` | `/usr/bin/zsh` |
| `EDITOR` | `nano` |
| `PAGER` | `cat` |
| `TERM` | `tmux-256color` dentro de tmux; `xterm-256color` en el padre |
| `COLORTERM` | `truecolor` |
| `TERM_PROGRAM` | `tmux` dentro de la sesión |
| `TMUX` | socket, PID e índice de cliente del servidor tmux |
| `DISPLAY` | `:0.0` (X11) |
| `SSH_AUTH_SOCK` | definido (agente SSH local; ruta omitida) |
| `LANG` | `es_BO.UTF-8` |
| `PATH` | incluye NVM, `.local/bin`, Cargo, sistema y shim de Codex; hay duplicados |
| `NVM_DIR` | declarado en los archivos de shell; NVM está instalado |
| `STARSHIP_CONFIG` | no definido |

No se muestran variables de credenciales, tokens, cookies u otros valores sensibles.

## 10. Árbol de configuración

```text
~/
├── .tmux.conf                                      [existe]
├── .tmux/
│   └── plugins/                                    [existe: TPM, resurrect, continuum]
├── .zshrc                                          [existe]
├── .zshenv                                         [no existe]
├── .zprofile                                       [no existe]
├── .zlogin                                         [no existe]
├── .bashrc                                         [existe]
├── .bash_profile                                   [no existe]
├── .bash_login                                     [no existe]
├── .bash_aliases                                   [no existe]
├── .profile                                        [existe]
├── .config/
│   ├── starship.toml                               [no existe]
│   ├── wezterm/                                    [no existe]
│   ├── alacritty/
│   │   └── alacritty.toml                          [existe]
│   ├── kitty/                                      [no existe]
│   ├── ghostty/                                    [no existe]
│   ├── foot/                                       [no existe]
│   ├── konsole/                                    [no existe]
│   ├── gnome-terminal/                             [no existe]
│   ├── tmux/                                       [no existe]
│   └── xfce4/xfconf/xfce-perchannel-xml/
│       └── xfce4-terminal.xml                      [existe]
└── .local/share/fonts/                             [existe: JetBrainsMono Nerd Font]
```

## 11. Problemas detectados

1. **Secreto expuesto en `~/.bashrc` (crítico).** Hay una credencial de API declarada directamente en el archivo. No se reproduce su valor. Esto expone el secreto a copias de dotfiles, historial de Git y cualquier proceso que cargue Bash.
2. **Bloque TPM/Resurrect/Continuum duplicado.** El tramo de plugins, sus tres declaraciones, las opciones de continuum y `run '~/.tmux/plugins/tpm/tpm'` aparece dos veces consecutivas en `~/.tmux.conf`. Puede ejecutar TPM dos veces y dificulta saber qué configuración prevalece.
3. **Carga de NVM duplicada en zsh.** `~/.zshrc` declara `NVM_DIR` y carga `nvm.sh` dos veces. El primer bloque también invoca `bash_completion` usando la ruta de `nvm.sh`, y el segundo omite el completado.
4. **PATH duplicado.** `.local/bin` se antepone varias veces en `.bashrc` y `.profile`; el PATH de la sesión contiene entradas repetidas. Esto aumenta ambigüedad y tiempo de resolución sin aportar una ruta nueva.
5. **Configuración dividida entre dos emuladores.** El emulador activo (Xfce Terminal) usa `Monospace 10`, transparencia y paleta de 16 colores; Alacritty define JetBrainsMono Nerd Font, otra opacidad y 100,000 líneas de historial. Migrar sin reconciliar estas diferencias puede cambiar iconos, colores, clipboard y scrollback.
6. **Fuente de iconos no garantizada en el emulador actual.** Tmux usa iconos Nerd Font, pero Xfce Terminal solicita `Monospace`, no la familia JetBrainsMono Nerd Font instalada. Puede haber sustitución de glifos o iconos ausentes.
7. **Portapapeles tmux no definido explícitamente.** `xclip` existe en X11, pero tmux no tiene una ruta de copia configurada. La copia puede depender de las capacidades del emulador y comportarse diferente al migrar a Wayland, WezTerm o Kitty.
8. **Color TrueColor forzado globalmente.** `terminal-overrides=*:Tc` afecta a todos los clientes, incluso futuros emuladores con capacidades distintas. Es una dependencia de terminal que requiere validación al migrar.
9. **Alias no equivalentes entre zsh y Bash.** Bash sigue usando `ls`/`grep` estándar con color, mientras zsh los cambia a `eza`/`rg`. Un terminal nuevo no lo causa, pero iniciar Bash cambia el comportamiento operativo.
10. **Alias con ruta de proyecto específica.** `aiderstart` contiene una ubicación concreta de otro proyecto. No es portátil al copiar dotfiles a otra máquina ni al cambiar esa ruta.
11. **Starship sin archivo portable de configuración.** El prompt funciona por defaults; no existe un `starship.toml` que permita reproducir exactamente su aspecto y módulos en otra máquina.
12. **Archivo comprimido de fuente conservado junto a fuentes instaladas.** `~/.local/share/fonts` contiene `JetBrainsMono.zip` además de los TTF. No afecta directamente a Fontconfig, pero es un artefacto de instalación que conviene clasificar al empaquetar dotfiles.

## 12. Recomendaciones para revisión posterior

No se aplicó ninguna corrección. Antes de migrar, conviene revisar manualmente lo siguiente:

- Rotar y retirar la credencial expuesta de los archivos de inicio; conservar secretos fuera de un repositorio de dotfiles.
- Consolidar bloques duplicados de tmux, NVM y `PATH` después de confirmar qué comportamiento se desea preservar.
- Definir una fuente monoespaciada Nerd Font única para cada emulador, o documentar intencionalmente la diferencia entre XFCE Terminal y Alacritty.
- Decidir una estrategia de portapapeles independiente del emulador y probarla en X11 y, si aplica, Wayland.
- Validar `terminal-overrides` y `terminal-features` de tmux por emulador en vez de asumir que una regla global es válida para todos.
- Exportar explícitamente un `starship.toml` si se desea un prompt reproducible.
- Separar configuración portable (shell, Starship, tmux, fuente) de preferencias propias de cada emulador (opacidad, padding, paleta, shortcuts).
- Revisar aliases dependientes de rutas locales y documentar cuáles deben existir en todas las máquinas.

