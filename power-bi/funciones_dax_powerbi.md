# Funciones DAX en Power BI (con ejemplos comentados)

Este documento explica las funciones más comunes de **DAX (Data Analysis
Expressions)** en Power BI, con descripciones claras y ejemplos
prácticos.\
Fuente oficial: [Referencia de DAX -
Microsoft](https://learn.microsoft.com/en-us/dax/dax-function-reference)

------------------------------------------------------------------------

## 1. Funciones de Agregación

-   `SUM(column)` → Suma los valores de una columna numérica.\
-   `AVERAGE(column)` → Calcula el promedio.\
-   `MIN(column)` / `MAX(column)` → Devuelve el valor mínimo o máximo.\
-   `COUNT(column)` → Cuenta los valores **no nulos**.\
-   `COUNTROWS(table)` → Cuenta el número de filas de una tabla.\
-   `DISTINCTCOUNT(column)` → Devuelve el número de valores únicos.\
-   Iteradores (`SUMX`, `AVERAGEX`, `MINX`, `MAXX`) → Recorren fila por
    fila de una tabla aplicando una expresión.

**Ejemplo**:

``` dax
Total Ventas = SUM(Ventas[Monto])
Promedio por Producto = AVERAGEX( VALUES(Productos[Nombre]), [Total Ventas] )
```

------------------------------------------------------------------------

## 2. Funciones de Fecha y Hora / Time Intelligence

-   `DATE(year, month, day)` → Crea una fecha.\
-   `TODAY()` → Devuelve la fecha actual.\
-   `NOW()` → Devuelve fecha y hora actuales.\
-   `YEAR(date)`, `MONTH(date)`, `DAY(date)` → Extraen partes de la
    fecha.\
-   `WEEKDAY(date, [return_type])` → Devuelve el día de la semana.\
-   `DATEDIFF(start, end, unit)` → Diferencia entre dos fechas en días,
    meses o años.\
-   `EOMONTH(start_date, months)` → Último día del mes de la fecha.\
-   Inteligencia de tiempo:
    -   `TOTALYTD(expression, dates)` → Total acumulado en el año hasta
        hoy.\
    -   `DATESMTD()`, `DATESQTD()`, `DATESYTD()` → Devuelven rangos de
        fechas acumulados.\
    -   `SAMEPERIODLASTYEAR(dates)` → Mismo rango pero del año
        anterior.\
    -   `DATEADD(dates, interval, unit)` → Desplaza fechas.\
    -   `ENDOFMONTH(dates)`, `STARTOFYEAR(dates)` → Devuelven inicios o
        fines de periodos.

------------------------------------------------------------------------

## 3. Funciones Lógicas y de Información

-   `IF(condición, valor_si_verdadero, valor_si_falso)` → Lógica
    condicional.\
-   `SWITCH(expresión, valor1, resultado1, ..., [else])` → Evaluación
    múltiple (como CASE en SQL).\
-   `AND()`, `OR()`, `NOT()` → Operadores lógicos.\
-   `ISBLANK(x)` → ¿Es nulo?\
-   `ISERROR()`, `ISTEXT()`, `ISNUMBER()` → Verifican tipo de valor.\
-   `RELATED(tabla[columna])` → Trae un valor relacionado desde otra
    tabla.\
-   `LOOKUPVALUE(resultado, columna_búsqueda, valor)` → Busca un valor
    en otra tabla.

------------------------------------------------------------------------

## 4. Funciones de Filtro y Contexto

-   `CALCULATE(expression, filtro...)` → Cambia el contexto de
    evaluación aplicando filtros.\
-   `FILTER(tabla, condición)` → Devuelve solo las filas que cumplen una
    condición.\
-   `ALL(tabla_o_columna)` → Quita todos los filtros.\
-   `ALLEXCEPT(tabla, columna1, ...)` → Quita filtros excepto los de las
    columnas especificadas.\
-   `CALCULATETABLE(tabla, filtro...)` → Igual que `CALCULATE` pero
    devuelve tabla.\
-   `KEEPFILTERS(filtro)` → Mantiene filtros existentes al aplicar
    otros.\
-   `SELECTEDVALUE(columna, [alternativa])` → Devuelve el valor
    seleccionado o un alternativo si hay más de uno.

------------------------------------------------------------------------

## 5. Funciones de Texto

-   `CONCATENATE(text1, text2)` o `&` → Une textos.\
-   `CONCATENATEX(tabla, expresión, delimitador)` → Concatena varios
    valores.\
-   `FORMAT(valor, formato)` → Formatea un número o fecha como texto.\
-   `LEFT(texto, n)`, `RIGHT(texto, n)`, `MID(texto, inicio, longitud)`
    → Extraen partes del texto.\
-   `LEN(texto)` → Longitud del texto.\
-   `TRIM(texto)` → Elimina espacios extra.\
-   `SEARCH(palabra, texto)` / `FIND()` → Devuelve la posición de una
    palabra dentro de un texto.

------------------------------------------------------------------------

## 6. Funciones Matemáticas y Trigonométricas

-   `ABS(x)` → Valor absoluto.\
-   `CEILING(x, base)` / `FLOOR(x, base)` → Redondeo hacia
    arriba/abajo.\
-   `ROUND(x, decimales)` → Redondeo normal.\
-   `DIVIDE(num, den, [alternativo])` → División segura (evita error de
    /0).\
-   `SQRT(x)` → Raíz cuadrada.\
-   `POWER(x, y)` → Potencia.\
-   Trigonometría: `SIN`, `COS`, `TAN`, `ASIN`, etc.

------------------------------------------------------------------------

## 7. Funciones de Relación y Tablas

-   `RELATED()` → Trae un valor de una tabla relacionada.\
-   `RELATEDTABLE()` → Devuelve todas las filas de una tabla
    relacionada.\
-   `USERELATIONSHIP(col1, col2)` → Activa una relación inactiva en el
    modelo.\
-   `CROSSJOIN(tabla1, tabla2)` → Producto cartesiano.\
-   `UNION(tabla1, tabla2)` → Une filas de tablas.\
-   `INTERSECT(tabla1, tabla2)` → Coincidencias entre tablas.

------------------------------------------------------------------------

## 8. Funciones de Ranking y Estadísticas

-   `RANKX(tabla, expresión, [valor], [orden], [empates])` → Crea un
    ranking.\
-   `MEDIAN(x)` / `MEDIANX(tabla, expresión)` → Mediana.\
-   `VAR.P`, `VAR.S`, `STDEV.P`, `STDEV.S` → Varianzas y desviaciones
    estándar.\
-   `SUMMARIZE(tabla, columnas, expresión)` → Agrupa como en SQL GROUP
    BY.\
-   `SUMMARIZECOLUMNS(...)` → Agrupación optimizada.

------------------------------------------------------------------------

## 9. Ejemplo práctico: Generar Edades 1--97

### Lista completa (con el 2 incluido):

``` dax
Edades =
GENERATESERIES(1, 97, 1)
```

👉 Esto crea una tabla con una columna `[Value]` con valores del **1 al
97 incluyendo el 2**.

### Lista sin el 2:

``` dax
Edades =
FILTER(
    GENERATESERIES(1, 97, 1),
    [Value] <> 2
)
```

👉 Esto crea la misma tabla pero **excluyendo el 2**.

------------------------------------------------------------------------

## Nota Final

Esta chuleta está pensada como **referencia rápida**.\
Para la lista completa y oficial:\
👉 [Referencia oficial de
Microsoft](https://learn.microsoft.com/en-us/dax/dax-function-reference)\
👉 [DAX Guide](https://dax.guide/)
