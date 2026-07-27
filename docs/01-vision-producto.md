# Visión de Producto

## Nombre del proyecto

Piloto de inteligencia territorial para prevención de incendios — Montes de Málaga

## Contexto y problema

Los Montes de Málaga son un espacio natural periurbano de alto valor ecológico y paisajístico, situado junto a una de las áreas metropolitanas más pobladas de Andalucía. La combinación de orografía abrupta, masa forestal continua, abandono de usos agrícolas tradicionales y presión climática (olas de calor, sequías prolongadas) eleva el riesgo de incendio forestal de un año para otro.

Hoy, la prevención se apoya principalmente en inspecciones sobre el terreno, cartografía estática y criterios expertos que se actualizan con poca frecuencia. Esto dificulta:

- Detectar de forma temprana zonas con acumulación de combustible vegetal o cambios de riesgo.
- Priorizar de forma objetiva dónde actuar primero (desbroces, vigilancia, actuación de medios).
- Compartir una imagen común y actualizada del riesgo entre los distintos actores implicados (administración forestal, protección civil, bomberos, ayuntamientos, propietarios).

## Visión

Convertir datos territoriales (satélite, climáticos, topográficos, histórico de incendios y de gestión forestal) en una **capa de inteligencia de riesgo de incendio** clara, actualizada y accionable para el Parque Natural Montes de Málaga, que permita pasar de una prevención reactiva a una prevención basada en datos y priorización objetiva del riesgo.

## A quién sirve

- **Administración y gestores del espacio natural**: planificación de trabajos de prevención (desbroces, cortafuegos, vigilancia).
- **Protección Civil y servicios de extinción**: identificación de zonas críticas y apoyo a la planificación operativa en campaña de riesgo.
- **Ayuntamientos del entorno**: información para la toma de decisiones sobre urbanismo en interfaz urbano-forestal y comunicación a la ciudadanía.
- **Propietarios y gestores forestales**: visibilidad sobre el riesgo en sus parcelas para priorizar actuaciones.

## Qué construimos (piloto)

Un piloto que integra fuentes de datos abiertas y territoriales para generar un **mapa/índice de riesgo de incendio** del área de Montes de Málaga, con foco en:

1. **Ingesta de datos**: variables relevantes para el riesgo (vegetación/combustible, pendiente y orientación, clima reciente y previsto, histórico de incendios, accesos e infraestructura de extinción).
   - Datos propios capturados con dron (DJI Mavic 4 Pro): validación visual puntual de vegetación y accesos en zonas priorizadas por las capas anteriores. La automatización de vuelos y el uso de drones de terceros quedan fuera de esta fase.
2. **Modelo de riesgo**: combinación de estas variables en un índice o clasificación de riesgo por zonas, con metodología documentada y trazable.
3. **Visualización**: un mapa interactivo que permita explorar el riesgo por zonas y priorizar áreas de actuación.
4. **Validación**: contraste del modelo con conocimiento experto y, en la medida de lo posible, con eventos históricos.

## Alcance real de esta fase

Este piloto lo desarrolla y ejecuta una sola persona (sin equipo multidisciplinar todavía). El objetivo no es lanzar una plataforma operativa, sino demostrar con datos reales que el enfoque funciona, como base para escalarlo después. Los actores institucionales mencionados en "A quién sirve" son a quién se le mostrará el resultado una vez validado, no usuarios activos de esta fase.

## Qué queda fuera del piloto (por ahora)

- Predicción operativa en tiempo real durante un incendio activo.
- Gestión de despliegue de medios de extinción.
- Cobertura fuera del ámbito de Montes de Málaga (aunque el diseño debe permitir extenderlo a otros espacios).

## Criterios de éxito

- Existe un índice de riesgo de incendio para el ámbito del piloto, actualizable y explicable.
- El resultado es interpretable y útil para priorizar actuaciones de prevención por parte de los gestores del territorio.
- La arquitectura de datos y modelo permite iterar (nuevas variables, mejor resolución temporal/espacial) sin rehacer el sistema desde cero.
- Los actores clave (gestores del parque, protección civil) validan que el mapa refleja razonablemente el riesgo conocido del terreno.

## Principios de diseño

- **Basado en datos abiertos y reproducibles**: priorizar fuentes públicas y metodologías documentadas frente a cajas negras.
- **Explicable antes que sofisticado**: un modelo simple y comprensible por los gestores es preferible a uno complejo que no se pueda auditar.
- **Iterativo**: el piloto es un punto de partida, no un producto cerrado; debe poder mejorarse con más datos y validación de campo.
- **Pensado para la acción**: el output debe ayudar a decidir dónde y cuándo actuar, no solo describir el riesgo.
