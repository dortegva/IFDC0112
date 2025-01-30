

# Ejercicio de análisis exploratorio de datos

Haz una copia de la carpeta "cars" a tu area de ensayo.

Vamos a realizar un análisis exploratorio de los datos contenido en el fichero Electric_Vehicle_Population_Data.csv.

El metadata del fichero es:

|Columna | Descripcion|
|----------|-----------|
|VIN (1-10)| Partial vehicle identification number consisting of the first 10 digits.|
|County| The county where the vehicle is registered.|
|City| The city where the vehicle is registered.|
|State| The state where the vehicle is registered.|
|Postal Code| The postal code of the vehicle registration location|
|Model Year| The year the vehicle was manufactured.|
|Make| The manufacturer or brand of the vehicle.|
|Model| The specific model of the vehicle.|
|Electric Vehicle Type| Indicates whether the vehicle is a Battery Electric Vehicle (BEV) or a Plug-in Hybrid Electric Vehicle (PHEV).|
|Clean Alternative Fuel Vehicle (CAFV) Eligibility| Indicates if the vehicle is eligible for Clean Alternative Fuel Vehicle benefits.|
|Electric Range| The range of the vehicle on a full electric charge.|
|Base MSRP| The manufacturer's suggested retail price for the vehicle.|
|Legislative District| The legislative district associated with the vehicle registration location.|
|DOL Vehicle ID| Unique identifier assigned by the Washington State Department of Licensing.|
|Vehicle Location| The precise location of the vehicle.|
|Electric Utility| The electric utility company associated with the vehicle.|
|2020 Census Tract| The census tract where the vehicle is registered.|

## ¿Cuántos registros hay en el fichero?
99784
```bash
Escribe la linea de comandos bash con la  que has obtenido la respuesta
```
wc -l elecveh.csv (esto cuenta las lineas pero registros seria uno menos porque la primera linea es la de los títulos)

## ¿De cuántos estados hay vehículos registrados?
5
```bash
Escribe la linea de comandos bash con la  que has obtenido la respuesta
cut -d ';' -f 4 elecveh.csv | sort | uniq |wc -lc (esto cuenta las lineas pero registros seria uno menos porque la primera linea es la de los títulos)
```

## ¿En que posición se encuentra la columna con el año de fabricación?
6
```bash
Escribe la linea de comandos bash con la  que has obtenido la respuesta
head -n 1 elecveh.csv | tr ';' '\n' | grep -n "Model Year" | cut -d ':' -f 1
```
## ¿En que año se fabricó el vehículo matriculado en Texas (TX)?
2019
```bash
awk -F';' '$4=="TX" {print $6}'
o
cut -d';' -f4,6 elecveh.csv | grep TX | cut -d';' -f2
Escribe la linea de comandos bash con la  que has obtenido la respuesta
```
## ¿Cuál es el modelo de vehículo matriculado en Californía (CA)?
2021
```bash
Escribe la linea de comandos bash con la  que has obtenido la respuesta
awk -F';' '$4=="CA" {print $6}'
o 
cut -d';' -f4,6 elecveh.csv | grep CA | cut -d';' -f2
-f4,6 para coger la 4 y la 6 columna
```
## ¿De cuántas ciudades del estado de Washigthon hay datos en el fichero?
351
```bash
Escribe la linea de comandos bash con la  que has obtenido la respuesta

cut -d';' -f3,4 elecveh.csv | grep WA |sort | uniq | cut -d';' -f1| wc -l
```
## De los vehículos registrados en la ciudad de Shelton, el que tiene el mayor rango electrico, ¿cuántas millas puede recorrer?

330
```bash
Escribe la linea de comandos bash con la  que has obtenido la respuesta
cut -d';' -f3,11  elecveh.csv | grep Shelton | cut -d';' -f2 | sort -nr | head -n 1
```
## ¿Cuál es el DOL vehicle ID de ese vehículo que alcanza esa distancia máxima?
108257964
```bash
Escribe la linea de comandos bash con la  que has obtenido la respuesta
cut -d';' -f3,11,14  elecveh.csv | grep Shelton | cut -d';' -f2,3 | sort -nr | head -n 1| cut -d';' -f2
```
## ¿Cuáles son los fabricantes que tienen más de 4000 vehiculos registrados?

```bash
Escribe la linea de comandos bash con la  que has obtenido la respuesta
cut -d';' -f7  elecveh.csv | sort -n |
```

## ¿Qué modelo de Nissan es lider en ventas?

```bash
Escribe la linea de comandos bash con la  que has obtenido la respuesta
```

## Ordena de mayor a menor autonomía promedio a los fabricantes

```bash
Escribe la linea de comandos bash con la  que has obtenido la respuesta
```