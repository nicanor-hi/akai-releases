# Akai Releases

Repositorio publico de distribucion para las actualizaciones de Akai.

No contiene codigo fuente, keystores, credenciales ni archivos de configuracion privados.

## Canales y contenido publicado

- Mobile: `update.json` y el asset de GitHub Release `akai.apk`.
- TV: `update-tv.json` y el asset de GitHub Release `akai-tv.apk`.
- Las APK no se guardan en el historial Git; `*.apk` está excluido.

Los manifiestos conservan el contrato de seis campos de Akai: `versionName`,
`versionCode`, `downloadUrl`, `sha256`, `releaseNotes` y `mandatory`. Mobile
mantiene la URL histórica
`https://raw.githubusercontent.com/nicanor-hi/akai-releases/main/update.json`
y el asset `akai.apk` disponible en
`https://github.com/nicanor-hi/akai-releases/releases/latest/download/akai.apk`.
Conservar ambos contratos permite que versiones antiguas de Akai Mobile sigan
consultando y descargando actualizaciones Mobile.

## Preparación local

Desde la raíz del proyecto principal `flv-app-react-native`, compila ambas
variantes Release o solo el flavor que haya cambiado. Después ejecuta allí el
script de preparación con `both`, `mobile` o `tv`:

```text
scripts/windows/PWSH_COPY_RELEASE_TO_UPDATES.bat both
scripts/windows/PWSH_COPY_RELEASE_TO_UPDATES.bat mobile
scripts/windows/PWSH_COPY_RELEASE_TO_UPDATES.bat tv
scripts/linux/COPY_RELEASE_TO_UPDATES.sh both
scripts/linux/COPY_RELEASE_TO_UPDATES.sh mobile
scripts/linux/COPY_RELEASE_TO_UPDATES.sh tv
```

Por defecto se preparan los dos canales. En el modo de un solo canal, el script
requiere que el APK y manifiesto vigentes del otro canal ya estén en este
repositorio y que su SHA coincida. Si no están o no se pueden verificar, debe
detenerse; proporciona manualmente el par vigente verificable antes de reintentar.
Los scripts solo preparan y validan los archivos: no ejecutan Git ni publican.

## Publicación manual

Todo GitHub Release que vaya a ser **Latest** debe adjuntar ambos assets:
`akai.apk` y `akai-tv.apk`. Esto también aplica a un release que solo actualice
uno de los canales: el otro APK y su manifiesto se conservan con su versión y
SHA originales, sin recompilarlo ni sustituirlo por un artefacto desconocido.

Revisa que cada `downloadUrl` apunte al nombre correcto y que el hash del
manifiesto coincida con el asset antes de publicar. Mantén ambos manifiestos en
la rama `main` de este repositorio. La subida de assets y los cambios Git son
pasos manuales; no existe publicación automática. GitHub Release y el cambio
de los manifiestos no son atómicos: durante la transición, un cliente puede
ver el manifiesto anterior y descargar el asset nuevo de `latest`. La validación
SHA rechaza esa combinación de forma segura; publica ambos pasos seguidos.
