---
title: Buenas Prácticas de Cron en macOS
description: Cómo configurar cron en macOS resolviendo los problemas habituales de permisos (Full Disk Access) y entorno ($PATH).
date: 2026-03-22
source: https://github.com/jpgil/playbook/blob/main/macOS-cron-practices.md
---

# Buenas Prácticas: Cron en macOS

`cron` sigue siendo completamente funcional en macOS y es una excelente opción rápida frente a `launchd`, especialmente si tienes memoria muscular de Linux. Sin embargo, macOS impone dos restricciones de seguridad y entorno que hacen que los trabajos programados fallen silenciosamente si no se configuran.

## 1. El Problema de Permisos (Full Disk Access)

**Síntoma:** Error `Operation not permitted` en los logs, correos de error del sistema o fallos al leer/escribir archivos.

**Causa:** System Integrity Protection (SIP). macOS no permite que ningún proceso en segundo plano (como `cron`) lea o escriba en las carpetas de usuario protegidas (Documentos, Escritorio, Descargas, y repositorios en la nube como iCloud, Google Drive o Dropbox) a menos que el usuario lo autorice explícitamente.

**Solución:** Darle a `/usr/sbin/cron` "Acceso total al disco".

1. Abre **Configuración del Sistema** (System Settings) > **Privacidad y seguridad** (Privacy & Security).
2. Haz clic en **Acceso total al disco** (Full Disk Access).
3. Haz clic en el botón `+` en la parte inferior izquierda e ingresa tu contraseña.
4. Presiona `Cmd + Shift + G` (Ir a la carpeta) y escribe: `/usr/sbin/cron`.
5. Selecciona el ejecutable `cron` y dale a "Abrir". 
6. Verifica que el interruptor quede activado.

---

## 2. El Problema del Entorno ($PATH)

**Síntoma:** Error `command not found` referenciando comandos instalados por el usuario (como paquetes de Homebrew, Node, Python, CLI de IA, etc).

**Causa:** `cron` ejecuta comandos en un shell casi vacío y no lee tus perfiles normales (`.zshrc`, `.bash_profile`). Su variable `$PATH` por defecto es algo escasa (típicamente `/usr/bin:/bin`). Por lo tanto, no sabrá dónde están instalados los binarios como `/opt/homebrew/bin/tu-comando`.

**Solución:** Declarar explícitamente el `$PATH` al inicio del archivo `crontab`.

### Ejemplo de Configuración Correcta en `crontab -e`

```bash
# Declarar PATH incluyendo Homebrew y directorios locales
PATH=/opt/homebrew/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin

# Tarea de ejemplo (Ejecutar en el minuto 15 de cada hora)
# Recomendaciones:
# 1. Usa comillas en la ruta de trabajo si contiene espacios.
# 2. Agrupa los comandos entre paréntesis para forzar una única salida.
# 3. Redirige la salida estándar y de error a un solo log (>> mi-log.txt 2>&1).

15 * * * * cd "/Users/tu-usuario/ruta/a/tu/proyecto" && (date; tu-comando --opcion) >> cron-execution.log 2>&1
```

---

## Checklist (`crontab -l`)

- [ ] ¿`cron` tiene Full Disk Access habilitado?
- [ ] ¿Tu `crontab` declara explícitamente la variable `PATH` al principio?
- [ ] ¿Las rutas en los comandos utilizan comillas absolutas?
- [ ] ¿Concatenas y agrupas stdout/stderr (`2>&1`) útil para debuggear?

---

## Fronteras

| Nivel | Regla |
|---|---|
| **Hacer siempre** | Declarar `PATH` al inicio del crontab. |
| **Hacer siempre** | Redirigir stdout y stderr a un log para detectar fallos silenciosos. |
| **Preguntar primero** | Antes de otorgar Full Disk Access a un nuevo binario. |
| **Nunca hacer** | Asumir que el entorno de cron tiene el mismo `$PATH` que tu terminal. |
