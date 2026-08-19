# Decisiones de arquitectura

Este registro existe para conservar el motivo de las decisiones importantes y
evitar que la configuración vuelva a depender de memoria o de suposiciones.

## 2026-08-05 — Reconstrucción en lugar de reparación

**Decisión:** crear configuraciones nuevas y no reparar las activas como base.

**Motivo:** la auditoría identificó bloques tmux duplicados, cargas repetidas
de NVM y PATH, configuraciones visuales repartidas entre terminales y una
dependencia de plugins. Reparar cada detalle conservaría intenciones no
verificables y deuda técnica.

**Consecuencia:** solo se rescatarán comportamientos que se decidan de forma
explícita. El prefijo tmux `Ctrl+a` es uno de ellos.

## 2026-08-05 — Legacy aislado

**Decisión:** mantener `legacy/` solo como referencia histórica sin carga.

**Motivo:** permite consultar configuraciones anteriores sin convertirlas en
una dependencia implícita del nuevo diseño.

## 2026-08-05 — Terminales como adaptadores

**Decisión:** una carpeta por emulador bajo `terminal/`.

**Motivo:** fuente, transparencia, renderizado y preferencias de ventana son
propiedad del emulador. Tmux y las capas inferiores deben servir a cualquier
cliente de terminal.

## 2026-08-05 — Sin plugins de tmux inicialmente

**Decisión:** la primera versión de tmux no tendrá TPM, temas, restauración ni
plugins.

**Motivo:** una base pequeña y comprobable permite añadir una dependencia cada
vez, con una razón, prueba y documentación explícitas.

## 2026-08-05 — Base tmux de Fase 3A

**Decisión:** configurar solo `Ctrl+a`, división, navegación de paneles,
recarga, historial y ratón.

**Motivo:** son las operaciones mínimas de multiplexación. Las teclas `h/j/k/l`
tras el prefijo son más transportables que combinaciones Alt y no requieren
capacidades particulares de un emulador.

**Consecuencia:** color, truecolor, barra personalizada, persistencia,
portapapeles del sistema y plugins esperan fases posteriores.

## 2026-08-05 — Git seguro desde el inicio

**Decisión:** preparar `git/` con configuración compartible, atributos e
ignore global, pero sin identidad, credenciales, tokens, claves ni hooks.

**Motivo:** Git es parte del entorno reproducible, mientras que identidad y
secretos pertenecen a cada equipo y deben configurarse fuera del repositorio.
