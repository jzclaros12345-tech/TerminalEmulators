# Git

Esta carpeta existe para versionar una base de Git portable y segura. Separa
las decisiones compartibles de la identidad y de las credenciales de cada
equipo.

## Contenido

- `gitconfig`: opciones generales sin nombre, correo ni credenciales.
- `gitignore_global`: descartes personales globales deliberadamente mínimos.
- `attributes`: normalización de texto para el propio repositorio.
- `hooks/`: reserva para hooks versionados futuros; actualmente no ejecuta
  nada.

## Fuera del repositorio

Configura la identidad localmente, por ejemplo con `git config --global
user.name` y `git config --global user.email`. Tokens, claves SSH y
credenciales se gestionan mediante el sistema, un gestor de credenciales o un
agente SSH; nunca se añaden a este árbol.
