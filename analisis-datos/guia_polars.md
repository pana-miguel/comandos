# Guía Completa de Polars (Python)

## 1. Instalación
```bash
pip install polars
```

---

## 2. Importación
```python
import polars as pl
```

---

## 3. Crear DataFrames

```python
df = pl.DataFrame({
    "nombre": ["Ana", "Luis", "Carlos"],
    "edad": [23, 30, 35],
    "salario": [1200, 2000, 2500]
})
```

---

## 4. Lectura de Datos

```python
pl.read_csv("archivo.csv")
pl.read_parquet("archivo.parquet")
pl.read_excel("archivo.xlsx")
```

---

## 5. Exploración Básica

```python
df.head()
df.tail()
df.shape
df.columns
df.describe()
```

---

## 6. Selección de Columnas

```python
df.select("nombre")
df.select(["nombre", "edad"])
```

---

## 7. Filtrado

```python
df.filter(pl.col("edad") > 25)
df.filter((pl.col("edad") > 25) & (pl.col("salario") > 1500))
```

---

## 8. Crear y Modificar Columnas

```python
df.with_columns([
    (pl.col("salario") * 1.1).alias("salario_aumentado")
])
```

---

## 9. Ordenar

```python
df.sort("edad")
df.sort("edad", descending=True)
```

---

## 10. Agrupaciones (GroupBy)

```python
df.group_by("edad").agg([
    pl.col("salario").mean(),
    pl.col("salario").sum(),
    pl.count()
])
```

---

## 11. Joins

```python
df1.join(df2, on="id", how="inner")
df1.join(df2, on="id", how="left")
df1.join(df2, on="id", how="outer")
```

---

## 12. Operaciones con Strings

```python
df.with_columns(
    pl.col("nombre").str.to_uppercase()
)
```

---

## 13. Manejo de Nulos

```python
df.drop_nulls()
df.fill_null(0)
```

---

## 14. Expresiones

```python
df.select([
    pl.col("edad") + 10,
    pl.col("salario").log()
])
```

---

## 15. Ventanas (Window Functions)

```python
df.with_columns(
    pl.col("salario").mean().over("edad")
)
```

---

## 16. Lazy API (Optimización)

```python
df = pl.scan_csv("archivo.csv")

df.filter(pl.col("edad") > 25).select(["nombre"]).collect()
```

---

## 17. Escritura de Datos

```python
df.write_csv("salida.csv")
df.write_parquet("salida.parquet")
```

---

## 18. Funciones Útiles

```python
df.unique()
df.n_unique()
df.sample(5)
```

---

## 19. Recuento y Estadísticas

```python
df.select(pl.count())
df.select(pl.col("edad").mean())
df.select(pl.col("edad").max())
df.select(pl.col("edad").min())
```

---

## 20. Buenas Prácticas

- Usar Lazy API para grandes volúmenes
- Evitar loops, usar expresiones
- Encadenar operaciones
- Preferir Parquet sobre CSV
