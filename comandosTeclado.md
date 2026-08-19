Nivel 1 — Lo imprescindible (úsalo todos los días)
Crear una sesión
tmux new -s Backtester
Ver sesiones
tmux ls
Entrar a una sesión
tmux attach -t Backtester
Salir sin cerrar
Ctrl+a
d

(detach)

Cerrar una sesión
tmux kill-session -t Backtester
Ventanas

Nueva ventana

Ctrl+a c

Siguiente

Ctrl+a n

Anterior

Ctrl+a p

Elegir ventana

Ctrl+a w

Renombrar

Ctrl+a ,
Paneles

Horizontal

Ctrl+a -

Vertical

Ctrl+a |

Moverse

Ctrl+a h

Ctrl+a j

Ctrl+a k

Ctrl+a l

Cerrar panel

exit

o

Ctrl+d
Redimensionar

Más adelante puedes configurar

Ctrl+a Shift+h

Ctrl+a Shift+l

Ctrl+a Shift+j

Ctrl+a Shift+k
Recargar configuración
Ctrl+a r
Mouse

Si está activado

seleccionar panel
redimensionar
scroll
Historial

Entrar

Ctrl+a [

Salir

q
Copiar

Dentro del modo copia

Space

mover cursor

Enter

Pegar

Ctrl+a ]
Nivel 2 — Administración

Ver clientes

tmux list-clients

Ver ventanas

tmux list-windows

Ver paneles

tmux list-panes

Renombrar sesión

tmux rename-session -t idb backend

Cambiar nombre ventana

Ctrl+a ,
Nivel 3 — Servidores

Matar servidor completo

tmux kill-server

Nueva sesión sin entrar

tmux new -ds idb

Entrar después

tmux attach -t idb
Nivel 4 — Flujo de trabajo

Aquí es donde tmux realmente brilla.

Proyecto Backtester
Sesión: idb

Ventana 1
──────────────

Panel 1
Editor

Panel 2
Git

Panel 3
Node Server

Panel 4
Logs

────────────────────────

Ventana 2

SQLite

────────────────────────

Ventana 3

Tests

────────────────────────

Ventana 4

Descargas Binance Vision

────────────────────────

Ventana 5

htop
Dashboard Binance

Otra sesión

dashboard
Dotfiles
dotfiles
Lo que yo haría

Cada proyecto tendría

1 sesión

Nunca mezclaría proyectos.

Guardar sesiones

Aquí tienes dos caminos.

Opción 1

Plugins

TPM

Resurrect

Continuum

Guardan:

ventanas
paneles
comandos
directorios
sesiones

Muy cómodo.

Opción 2 (mi favorita para tu caso)

No guardar nada automáticamente.

Crear un script.

Ejemplo

workspace idb

Hace

si no existe

crear sesión

crear ventanas

abrir servidores

abrir logs

abrir git

abrir sqlite

attach

Es totalmente reproducible.

Y además queda versionado.

Ejemplo

Imagínate

workspace idb

Y automáticamente

idb

├── editor

├── git

├── node profile server

├── node downloader

├── sqlite

├── logs

├── htop

Todo listo.

No dependes de restaurar estados viejos.

Esto es exactamente lo que yo haría en tu proyecto

Conociendo cómo trabajas, creo que tu flujo ideal sería:

workspace idb

↓

crea sesión

↓

Ventana 1

editor

git

↓

Ventana 2

Profile Server

↓

Ventana 3

Downloader Binance Vision

↓

Ventana 4

Backtester

↓

Ventana 5

SQLite

↓

Ventana 6

Logs

↓

Ventana 7

htop

↓

attach


Si mañana cambias de ordenador, ejecutas un único comando y en menos de un minuto tienes exactamente el mismo entorno.

---

# Mi recomendación final

Yo **no usaría Resurrect ni Continuum como base de tu flujo de trabajo**. Los dejaría para mucho más adelante, como una comodidad opcional.

Para un proyecto como el tuyo, con servidores bien definidos (por ejemplo, el servidor del perfil, el descargador de Binance Vision, procesos de Node.js, SQLite, pruebas, etc.), es más robusto y reproducible definir el entorno como **código**. Un script `workspace idb` que cree toda la sesión desde cero siempre producirá el mismo resultado, queda versionado en Git, es fácil de revisar y funciona igual en cualquier máquina. Si algún proceso cambia, actualizas el script y todo el equipo de trabajo evoluciona de forma controlada.

Ese enfoque encaja muy bien con la filosofía que has estado construyendo para tu repositorio: infraestructura reproducible, documentada y sin depender de estados ocultos.