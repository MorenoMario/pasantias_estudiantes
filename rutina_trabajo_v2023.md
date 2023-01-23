---
Title: " Tutorial genómica v1.0"
Author: "Mario Moreno-Pino"
Date: "23/01/2022"
---
#### El objetivo de este tutorial es caracterizar el pontencial funcional de aislados bacterianos asociados a una esponja antártica. Analizaremos los módulos de metabolitos secundario de 4 genomas bacterianos. 

# Día

## Entrar al servidor
Antes de comenzar con cualquier tipo de trabajo en la pantalla negra, debemos aprender a conectarnos de forma remota. 
##### Nota: Descagar dos programas muy útiles [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html), [winscp](https://winscp.net/eng/download.php) y [Notepad++](https://notepad-plus-plus.org/downloads/)

## En putty
```
-mmorenos.ddns.net
-user: st1
-Pass: st12023
```

## Comandos básicos Linux
Existen diferentes comandos para ingresar a la matrix de Linux. Puedes buscar en la web hay muchos [Link](http://hpc.aut.uah.es/~jmruiz/Descarga_LE/Pract_1_Comandos_Linux.pdf) con los más basicos

```

- cd : entrar a directorio
- cd .. : retroceder al directorio anterior
- pwd : conocer el directorio donde estoy
- ls : desplegar lista de archivos en directorio
- ll : desplegar lista de archivo con más info.
- less : ver archivo 
- vi : ver archivo
- nano : editar archivo
- mkdir: crear directorio
- cp: copiar archivo
- cp -r : copiar directorio
- rm : borrar (usar con sabiduria)
- mv : mover directorio/archivo a otro directorio
- head: muestra cabecera de un/unos archivos

```
### Ejemplo

```
cd /Documentos/01_genomas
mkdir 02_analisis
mv 02_analisis ../
```
### Tarea 1: Acceder a los genomas depositados en la carpeta "01_genomas" en la carpeta *Documentos*.
> Explorar y abrir cada uno de los archivos depositados
> Que formato logras identificar?

`Deposita acá tu respuesta:` El formato de los archivos es .fa o FASTA, se puede observar que la primera línea iniciada por un ">", el nodo, la longitud de la secuencia y la cobertura correspondiente.

### Tarea:
>Acceder a la base de datos del [NCBI](https://www.ncbi.nlm.nih.gov/)
-Buscar la base de datos de genomas del NCBI
-Descargar un genoma de referencia [ejemplo](https://www.ncbi.nlm.nih.gov/genome/?term=E.%20coli)
-Descargar archivo [Fasta](https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/005/845/GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_genomic.fna.gz) del genoma.
-Descargar archivo [GFF](https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/005/845/GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_genomic.gff.gz) del genoma.
-Descargar archivo [GBK](https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/005/845/GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_genomic.gbff.gz) del genoma.

> Que formato logras identificar?

`Deposita acá tu respuesta:` Se identifican 3 formatos, FASTA(.fa), GFF(.gff) y GeneBank(.gbff) respectivamente
### Explorar en programas y ver que información tienes en cada archivo
- `Deposita acá tu respuesta:` FASTA...
- `Deposita acá tu respuesta:` GBK...
- `Deposita acá tu respuesta:` GFF...

> Alguna diferencia entre archivos?

`Deposita acá tu respuesta:` El archivo FASTA nos muestra la secuencia con una información mínima, en cuanto a GBK este nos enseña una interfaz con información relevante a las bases de datos de NCBI. El archivo GFF nos muestra las regiones respectivas de la secuencia, su función y localización.

### Para comenzar a explorar los genomas descargados vamos a usar un programa llamado [Geneious](https://www.geneious.com/download/). El programa es muy útil, pero es pagado :( , por lo tanto vamos a usar la version trial de 14 días.

> Crear una carpeta llamada `"02_genomas_ncbi"` (usar comandos linux)
> Copiar los archivos desgargados desde el `NCBI` a la carpeta `"02_genomas_ncbi"` usando el programa `winscp`

Cargar los archivos de `genomas`, `GBK`  y `GFF` en Geneious


## Identificación de genes de interes en los genomas

De acuerdo a lo que observamos el archivo GFF es muy útil para identificar las coordenadas de los genes de un genoma.

#Vamos a usar esta información para extraer los genes ribosomales de los genomas tanto descargados

# Día 2

## Hoy usaremos la información contenida en el archivo `.gff` para extraer algunos genes de interés.

Inicialmente usaremos la herramienta [`Barnap`](https://github.com/tseemann/barrnap) y el webserver de [`RNAmmer`](http://www.cbs.dtu.dk/services/RNAmmer/)

Extraeremos las coordenadas de la posición de los genes ribosomales del genoma de *E. coli* (archivo.fasta)

> barrnap --threads 10 --kingdom bac --outseq output.txt input.fasta
*reemplazar output and input (seq.fasta)

- `Que información tiene el archivo? (output.txt):`  El archivo output muestra las secuencias predichas por barrnap correspondientes a las mejores opciones de secuencias 16s, 23s y 5s

Esta información es útil cuando tenemos un computador/servidor donde podamos correr el programa, si no tenemos esta opción podemos ocupar la plataforma online de 
[`RNAmmer`](http://www.cbs.dtu.dk/services/RNAmmer/)

>cargar genoma en formato `.fasta` al webserver de RNAmmer y examinar la salida (output.txt)

 - `Que información tiene la salida? (output.txt):` La salida muestra predicciones de manera ordenada correspondientes a las mejores opciones de secuencias 16s, 23s y 5s

### Extraer y descargar la región del gen 16S rRNA desde el genoma de *E. coli* en formato `.fasta` y cargarlo en `Geneious`

Ahora comenzaremos con la identificación taxonómica de *E. coli*. Eso no sería posible sin `Woese y Fox`, quienes descubrieron los 3 dominios de la vida usando los genes ribosomales. 
Como una sugerencia -(una fueeerte sugerencia)- debes leer el artículo [`Carl Woese y George Fox, 1977`](https://sci-hub.st/https://www.pnas.org/content/74/11/5088).

### Lo primeros será realizar un alineamiento del gen 16S rRNA de *E. coli* usando [BLAST](https://blast.ncbi.nlm.nih.gov/Blast.cgi) contra la base de datos de nucleótidos del NCBI

 - `Que información tiene la salida? (BLAST webserver):` La salida es un listado de los mejores hits (BBH) alineados en forma de mejor resultado al menos parecido según el criterio o parámetro seleccionado (Per.Ident, Query Cover, E-Value, etc)

### Tarea:

- `Completar la tabla las coordenadas de los genes ribosomales 16S rRNA de los genomas bacterianos asociados a esponjas (BAE):`

|Genoma<br />name  | Coordenada<br />inicio | Coordenada<br />final | Largo<br />gen | Ribosomal<br />16S/23S/5S |
| :---  | :---  | :--- | :--- | :--- |
| E16_8_1569.5 | 69692| 71241 | 1549 | 1/0/0 |
| E16_8_1569.5 | 71569 | 74496 | 2927 | 0/1/0 |
| E16_8_1569.5 | 74648 | 74756 | 108 | 0/0/1 |
| E19_1_53246.88 | 50 | 1581 | 1531 | 1/0/0|
| E19_1_53246.88 | 24 | 2911 | 2887 | 0/1/0 |
| E19_1_53246.88 | 6508 | 6584 | 76 | 0/0/1 |
| E19_3_286104.7 | 4720 | 6241 | 1521 | 1/0/0 |
| E19_3_286104.7 | 1372 | 4187 | 2815 | 0/1/0 |
| E19_3_286104.7 | 1120 | 1223 | 103 | 0/0/1 |
| E19_4_907197.4 | 285 | 1813 | 1528 | 1/0/0 |
| E19_4_907197.4 | 378 | 3262 | 2884 | 0/1/0 |
| E19_4_907197.4 | 3376 | 3477 | 101 | 0/0/1 |

- `Anotar la información de salida del alineamiento usando Blast del gen ribosomal 16S de las BAE:`

|Genoma<br />name  | Organism<br />name  | Best<br />Hit | %<br />identidad  | %<br /> cobertura |
| :---  | :---  | :--- | :--- | :--- |
| CP060287 (E16_8)| Sporosarcina sp | 16s* | 95,5 | 22,65 |
| CP014616 (E16_8)| Sporosarcina psychrophyla | 16s* | 95,5 | 22,65 |
| CP060287 (E16_8)| Sporosarcina sp | 16s* | 90,8 | 78,06 |
| CP014616 (E16_8)| Sporosarcina psychrophyla | 16s* | 90,8 | 70,06 |
| CP036528 (E16_8)| Ureibacillus thermophilus | 16s* | 73,8 | 19,87 |
| CP011025 (E19_1)| Pseudoalteromonas arctica | 16s* | 88,7 | 95 |
| CP066804 (E19_1)| Pseudoalteromonas sp | 16s* | 88,42 | 95 |
| CP040558 (E19_1)| Pseudoalteromonas sp | 16s* | 88,1 | 95 |
| CP012737 (E19_1)| Pseudoalteromonas sp | 16s* | 81,2 | 95 |
| CP013138 (E19_1)| Pseudoalteromonas sp | 16s* | 81 | 95 |
| CP060297 (E19_3)| Winogradskyella sp | 16s* | 83,2 | 80,7 |
| CP053352 (E19_3)| Winogradskyella helgolandensis | 16s* | 84,8 | 80,03 |
| CP053350 (E19_3)| Winogradskyella forsetii | 16s* | 82,9 | 79,89 |
| CP053349 (E19_3)| Winogradskyella forsetii | 16s* | 83 | 78,32 |
| CP053348 (E19_3)| Winogradskyella forsetii | 16s* | 83 | 78,32 |
| CP013145 (E19_4)| Colwellia sp | 16s* | 76,6 | 75,6 |
| CP047130 (E19_4)| Colwellia sp | 16s* | 77,1 | 75,5 |
| CP034759 (E19_4)| Litorilituus sediminis sp | 16s* | 77,4 | 74,04 |
| KT428295 (E19_4)| Colwellia sp | 16s* | 77,3 | 74,64 |
| CP000083 (E19_4)| Colwellia psychrerythraea | 16s* | 76,8 | 74,62 |

- `Anotar la información de salida del alineamiento usando Blast de los genes ribosomales 23s y 5s de las BAE:`

|Genoma<br />name  | Best<br />Hit | %<br />identidad  | %<br /> cobertura |
| :---  | :---  | :--- | :--- |
| CP060287 (E16_8)| 23s* | 94,1 | 58,40 |
| CP014616 (E16_8)| 23s* | 94,2 | 58,40 |
| CP060287 (E16_8)| 5s* | 94,5 | 100 |
| CP014616 (E16_8)| 5s* | 94,5 | 100 |
| CP011025 (E19_1)| 23s* | 89,15 | 96 |
| CP066804 (E19_1)| 23s* | 88,92 | 96 |
| CP011025 (E19_1)| 5s* | 90,91 | 100 |
| CP066804 (E19_1)| 5s* | 88 | 97 |
| CP053352 (E19_3)| 23s* | 83,3 | 53,80 |
| CP053352 (E19_3)| 23s* | 86,4 | 27,13 |
| CP013145 (E19_4)| 23s* | 78,3 | 61,53 |
| CP047130 (E19_4)| 23s* | 78,1 | 68,18 |
| CP000083 (E19_4)| 5s* | 78,4 | 99,02 |
| CP047130 (E19_4)| 5s* | 75,6 | 76,47 |


# Día 3

-Descargar la secuencia de los primeros 5 Best Blast Hits (BBH)
-Cargar las secuencias del BBH en `Geneius`
-Realizar un alineamiento múltiple (por genoma) usando las secuencias del 16S descargadas ( 5 seqs. ) y el 16S rRNA de los genomas.
-Usar Muscle o Clustal y observar la salida

- `Que información tiene el alineamiento?:` Javier... 
- `Que muestran las distintas columnas del alineamiento?`Javier... 
- `Que representan las variaciones y las conservaciones en el alineamiento?:` Javier... 

### Hacer una filogenia del 16S rRNA usando [MEGAX](https://www.megasoftware.net/)

-Realizar una limpieza del alineamiento usando [TrimalAI](http://trimal.cgenomics.org/trimal) [Gblocks](http://molevol.cmima.csic.es/castresana/Gblocks_server.html), leer [documentación](http://molevol.cmima.csic.es/castresana/Gblocks/Gblocks_documentation.html)

```
trimal -automated1 -in -out

```
### Tarea: 
- `investigar sobre los parametros usados en la versión webserver: son conservadoras? o muy flexibles? ` Javier...
 
Una vez eliminemos regiones del alineamiento pobremente conservadas, realizaremos los siguientes pasos:


1. Exportar el alineamiento generado en `Geneius`
2. Cargar el alineamiento en alineamiento en `MEGAX`
3. Estimar el mejor modelo de sustitución en cada uno de los alineamientos (hacer la prueba con un genoma) [info](https://www.ccg.unam.mx/~vinuesa/Cursos2RMBF/PDFs/C1/Tema4_modelos_de_sust_nt.pdf)
4. Realizar la filogenia usando tan solo 50 iteraciones, usando el modelo de sust. obtenido arriba
5. Cargar la filogenia en [itol]https://itol.embl.de/upload.cgi
*opción para visualizar alineamientos en terminal [mpdunne](https://github.com/mpdunne/Alan)
### Tarea:
- `completar la información clave ? ` Javier...

|Genoma<br />name  | Best<br />Model | Informative<br />sites  | Nº original<br />positions |
| :---  | :---  | :--- | :--- | 
| Rellene | Rellene | Rellene | Rellene |

# Día 4
### Average Nucleotide Identity (ANI) 
La identidad de nucleótidos promedio (ANI) es una medida de similitud genómica a nivel de nucleótidos entre las regiones codificantes de dos genomas. *.."Typically, the ANI 
values between genomes of the same species are above 95% (e.g., Escherichia coli). Values below 75% are not to be trusted, and AAI should be used instead. This tool supports both complete and draft genomes (multi-fasta)"*

1. Seleccionar un genoma de los que estamos trabajando
2. Descargar el genoma más cercano a nuestro genoma, basado en el  mejor *BBH* del gen 16S rRNA, de NCBI 
3. Subir los dos genomas ( el de interes y el descargado de la base de datos [ANI-enveomics](http://enve-omics.ce.gatech.edu/ani/) o [ANI-ezbio](https://www.ezbiocloud.net/tools/ani)
4. Anotar la información y determinar si existen diferencias entre usar únicamente el gen 16S rRNA y el genóma completo?
5. El 16S rRNA nos permite clasificar de buena manera nuestros genómas

### Tarea:

- `Computar el ANI de todos los genómas con su BBH correspondiente ` Javier...

### Anotación funcional 

Vamos a usar un anotador de genomas microbianos (bacterias y arqueas) muy usado llamado PROKKA. Javier debe leer el [Paper](https://academic.oup.com/bioinformatics/article/30/14/2068/2390517) de la herramienta.

Usaremos un genoma para realizar la anotación funcional de nuestro genóma y el BBH
```
conda activate prokka_env
prokka
prokka --outdir ./prokka_out --force --prefix E16_8 --cpus 20 E16_8_genoma.fasta
*conda deactivate*
```
Explorar las salidas y identificar las que encuentren conocidas
Buscar genes de interes, alguno conocido por producir metabolitos secundarios?.

### Tarea:
Identificar 3 genes relacionados con rutas de sintesis de metabolitos secundarios

### Tarea:

- `Anotar todos los genómas de las BAS ` Javier...

### Finalmente realizamos la identificación de módulos que sean relacionados con la sintesis de metabolitos con interés biotec. 

Por esto, emplearemos la herramienta webserver [antismash](https://antismash.secondarymetabolites.org/#!/start)










