# Modelo de Riesgo — Piloto Montes de Málaga

## Enfoque

Índice de riesgo ponderado por zonas, en lugar de un modelo de machine learning entrenado. Esta decisión sigue el principio de "explicable antes que sofisticado" fijado en la visión de producto: en esta fase, con una sola persona ejecutando el piloto y sin un histórico de incendios lo bastante grande para entrenar un modelo sin sobreajustar, un índice con pesos fijos y documentados es más rápido de construir, más fácil de validar y más fácil de justificar ante gestores del parque y protección civil que una caja opaca de ML.

El índice ponderado sirve además como baseline explicable frente al que comparar, en el futuro, un modelo más sofisticado, si el piloto demuestra valor y se justifica la inversión.

## Unidad espacial

Rejilla de celdas de referencia (~100–250 m de lado) sobre el ámbito de Montes de Málaga. Es un tamaño intermedio entre la resolución de las capas de Sentinel/IGN (10–25 m) y el FWI (más agregado); cada celda hereda el valor de cada capa por superposición espacial.

## Variables de entrada y normalización

Todas las variables se normalizan a una escala 0–1, donde 1 representa el mayor riesgo.

| Variable | Fuente | Cómo se normaliza |
|---|---|---|
| Riesgo meteorológico | FWI (Junta de Andalucía / AEMET) | Escala 0–4 dividida entre 4 |
| Estrés del combustible | NDVI/NDMI (Sentinel) | Invertido: menor humedad de vegetación → mayor riesgo |
| Pendiente | MDT (IGN) | Normalizada 0–1 con tope en ~45° |
| Orientación | MDT (IGN) | Ver tabla de valores fijos abajo |
| Proximidad a incendios históricos | NASA FIRMS | Decaimiento lineal con distancia de corte (ver detalle abajo) |
| Interfaz urbano-forestal | Catastro + OpenStreetMap | Inversa a la distancia a caminos/zonas urbanizadas (más exposición/probabilidad de ignición) |

### Tabla de valores para orientación

La orientación se clasifica en 8 sectores según los grados de la ladera (0°–360°, medidos desde el norte). Las laderas sur/suroeste puntúan más alto por mayor insolación y sequedad del combustible:

| Sector | Rango (grados) | Valor de riesgo |
|---|---|---|
| Sur (S) | 157.5°–202.5° | 1.0 |
| Suroeste (SW) / Sureste (SE) | 112.5°–157.5° / 202.5°–247.5° | 0.85 |
| Oeste (W) / Este (E) | 67.5°–112.5° / 247.5°–292.5° | 0.6 |
| Noroeste (NW) / Noreste (NE) | 22.5°–67.5° / 292.5°–337.5° | 0.4 |
| Norte (N) | 337.5°–22.5° | 0.2 |
| Terreno plano (pendiente ≈ 0°, sin orientación definida) | — | 0.5 (valor neutro) |

### Detalle: proximidad a incendios históricos

Se calcula la distancia desde el centro de cada celda al incendio histórico más cercano registrado en NASA FIRMS. La contribución al riesgo decae linealmente con la distancia, con un corte físico a partir del cual se considera que no hay influencia:

- Distancia = 0 km → valor de riesgo = 1.0
- Distancia = 5 km → valor de riesgo = 0.0
- Distancia > 5 km → valor de riesgo = 0.0 (sin influencia; evita que un incendio lejano siga puntuando)

Fórmula: `valor = max(0, 1 - distancia_km / 5)`

El corte de 5 km es un valor inicial razonable para el tamaño del ámbito piloto y puede ajustarse con la validación de campo.

## Combinación

Suma ponderada de las variables normalizadas. Pesos iniciales, documentados y ajustables manualmente:

- Riesgo meteorológico (FWI): 25%
- Estado del combustible (NDVI/NDMI): 25%
- Topografía (pendiente + orientación): 20%
- Histórico de incendios: 15%
- Interfaz urbano-forestal: 15%

El resultado es una puntuación de 0 a 1 por celda, clasificada en 5 niveles: muy bajo, bajo, medio, alto, muy alto. Se usan umbrales fijos en vez de cuantiles, para que el mismo valor de riesgo signifique lo mismo de un mes a otro.

## Rol de los datos de dron

Los datos propios capturados con dron (DJI Mavic 4 Pro) no entran como variable continua del índice: su uso es puntual y manual, según el catálogo de datos. Se emplean para **validar** las celdas que el índice marca como riesgo alto o muy alto:

- Si el vuelo confirma vegetación seca o accesos bloqueados, refuerza la confianza en el modelo.
- Si lo contradice, es señal de que hay que revisar los pesos o los datos de esa zona.

## Fuera de esta versión (v1)

- Simulación dinámica de propagación (dirección/velocidad de viento en tiempo real).
- Ajuste automático de pesos (aprendizaje); los pesos son fijos y se revisan manualmente.
- Humedad de combustible in situ mediante sensores propios (ya marcado como fuera de fase en el catálogo de datos).
