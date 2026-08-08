# Akai Releases

Repositorio publico de distribucion para las actualizaciones de Akai.

No contiene codigo fuente, keystores, credenciales ni archivos de configuracion privados.

## Contenido publicado

- `update.json`: manifiesto que consulta Akai para detectar una version nueva.
- `akai.apk`: asset del ultimo GitHub Release. No se guarda en el historial Git.

## Publicar una version

1. En el repositorio privado de Akai, aumentar `versionName` y `versionCode`.
2. Ejecutar `AnimeFLVApp/android/gradlew.bat assembleRelease`.
3. Crear un GitHub Release con tag `v<versionName>` y adjuntar `app-release.apk` con el nombre `akai.apk`.
4. Copiar el `update.json` generado a la raiz de este repositorio y subirlo a `main`.

El manifiesto se publica al final, cuando el asset `akai.apk` ya esta disponible. Asi los dispositivos nunca reciben una URL de descarga inexistente.
