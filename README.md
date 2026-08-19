# Entorno de desarrollo Linux

Este repositorio es la documentación técnica y la fuente reproducible del
entorno de desarrollo. Existe para que el entorno pueda entenderse,
reconstruirse y migrarse sin depender de memoria ni de una configuración
preexistente.

La arquitectura separa terminal, tmux, shell, Starship, Git, fuentes y
automatización. Cada componente tiene un único propietario y puede retirarse
sin obligar a cambiar los demás.

## Estado del proyecto

La estructura base está creada. Aún no hay configuraciones activas migradas ni
instalador ejecutable. La siguiente fase reconstruirá tmux desde cero.

## Lectura recomendada

1. [Arquitectura](docs/architecture.md)
2. [Decisiones](docs/decisions.md)
3. [Roadmap](docs/roadmap.md)
4. [Instalación](docs/installation.md)

## Documentación canónica y antecedentes

`docs/` contiene la documentación canónica de la arquitectura nueva. Los
documentos de diseño situados en la raíz se conservan sin cambios como
antecedentes de la auditoría y de la transición; no son una configuración
activa ni sustituyen las decisiones registradas en `docs/decisions.md`.

## Límites de seguridad

Este repositorio no contiene secretos, tokens, claves privadas ni credenciales.
Los valores sensibles se gestionan fuera del repositorio.
# TerminalEmulators
