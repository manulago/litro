# litro

SPA instalable (PWA) para comparar precios de carburantes en España, localizar estaciones y estimar ahorro con consumo del vehículo.

## Ejecutar

Abre `index.html` en un navegador moderno o sirve esta carpeta desde un servidor estático (por ejemplo `npx serve .`). Para geolocalización el navegador requiere HTTPS o localhost. La app consulta el servicio oficial Geoportal de Gasolineras del Ministerio:

`https://sedeaplicaciones.minetur.gob.es/ServiciosRESTCarburantes/PreciosCarburantes/EstacionesTerrestres/`

Si no hay conexión, aparecen tres datos de demostración claramente indicados en pantalla. La búsqueda por ciudad usa Nominatim / OpenStreetMap. El mapa usa Leaflet y cartografía OpenStreetMap; la ruta de coche se obtiene de OSRM. Las apps de navegación se abren mediante enlaces a Google Maps o Waze. Los servicios públicos de rutas y búsqueda tienen límites de uso y requieren internet. Con una ubicación fijada, solo lista estaciones con coordenadas y precio del combustible elegido a un máximo de 40 km; la distancia se calcula en línea recta y el coste del desplazamiento es una estimación, mientras la ruta se calcula por carretera.

Para reducir tráfico, no se consulta el Geoportal al inicio: se piden solo los productos elegidos cuando se selecciona una zona (consultas de producto en paralelo, en lugar del catálogo nacional completo). Los datos oficiales se guardan por combustible en IndexedDB durante 4 horas; «Actualizar» solicita una versión nueva. Leaflet y sus teselas se cargan al acercarse al mapa y las distancias se reutilizan al cambiar consumo u ordenar.

La geolocalización del navegador necesita HTTPS o localhost; una URL HTTP servida por la IP local no puede obtenerla. Para instalar en Android: publica/abre la URL HTTPS en Chrome y selecciona «Añadir a pantalla de inicio».

## Publicar en Vercel

Es una SPA estática, sin paso de compilación ni dependencias de npm. Importa el repositorio en Vercel con **Framework Preset: Other**, sin comando de build y con `.` como directorio de salida. Al desplegar en HTTPS funcionará la geolocalización del navegador.

## Atribuciones

- Precios: Geoportal de Gasolineras del Ministerio para la Transición Ecológica.
- Mapa: © OpenStreetMap contributors. Leaflet 1.9.4 se distribuye bajo su licencia BSD en `leaflet/LICENSE`.
- Búsqueda de lugares: Nominatim / OpenStreetMap. Rutas: OSRM.
- El logotipo de Plenergy procede del archivo publicado en su sitio oficial; las marcas pertenecen a sus respectivos titulares.
