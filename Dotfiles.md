# Dotfiles

Repositorio personal de configuración para mi entorno de desarrollo en Linux.

Este proyecto tiene dos objetivos principales:

1. Mantener todas mis configuraciones bajo control de versiones.
2. Documentar cada decisión para poder migrar fácilmente entre distribuciones, terminales y equipos.

---

# Filosofía del proyecto

No quiero depender de recordar cómo configuré mi sistema.

Cada archivo de configuración debe estar:

- Versionado con Git.
- Documentado.
- Explicado.
- Fácil de restaurar.
- Independiente del emulador de terminal.

Siempre que sea posible, las configuraciones deberán ser portables entre:

- Linux Mint
- Ubuntu
- Debian
- Arch Linux

y entre distintos emuladores como:

- Alacritty
- WezTerm
- Kitty
- Ghostty
- Xfce Terminal

---

# Objetivos

Este repositorio busca construir un entorno:

- limpio
- rápido
- reproducible
- portable
- bien documentado

No se copiarán configuraciones de Internet sin entenderlas.

Cada línea importante deberá tener una explicación.

---

# Principios

## 1. Primero entender, luego configurar

Nunca agregar una opción sin saber exactamente qué hace.

---

## 2. Cambios pequeños

Cada cambio debe poder probarse de manera aislada.

Evitar modificar muchas cosas al mismo tiempo.

---

## 3. Sin duplicados

No debe existir la misma configuración en varios lugares.

Si algo se configura en tmux, no debe volver a configurarse innecesariamente en el terminal.

---

## 4. Documentación antes que memoria

Todo cambio importante debe quedar documentado.

No confiar en recordar por qué se hizo algo.

---

## 5. Portabilidad

Cambiar de terminal o distribución no debería requerir rehacer toda la configuración.

---

# Organización

```
dotfiles/

├── README.md

├── audit/
│   ├── terminal-audit.md
│   └── screenshots/

├── docs/
│   ├── decisions.md
│   ├── migration.md
│   ├── troubleshooting.md
│   ├── shortcuts.md
│   └── roadmap.md

├── tmux/
│   ├── tmux.conf
│   ├── keybindings.md
│   ├── plugins.md
│   ├── themes/
│   └── scripts/

├── starship/
│   └── starship.toml

├── shell/
│   ├── zshrc
│   ├── bashrc
│   ├── aliases.sh
│   ├── exports.sh
│   └── functions.sh

├── terminals/
│   ├── xfce4/
│   ├── alacritty/
│   ├── wezterm/
│   ├── kitty/
│   └── ghostty/

├── fonts/

└── scripts/
```

---

# Roadmap

## Fase 1

Auditoría completa del sistema.

Estado actual.

---

## Fase 2

Limpieza de tmux.

Crear una configuración mínima y completamente entendida.

---

## Fase 3

Starship.

Crear un prompt propio.

---

## Fase 4

Shell.

Organizar aliases, variables y funciones.

---

## Fase 5

Alacritty.

Crear una configuración moderna desde cero.

---

## Fase 6

Comparar otros emuladores.

- WezTerm
- Kitty
- Ghostty

---

## Fase 7

Automatizar la instalación.

Scripts para reconstruir el entorno desde cero.

---

# Reglas

Antes de modificar cualquier configuración:

1. Hacer copia de seguridad.
2. Documentar el motivo.
3. Probar el cambio.
4. Confirmar que funciona.
5. Recién entonces hacer commit.

---

# Convención de commits

docs:
Cambios únicamente en documentación.

tmux:
Configuración de tmux.

starship:
Configuración del prompt.

shell:
Configuración de zsh o bash.

terminal:
Configuraciones del emulador.

fonts:
Fuentes.

scripts:
Automatizaciones.

---

# Objetivo final

Poder instalar un Linux nuevo y reconstruir todo el entorno de desarrollo únicamente clonando este repositorio y siguiendo la documentación.

El repositorio debe servir también como referencia técnica para entender cada decisión tomada durante la evolución del entorno.