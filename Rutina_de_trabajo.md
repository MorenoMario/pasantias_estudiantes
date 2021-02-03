# Día 1

## Entrar al servidor
Antes de comenzar con cualquier tipo de trabajo en la pantalla negra, debemos aprender a conectarnos de forma remota. 
##### Nota: Descagar dos programas muy útiles [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html), [winscp](https://winscp.net/eng/download.php) y [Notepad++](https://notepad-plus-plus.org/downloads/)

## En putty
```
-mmorenos.ddns.net
-user: javier
-Pass: javier2021
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
### Tarea 1: Acceder a los genomas depositados en la carpeta "01_genomas" en tus Documentos.
> Explorar y abrir cada uno de los archivos depositados
> Que formato logras identificar?

`Deposita acá tu respuesta:` El formato de los archivos es .fa o FASTA, se puede observar que la primera línea iniciada por un ">", el nodo, la longitud de la secuencia y la cobertura correspondiente.

### Tarea 2:
>Acceder a la base de datos del [NCBI](https://www.ncbi.nlm.nih.gov/)
-Buscar la base de datos de genomas del NCBI
-Descargar un genoma de referencia [ejemplo](https://www.ncbi.nlm.nih.gov/genome/?term=E.%20coli)
-Descargar archivo [Fasta](https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/005/845/GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_genomic.fna.gz) del genoma.
-Descargar archivo [GFF](https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/005/845/GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_genomic.gff.gz) del genoma.
-Descargar archivo [GBK](https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/005/845/GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_genomic.gbff.gz) del genoma.

> Que formato logras identificar?

`Deposita acá tu respuesta:` Se identifican 3 formatos, FASTA(.fa), GFF(.gff) y GeneBank(.gbff) respectivamente

> Alguna diferencia entre archivos?

`Deposita acá tu respuesta:` El archivo FASTA nos muestra la secuencia con una información mínima, en cuanto a GBK este nos enseña una interfaz con información relevante a las bases de datos de NCBI. El archivo GFF nos muestra las regiones respectivas de la secuencia, su función y localización.

### Para comenzar a explorar los genomas descargados vamos a usar un programa llamado [Geneious](https://www.geneious.com/download/). El programa es muy útil, pero es pagado :( , por lo tanto vamos a usar la version trial de 14 días.

> Crear una carpeta llamada `"02_genomas_ncbi"` (usar comandos linux)
> Copiar los archivos desgargados desde el `NCBI` a la carpeta `"02_genomas_ncbi"` usando el programa `winscp`

Cargar los archivos de `genomas`, `GBK`  y `GFF` en Geneious

### Explorar en programas y ver que información tienes en cada archivo
- `Deposita acá tu respuesta:` FASTA...
- `Deposita acá tu respuesta:` GBK...
- `Deposita acá tu respuesta:` GFF...

## Identificación de genes de interes en los genomas

De acuerdo a lo que observamos el archivo GFF es muy útil para identificar las coordenadas de los genes de un genoma.

#Vamos a usar esta información para extraer los genes ribosomales de los genomas tanto descargados

# Día 2

##Hoy usaremos la información contenida en el archivo `.gff` para extraer algunos genes de interés.

Inicialmente usaremos la herramienta [`Barnap`](https://github.com/tseemann/barrnap) y el webserver de [`RNAmmer`](http://www.cbs.dtu.dk/services/RNAmmer/)

Extraeremos las coordenadas de la posición de los genes ribosomales del genoma de *E. coli* (archivo.fasta)


> barrnap --threads 10 --kingdom bac --outseq output.txt input.fasta

### Explorar en archivo de salida 
- `Que información tiene el archivo?:` output.txt...

Esta información es útil cuando tenemos un computador/servidor donde podamos correr el programa, si no tenemos esta opción podemos ocupar la plataforma online de 
[`RNAmmer`](http://www.cbs.dtu.dk/services/RNAmmer/)

- `Que información tiene la salida?:` output.txt...

Descargar archivo fasta de cada genoma depositado en la 



