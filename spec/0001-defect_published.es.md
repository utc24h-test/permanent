# Nota de publicación 0001

| | |
|---|---|
| **Publicada** | 2026-09-09 |
| **Código** | `defect_published` |

## Qué pasó

Se encontraron dos defectos en textos que ya estaban publicados en este repositorio.

**1. La especificación decía que los turnos eran cada cinco minutos.** Son cada diez, y lo son
desde el 2026-08-27. `spec/README.md` y `spec/README.es.md` traían un ejemplo armado sobre las
`05:05`, un instante que no es un turno y no tiene archivo. Quien siguiera ese ejemplo buscaba
archivos que no pueden existir.

**2. Las reglas de los avisos se contradecían a sí mismas.** `spec/notices.md` decía que las notas
de publicación viven en `spec/NNNN-*.md` —Markdown— y, dos líneas más abajo, que van *firmadas con
la misma clave que todo lo demás*. Un archivo Markdown no puede llevar una firma adentro. Las dos
afirmaciones no podían ser ciertas a la vez, así que la regla no decía qué es una nota.

**3. El parte de incidente publicaba cuatro campos que la especificación no declaraba** —
`variant`, `attempts`, `unanchored_commitment` y `warning_en`. Quien leyera la especificación se
encontraba con campos de los que nunca se le habló.

## Qué se hizo

Los tres se corrigieron en el lugar, en los dos idiomas:

- se agregó el párrafo de la cadencia y se rehizo el ejemplo sobre las `05:10`
- las notas quedan declaradas como **Markdown y sin firma**, con el motivo escrito al lado de la
  regla: una nota informa, no prueba. Si una clave de firma estuviera en manos ajenas, firmar con
  ella *«me robaron la clave»* no probaría nada — quien la tiene puede firmar lo mismo. Lo que
  respalda a una nota es dónde vive: este repositorio es *append-only* y la fecha del commit la
  pone el proveedor, no nosotros.
- se agregaron los cuatro campos a la tabla del parte de incidente, marcados como que solo aparecen
  cuando corresponden

**Nada de lo emitido cambió.** Son documentos, no el formato: no se tocó ningún archivo `.jws`,
ninguna firma ni ninguna regla de derivación, y todo lo publicado hasta hoy reproduce exactamente
igual que antes.

## Qué debería comprobar un tercero

- `spec/README.es.md` describe una cadencia de diez minutos, y su ejemplo usa instantes que sí son
  turnos
- `spec/notices.es.md` ya no afirma que un archivo Markdown esté firmado
- la tabla del parte de incidente lista todos los campos que un parte puede llevar
- el historial de este repositorio muestra que esos archivos fueron **modificados y nunca
  reemplazados**: las versiones anteriores siguen en el log, con la fecha que el proveedor le puso
  a cada commit
