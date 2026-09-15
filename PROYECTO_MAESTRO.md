# PERLENTAUCHER - Proyecto maestro de Gestión de Obra
Versión: 2.0 · 15/09/2026

Este archivo es el punto de partida para futuras modificaciones. Conserva las decisiones funcionales y de diseño acordadas.

## Objetivo
Aplicación responsive para escritorio y móvil destinada a gestionar obras, incidencias, planos, fotografías, seguimientos, actas, listados y documentación de obra.

## Reglas funcionales aprobadas
- Obras: lista inicialmente vacía; se añaden según necesidad.
- Categorías: lista inicialmente vacía; se añaden/quitan según necesidad.
- Numeración de incidencias independiente por obra: 001, 002, 003...
- Nombre de archivos de informe: `Obra - Título - Nº`.
- Autor: cada incidencia y seguimiento registra la persona que lo realiza.
- Campos: obra, nº, título, fecha, categoría, zona, ubicación, responsable, estado, prioridad, descripción y autor.
- Seguimiento: una incidencia puede recibir actualizaciones posteriores con fecha, autor, comentario, estado y nuevos archivos sin perder el historial anterior.
- Planos: pertenecen a una obra; se pueden añadir, quitar y actualizar por revisión.
- Entrada de planos: selector de ruta y arrastrar/soltar PDFs.
- Fotografías/documentos: selector de ruta y arrastrar/soltar.
- Localización en plano prevista: elegir plano/página, zoom, desplazamiento, fijar vista, marcar con dedo/ratón y guardar captura sin modificar el plano original.
- Actas: agrupan cualquier conjunto de incidencias de una obra; numeración propia por obra.
- Listados: filtros por obra/categoría/zona/ubicación/estado/prioridad/responsable/fechas y exportación Excel.
- Informes: individual, por categoría, acta y listado general.

## Diseño de informe aprobado
- DIN A4.
- Sin marca de agua.
- Logotipo sin recuadro.
- Encabezado PERLENTAUCHER (todo junto) e INFORME DE INCIDENCIA en verde corporativo del pez.
- Tipografía objetivo: Neutra Cond Medium para encabezados; usar equivalente condensada si no está licenciada/disponible.
- Datos compactos: fila 1 Categoría/Zona/Ubicación; fila 2 Responsable/Estado/Prioridad; maximizar espacio de descripción.
- La sección Localización en plano solo aparece cuando hay plano/captura asociada.
- Fotografías: una sola foto ocupa todo el ancho útil; con dos o más, dos fotografías por fila. Comentario opcional alineado al ancho exacto de cada fotografía.

## Arquitectura
La entrega actual es una PWA responsive única: el mismo código adapta la interfaz a escritorio y móvil. Esto reduce mantenimiento y garantiza que las dos versiones evolucionen juntas.

## Sincronización multiusuario
Requisito aprobado: escritorio y móvil deben sincronizarse. Para activarlo en producción se necesita un backend común (base de datos, autenticación y almacenamiento de archivos) desplegado en HTTPS. Las credenciales no se incorporan al paquete maestro. La entrega actual conserva datos localmente hasta conectar dicho backend.

## Archivos principales
- `index.html`: aplicación.
- `manifest.webmanifest`: instalación PWA.
- `sw.js`: caché del shell de la aplicación.
- `assets/logo.jpg`: logotipo de informes.
- `assets/app-icon.jpg`: icono de aplicación.
- `README_INSTALACION.txt`: instrucciones rápidas.

## Próxima fase técnica obligatoria para producción multiusuario
1. Elegir backend/hosting y dominio HTTPS.
2. Crear usuarios y permisos por obra.
3. Migrar metadatos de localStorage a base de datos central.
4. Guardar fotos/PDF en almacenamiento de objetos.
5. Implementar conflictos/sincronización offline.
6. Completar visor PDF con zoom, captura y anotación táctil.
7. Generar DOCX nativo y PDFs con fotografías/planos completos desde los datos sincronizados.
8. Pruebas con varios usuarios y dispositivos antes de distribución general.

## Fase piloto individual aprobada
- Antes de activar sincronización, la aplicación se distribuirá a varios compañeros para pruebas individuales.
- Cada usuario mantiene sus propias obras y datos locales; no se comparten entre compañeros.
- El objetivo es recopilar propuestas y validar el flujo antes de construir el backend común.
- Para distribuir la misma versión en móvil como PWA, se recomienda publicar una única copia del frontend en HTTPS; el almacenamiento seguirá siendo local e independiente en cada navegador durante el piloto.
- Planos, fotografías y documentos deben poder incorporarse tanto mediante selector/ruta como mediante arrastrar y soltar.
- En el piloto actual se valida el flujo de adjuntos; la persistencia binaria completa y la anotación real de PDFs quedan para la siguiente fase técnica.
