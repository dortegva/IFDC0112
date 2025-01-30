+ cabecera head 5 <file>
+ cola tail 7 <file>
+ contar columnas

    substituimos los separadores por un retorno de linea. Contamos las lineas.
    ```bash
    head -1 flags.csv | sed -e s/:/\\n/g | wc -l
    ```
wc-> para contar palabras

+ extraer datos de una columna


    ```bash
awk -F: '{print $10}' flags.csv | head -5
    ```
el $ es per dir la columna

 cut -d: -f10,11 flags.csv
 cut comando para cortar
 -d para delimitar ( en este caso delimitas con : por eso le especificamos el caracter)-> -d:
 -f las columnas que querremos coger
flags.csv = <nombre del archivo que queremos seleccionar>

grep -v <valor/palabra/caracter> (el -v es para que te excluya el siguiente valor/palabra caracter)
