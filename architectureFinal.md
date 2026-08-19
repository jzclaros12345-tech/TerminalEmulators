• De acuerdo. Incorporo esas reglas como requisitos de arquitectura para la Fase 2. No he creado ni migrado archivos todavía.

  Propongo esta estructura final:

  dotfiles/
  ├── README.md
  ├── LICENSE
  ├── bootstrap/
  │   └── install.sh
  ├── docs/
  │   ├── architecture.md
  │   ├── decisions.md
  │   ├── installation.md
  │   ├── keybindings.md
  │   ├── migrate-terminal.md
  │   ├── roadmap.md
  │   └── troubleshooting.md
  ├── audit/
  │   ├── 2026-08-02-terminal-audit.md
  │   └── phase-1-rebuild-audit.md
  ├── legacy/
  │   ├── README.md
  │   ├── shell/
  │   ├── tmux/
  │   └── terminal/
  ├── tmux/
  │   ├── tmux.conf
  │   └── README.md
  ├── shell/
  │   ├── zshrc
  │   ├── bashrc
  │   ├── aliases.sh
  │   ├── exports.sh
  │   ├── functions.sh
  │   ├── completion.sh
  │   └── README.md
  ├── starship/
  │   ├── starship.toml
  │   └── README.md
  ├── terminal/
  │   ├── alacritty/
  │   ├── ghostty/
  │   ├── gnome-terminal/
  │   ├── kitty/
  │   ├── wezterm/
  │   ├── xfce-terminal/
  │   └── README.md
  ├── fonts/
  │   └── README.md
  ├── git/
  │   ├── gitconfig
  │   └── README.md
  └── scripts/
      └── README.md

  Principios concretos del diseño:

   Área                    Único propietario                                                       No debe contener
  ━━━━━━━━━━━━━━━━━━━━━━  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
   terminal/<emulador>/    Fuente, transparencia, renderizado, portapapeles propio del terminal    tmux, aliases, prompt, Git
  ──────────────────────  ──────────────────────────────────────────────────────────────────────  ────────────────────────────────────────────────────
   tmux/                   Sesiones, ventanas, paneles y atajos de tmux                            Tema del terminal, fuentes, plugins inicialmente
  ──────────────────────  ──────────────────────────────────────────────────────────────────────  ────────────────────────────────────────────────────
   shell/                  PATH, variables, aliases, funciones y completado                        Prompt y preferencias visuales
  ──────────────────────  ──────────────────────────────────────────────────────────────────────  ────────────────────────────────────────────────────
   starship/               Prompt                                                                  Inicialización repartida en varios archivos
  ──────────────────────  ──────────────────────────────────────────────────────────────────────  ────────────────────────────────────────────────────
   git/                    Configuración de Git                                                    Tokens, claves o secretos
  ──────────────────────  ──────────────────────────────────────────────────────────────────────  ────────────────────────────────────────────────────
   fonts/                  Inventario e instalación de fuentes                                     Colores, layouts y opciones de tmux
  ──────────────────────  ──────────────────────────────────────────────────────────────────────  ────────────────────────────────────────────────────
   scripts/                Automatización explícita y documentada                                  Configuración oculta al ejecutarse automáticamente
  ──────────────────────  ──────────────────────────────────────────────────────────────────────  ────────────────────────────────────────────────────
   legacy/                 Referencia histórica de solo lectura                                    Dependencias de la arquitectura nueva

  Reglas operativas que aplicaría:

  - legacy/README.md declarará que nada fuera de esa carpeta puede cargar, enlazar ni depender de archivos legacy.
  - Cada archivo tendrá un encabezado que explique su propósito, propietario, por qué existe y qué no debe configurarse allí.
  - Starship tendrá un único punto de inicialización: shell/zshrc para zsh y, si se admite Bash, shell/bashrc para Bash. Ambos cargarán el mismo starship/starship.toml; no habrá inicializaciones indirectas.
  - Cada emulador será reemplazable como unidad independiente: instalar o retirar Ghostty no requiere editar tmux, shell, Starship, Git ni scripts.
  - El instalador será explícito e idempotente: mostrará qué enlaces o copias realizará, no manejará secretos y no modificará configuraciones antiguas sin una acción confirmada.
  - README.md será el punto de entrada: requisitos, instalación, selección de shell/emulador y enlaces a la documentación técnica.
  - docs/decisions.md registrará decisiones irreversibles o con alternativas descartadas; por ejemplo, por qué se mantiene Ctrl+a, por qué no habrá plugins de tmux inicialmente y cómo se gestionan secretos fuera del repositorio.

  La fase de implementación empezaría creando únicamente esta estructura, sus README y la documentación de arquitectura/decisiones; todavía sin activar enlaces, tocar ~/.zshrc, ~/.tmux.conf ni migrar configuraciones.
