# Tablero MetroBahía

Proyecto de Inteligencia de Negocios · Universidad Autónoma del Caribe · **Grupo 4**

## ¿De qué trata?

MetroBahía es un sistema de buses en fase piloto en Barranquilla y Soledad (dos rutas con 14 estaciones y un expreso de Soledad al norte). Este tablero web le muestra al **director de operaciones**, de un vistazo, si la operación va bien o mal y dónde está el problema.

**Pregunta que responde:** ¿cuántos buses despachar por ruta y franja del día, y qué estaciones reforzar?

**Quién lo usa y cada cuánto:** el director de operaciones, cada semana, y todos los días en las horas pico.

## Integrantes

| Integrante | Rol |
|---|---|
| Hernán Arias | Líder de proyecto y analista de negocio |
| John Franco | Ingeniero de datos |
| Emanuel Polo | Desarrollador de la lógica |
| Jeilyn Garcia | Desarrolladora de pantallas |
| Camilo Peñaranda | Calidad y despliegue |

## Tecnología

- **Python + Dash:** pantallas, gráficas, filtros e inicio de sesión
- **PostgreSQL:** base de datos (el tablero lee solo de aquí, nunca de los Excel)
- **Docker:** para que corra igual en el computador y en el servidor
- **GitHub:** código del grupo y publicación

## Datos del cliente

| Archivo | Qué contiene |
|---|---|
| `estaciones.csv` | Catálogo de estaciones (separador `;`) |
| `rutas.xlsx` | Catálogo de rutas |
| `validaciones.xlsx` | Cada paso de tarjeta en una estación |
| `despachos.xlsx` | Despachos programados y realizados por ruta y franja |

Los archivos traen errores (duplicados, textos escritos distinto, valores negativos, fechas vacías). Al cargarlos se revisa cada fila: lo que está bien se guarda y lo que no se rechaza con su motivo. **Los datos nunca se corrigen a mano.**

## Indicadores

1. Cumplimiento de despachos (meta ≥ 97 %)
2. Validaciones por día hábil (meta ≥ 200)
3. Ingresos por pasajes
4. Despachos no realizados
5. Variación mensual de ingresos
6. Validaciones por despacho

Las fórmulas y los semáforos están en [`docs/indicadores.md`](docs/indicadores.md).

## Carpetas

```
docs/        diagrama de la base de datos, boceto e indicadores
```

(Se irán agregando las carpetas del código, las pruebas y el Docker en los siguientes momentos.)

## Cómo correrlo

Se completa en el Momento 2, cuando esté el Docker y la base de datos en el servidor.

> Ninguna contraseña ni dirección privada va dentro del código: se usan variables de entorno.

## Estado del proyecto

| Momento | Fecha | Qué incluye |
|---|---|---|
| 1 | 11 de noviembre | Cliente entendido, indicadores, diseño de la base de datos y repositorio |
| 2 | 18 de noviembre | Base de datos en el servidor y carga de archivos |
| 3 | 25 de noviembre | Tablero completo con filtros, detalle con clic y perfiles |
| 4 | 2 de diciembre | Pruebas automáticas, validación con el cliente y entrega |
