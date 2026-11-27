# Indicadores del tablero MetroBahía

Los datos de cada fórmula salen de los archivos del cliente ya revisados y guardados en la base de datos.

## 1. Fórmulas, metas y semáforo

| # | Indicador | Fórmula | Meta | Verde | Amarillo | Rojo |
|---|---|---|---|---|---|---|
| 1 | Cumplimiento de despachos | Σ despachos realizados ÷ Σ despachos programados × 100 | 97 % | ≥ 97 % | 94 % a menos de 97 % | < 94 % |
| 2 | Validaciones por día hábil | Total de validaciones ÷ número de días hábiles del periodo | 200 | ≥ 200 | 170 a 199 | < 170 |
| 3 | Ingresos por pasajes | Σ valor_pasaje de las validaciones del mes | Mayor que el mes anterior | ≥ mes anterior | hasta 3 % menos que el mes anterior | más de 3 % menos |
| 4 | Despachos no realizados | Σ (programados − realizados) por ruta y franja; también como % de los programados | 0 (menor es mejor) | ≤ 3 % | más de 3 % y hasta 6 % | > 6 % |
| 5 | Variación mensual de ingresos | (ingresos del mes − ingresos del mes anterior) ÷ ingresos del mes anterior × 100 | Crecer cada mes | ≥ 0 % | −3 % a menos de 0 % | < −3 % |
| 6 | Validaciones por despacho | Total de validaciones ÷ Σ despachos realizados, por ruta y franja | ≤ 3 validaciones por despacho | ≤ 3 | más de 3 y hasta 4,5 | > 4,5 |

Las metas de los indicadores 1, 2 y 3 las dio el cliente. Los umbrales de amarillo y rojo los propuso el grupo y se pueden ajustar (si se cambian, se anota en el registro de decisiones).

## 2. ¿De dónde sale cada dato?

| Dato que usa la fórmula | Archivo y columna | ¿Existe? |
|---|---|---|
| Despachos programados | `despachos.xlsx` → `despachos_programados` | Sí |
| Despachos realizados | `despachos.xlsx` → `despachos_realizados` | Sí |
| Ruta y franja del despacho | `despachos.xlsx` → `cod_ruta`, `franja` | Sí |
| Fecha del despacho | `despachos.xlsx` → `fecha` | Sí |
| Validaciones (conteo) | `validaciones.xlsx` → una fila por paso de tarjeta | Sí |
| Fecha y hora de la validación | `validaciones.xlsx` → `fecha_hora` | Sí |
| Valor del pasaje | `validaciones.xlsx` → `valor_pasaje` | Sí |
| Estación de la validación | `validaciones.xlsx` → `cod_estacion` | Sí |
| Ruta de la estación | `estaciones.csv` → `ruta` | Sí |
| **Días hábiles** | No viene en ningún archivo | **No: hay que calcularlo** |
| **Franja de una validación** | Las validaciones solo traen la hora | **No: hay que calcularla** |

## 3. Cosas que hay que resolver

- **Días hábiles:** ningún archivo dice qué días son hábiles. Hay que definir la regla (por ejemplo, lunes a viernes sin festivos de Colombia) y guardarla, por ejemplo en una tabla `calendario`.
- **Franja de las validaciones:** las validaciones solo traen la hora, así que se asignan a una franja según su hora. Mirando los datos, se concentran en dos bloques, y las franjas quedan así: Pico mañana 5:00 a 8:00, Valle 8:00 a 17:00, Pico tarde 17:00 a 19:00 y Noche 19:00 a 5:00. Es una propuesta del grupo.
- **Ruta R3 (expreso):** `estaciones.csv` no tiene estaciones de R3, así que sus validaciones no se pueden calcular por estación. Hay que preguntarle al cliente (docente) cómo se registran.
- **Tarifa:** subió en enero de 2026, así que el valor del pasaje cambia según la fecha. Esto afecta los indicadores 3 y 5: la variación de enero puede venir de la tarifa y no de más pasajeros.
- **Meta del indicador 6:** el cliente no la dio ni hay datos de la capacidad de los buses. Con los datos limpios, R1 tiene unas 3,1 validaciones por despacho y R2 unas 1,3. Se propone verde ≤ 3, amarillo hasta 4,5 y rojo más de 4,5. Es un umbral provisional del grupo.

## 4. Errores de los archivos que afectan los cálculos

- `despachos.xlsx`: filas repetidas, franjas escritas distinto, fechas vacías, fila "SUBTOTAL" y valores raros en `despachos_realizados` ("-", con coma, negativos).
- `validaciones.xlsx`: encabezado de 4 filas, filas repetidas, tarjetas y estaciones mal escritas (E15, e03, E0), fechas vacías o fuera del periodo, y `valor_pasaje` con "-", negativos o vacíos.

Todo esto se limpia o se rechaza en la carga, y lo rechazado queda registrado con su motivo.
