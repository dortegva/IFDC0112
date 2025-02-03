

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
|Electric Range|| The range of the vehicle on a full electric charge.|
|Base MSRP| The manufacturer's suggested retail price for the vehicle.|
|Legislative District| The legislative district associated with the vehicle registration location.|
|DOL Vehicle ID| Unique identifier assigned by the Washington State Department of Licensing.|
|Vehicle Location| The precise location of the vehicle.|
|Electric Utility| The electric utility company associated with the vehicle.|
|2020 Census Tract| The census tract where the vehicle is registered.|

## ¿Cuántos registros hay en el fichero?
99784 registros (hay que restar una línea al resultado obtenido para tener en cuenta la cabecera)

```bash
wc -l Electric_Vehicle_Population_Data.csv
```

## ¿De cuántos estados hay vehículos registrados?
Hay información de **5 estados**

```bash
cut -d ';' -f4 Electric_Vehicle_Population_Data.csv | sort | uniq | grep -v State | wc -l
```
## ¿En que posición se encuentra la columna con el año de fabricación?
Se encuentra en la **columna número 6**. Se añade el comando grep -n '$' para que añada el número de columna y saber cuál hay que buscar

```bash
head -1 Electric_Vehicle_Population_Data.csv | sed -e 's/;/\n/g' | grep -n '$'
```
## ¿En que año se fabricó el vehículo matriculado en Texas (TX)?
En 2019

```bash
cut -d ';' -f6,4 Electric_Vehicle_Population_Data.csv | grep TX
```
## ¿Cuál es el modelo de vehículo matriculado en Californía (CA)?
El modelo es el **Model Y**

```bash
cut -d ';' -f4,8 Electric_Vehicle_Population_Data.csv | grep 'CA;'
```
## ¿De cuántas ciudades del estado de Washigthon hay datos en el fichero?
De **347 ciudades** del estado de Washington

```bash
cut -d';' Electric_Vehicle_Population_Data.csv -f3,4 | grep 'WA' | cut -d';' -f1 | sort -u | grep -v City | wc -l
```
## De los vehículos registrados en la ciudad de Shelton, el que tiene el mayor rango electrico, ¿cuántas millas puede recorrer?
Puede recorrer hasta **330 millas**

```bash
cut -d';' -f3,11 Electric_Vehicle_Population_Data.csv | grep 'Shelton' | cut -d';' -f2 | grep -v 'Electric Range' | sort -gr | head -1
```
## ¿Cuál es el DOL vehicle ID de ese vehículo que alcanza esa distancia máxima?
El DOL ID de ese vehículo es **5YJSA1E24L**

```bash
cut -d';' -f1,3,11 Electric_Vehicle_Population_Data.csv | grep Shelton | cut -d';' -f1,3 | grep '330'
```
## ¿Cuáles son los fabricantes que tienen más de 4000 vehiculos registrados?
Son **4 fabricantes** con más de 4000 vehículos registrados

```bash
cut -d';' -f7 Electric_Vehicle_Population_Data.csv | sort | uniq -c | sort -r | awk -F' ' '$1>4000' | wc -l
```

## ¿Qué modelo de Nissan es lider en ventas?
Es el **Nissan Leaf** con 6322 unidades

```bash
cut -d';' -f7,8 Electric_Vehicle_Population_Data.csv | grep NISSAN | cut -d';' -f2 | sort | uniq -c | sort -r | head -1
```

## Ordena de mayor a menor autonomía promedio a los fabricantes

```bash
Escribe la linea de comandos bash con la  que has obtenido la respuesta
```