# Catálogo de Datos — Piloto Montes de Málaga

Cada fuente se registra con: propietario, acceso, cobertura, resolución, y qué variable aporta al modelo de riesgo.

## 1. Índice de riesgo de incendio forestal (FWI)

- **Propietario:** Junta de Andalucía (Portal Ambiental de Andalucía), con cálculo de AEMET.
- **Acceso:** descarga pública / cartografía web, por provincia (Málaga).
- **Cobertura:** toda Andalucía, filtrable a Montes de Málaga.
- **Resolución temporal:** diaria, con previsión a 3 días.
- **Variables:** clasificación 0–4 de riesgo, basada en temperatura, humedad, viento, precipitación y estado de la vegetación.
- **Uso en el proyecto:** capa base de riesgo meteorológico diario.

## 2. Detecciones satelitales de fuego activo (histórico e incendios recientes)

- **Propietario:** NASA FIRMS (MODIS, VIIRS, Landsat).
- **Acceso:** API pública + descargas históricas.
- **Resolución espacial:** MODIS ~1 km, VIIRS ~375 m, Landsat ~30 m (no intercambiables, cada una con su incertidumbre).
- **Uso:** histórico de incendios en la zona, validación de zonas ya afectadas.

## 3. Vegetación e índices espectrales (NDVI/NDMI)

- **Propietario:** Copernicus / Sentinel (ESA), acceso libre.
- **Acceso:** Copernicus Open Access Hub o Google Earth Engine.
- **Resolución:** 10–20 m, revisita cada 5 días.
- **Uso:** estado del combustible vegetal, estrés hídrico de la vegetación.

## 4. Topografía (pendiente, orientación, elevación)

- **Propietario:** Instituto Geográfico Nacional (IGN), Centro de Descargas CNIG.
- **Acceso:** modelos digitales del terreno (MDT) públicos y gratuitos.
- **Resolución:** 5–25 m según la hoja.
- **Uso:** pendiente y orientación como factores de propagación y accesibilidad.

## 5. Infraestructura y accesos

- **Propietario:** catastro (Sede Electrónica del Catastro) + OpenStreetMap para vías y caminos forestales.
- **Acceso:** descarga pública / API.
- **Uso:** accesibilidad, proximidad a caminos, distancia a zonas urbanizadas (interfaz urbano-forestal).

## 6. Datos propios (dron)

- **Propietario:** tú (Uppercam).
- **Método:** vuelos con DJI Mavic 4 Pro sobre zonas concretas señaladas como prioritarias por las capas anteriores.
- **Aporta:** validación visual del estado real de la vegetación/accesos, algo que las fuentes públicas no cubren con suficiente detalle local.
- **Nota:** en esta fase, uso puntual y manual — la automatización de vuelos queda para una fase posterior.

## Lo que queda fuera de esta fase

- Sensores IoT propios, estaciones meteorológicas locales, LiDAR — se incorporarán solo si el piloto demuestra valor y se justifica la inversión.
- Datos de otras empresas de drones — entran en la fase de escalado, no en el piloto.
