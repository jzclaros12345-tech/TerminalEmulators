# Graph Report - dotfiles  (2026-08-19)

## Corpus Check
- 32 files · ~6,883 words
- Verdict: corpus is large enough that graph structure adds value.

## Summary
- 146 nodes · 119 edges · 31 communities (12 shown, 19 thin omitted)
- Extraction: 100% EXTRACTED · 0% INFERRED · 0% AMBIGUOUS
- Token cost: 0 input · 0 output

## Community Hubs (Navigation)
- Arquitectura
- Auditoría de entorno de terminal
- Dotfiles.md
- Roadmap de migración
- 4. tmux
- Roadmap
- Decisiones de arquitectura
- Validación de tmux — Fase 3A
- 2. Shell
- Auditoría de reconstrucción — Fase 1
- Git
- Atajos de teclado
- Migrar de emulador de terminal
- Resolución de problemas
- architecture.md
- bootstrap/README.md
- comandosTeclado.md
- fonts/README.md
- hooks/README.md
- legacy/README.md
- scripts/README.md
- shell/README.md
- starship/README.md
- alacritty/README.md
- ghostty/README.md
- gnome-terminal/README.md
- kitty/README.md
- terminal/README.md
- wezterm/README.md
- xfce-terminal/README.md

## God Nodes (most connected - your core abstractions)
1. `Auditoría de entorno de terminal` - 13 edges
2. `Roadmap de migración` - 10 edges
3. `Roadmap` - 8 edges
4. `4. tmux` - 8 edges
5. `Decisiones de arquitectura` - 7 edges
6. `Principios` - 6 edges
7. `2. Shell` - 6 edges
8. `Arquitectura` - 6 edges
9. `Entorno de desarrollo Linux` - 5 edges
10. `5. Terminal Emulator` - 4 edges

## Surprising Connections (you probably didn't know these)
- None detected - all connections are within the same source files.

## Communities (31 total, 19 thin omitted)

### Community 0 - "Arquitectura"
Cohesion: 0.10
Nodes (15): Arquitectura, Capas y propiedad, Legacy, Principios, Puntos de carga previstos, Reemplazo de terminales, Estado actual, Instalación (+7 more)

### Community 1 - "Auditoría de entorno de terminal"
Cohesion: 0.13
Nodes (14): 10. Árbol de configuración, 11. Problemas detectados, 12. Recomendaciones para revisión posterior, 1. Sistema, 3. Starship, 5. Terminal Emulator, 6. Fonts, 7. Clipboard (+6 more)

### Community 2 - "Dotfiles.md"
Cohesion: 0.14
Nodes (13): 1. Primero entender, luego configurar, 2. Cambios pequeños, 3. Sin duplicados, 4. Documentación antes que memoria, 5. Portabilidad, Convención de commits, Dotfiles, Filosofía del proyecto (+5 more)

### Community 3 - "Roadmap de migración"
Cohesion: 0.18
Nodes (10): Fase 0, Fase 1, Fase 2, Fase 3, Fase 4, Fase 5, Fase 6, Fase 7 (+2 more)

### Community 4 - "4. tmux"
Cohesion: 0.25
Nodes (8): 4. tmux, Bindings propios, Layouts observados, Opciones globales y de ventana efectivas, Plugins, Posibles configuraciones obsoletas, Ratón, historial, color y barra de estado, Versión, archivo y servidor

### Community 5 - "Roadmap"
Cohesion: 0.25
Nodes (8): Fase 1, Fase 2, Fase 3, Fase 4, Fase 5, Fase 6, Fase 7, Roadmap

### Community 6 - "Decisiones de arquitectura"
Cohesion: 0.29
Nodes (7): 2026-08-05 — Base tmux de Fase 3A, 2026-08-05 — Git seguro desde el inicio, 2026-08-05 — Legacy aislado, 2026-08-05 — Reconstrucción en lugar de reparación, 2026-08-05 — Sin plugins de tmux inicialmente, 2026-08-05 — Terminales como adaptadores, Decisiones de arquitectura

### Community 7 - "Validación de tmux — Fase 3A"
Cohesion: 0.29
Nodes (5): Tmux, Checklist de configuración, Checklist de ejecución pendiente, Copia y pegado, Validación de tmux — Fase 3A

### Community 8 - "2. Shell"
Cohesion: 0.33
Nodes (6): 2. Shell, Bash: configuración declarada, Frameworks y plugins de shell, PATH observado en la sesión auditada, Shell activo y archivos de inicio, zsh: configuración declarada

### Community 9 - "Auditoría de reconstrucción — Fase 1"
Cohesion: 0.50
Nodes (3): Auditoría de reconstrucción — Fase 1, Restricción de seguridad, Resultado

### Community 10 - "Git"
Cohesion: 0.50
Nodes (3): Contenido, Fuera del repositorio, Git

## Knowledge Gaps
- **97 isolated node(s):** `Dotfiles`, `Filosofía del proyecto`, `Objetivos`, `1. Primero entender, luego configurar`, `2. Cambios pequeños` (+92 more)
  These have ≤1 connection - possible missing edges or undocumented components.
- **19 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `Auditoría de entorno de terminal` connect `Auditoría de entorno de terminal` to `2. Shell`, `4. tmux`?**
  _High betweenness centrality (0.032) - this node is a cross-community bridge._
- **Why does `4. tmux` connect `4. tmux` to `Auditoría de entorno de terminal`?**
  _High betweenness centrality (0.016) - this node is a cross-community bridge._
- **Why does `Decisiones de arquitectura` connect `Decisiones de arquitectura` to `Arquitectura`?**
  _High betweenness centrality (0.013) - this node is a cross-community bridge._
- **What connects `Dotfiles`, `Filosofía del proyecto`, `Objetivos` to the rest of the system?**
  _97 weakly-connected nodes found - possible documentation gaps or missing edges._
- **Should `Arquitectura` be split into smaller, more focused modules?**
  _Cohesion score 0.1 - nodes in this community are weakly interconnected._
- **Should `Auditoría de entorno de terminal` be split into smaller, more focused modules?**
  _Cohesion score 0.13333333333333333 - nodes in this community are weakly interconnected._
- **Should `Dotfiles.md` be split into smaller, more focused modules?**
  _Cohesion score 0.14285714285714285 - nodes in this community are weakly interconnected._