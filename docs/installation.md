# Instalación

Este documento existe para describir la reconstrucción en un equipo nuevo sin
recurrir a la memoria. Aún no contiene instrucciones ejecutables porque la
configuración activa se construirá por fases.

## Estado actual

La Fase 2 solo creó la arquitectura y la documentación base. No hay enlaces,
copias ni comandos de instalación que ejecutarse todavía.

## Reglas para el instalador futuro

- Será explícito, idempotente y revisable.
- Mostrará los destinos antes de cambiar archivos.
- No sobrescribirá archivos existentes sin una copia de seguridad y una acción
  confirmada.
- Nunca administrará secretos.
- Permitirá elegir shell y emulador sin instalar componentes no solicitados.
