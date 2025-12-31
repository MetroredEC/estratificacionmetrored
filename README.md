# Herramienta de Asignación de Auditores

Esta aplicación web estática permite cargar la base `ARC_AUDITORIA_MEDICA.csv`, filtrar por mes (opcional), estratificar por especialidad y asignar automáticamente las historias clínicas a dos auditores: **Dra. Mayte Vargas** y **Dr. Xavier Asan**. Al terminar el proceso, puedes descargar un archivo CSV con todas las historias y el auditor asignado.

## Cómo usarla

1. Descomprime la carpeta `estratificacion-asignacion-real` en la raíz de tu repositorio (o carpeta `docs/`) publicada en GitHub Pages. Asegúrate de que `index.html` esté en la raíz de la rama de publicación.
2. Abre la página en el navegador. Verás un formulario simple:
   - **Archivo ARC_AUDITORIA_MEDICA.csv:** selecciona el archivo CSV con las columnas originales (por ejemplo, `FECHA_ADMISION`, `CENTRO_MEDICO`, `ESPECIALIDAD`, etc.). La aplicación detecta automáticamente si el separador es coma, punto y coma o tabulador.
   - **Mes (opcional):** si eliges un mes en formato `YYYY‑MM`, la aplicación filtrará los registros para ese mes. Si dejas el campo vacío, se utilizarán todas las filas del CSV.
   - **Procesar y asignar:** lee el archivo, agrupa los registros por especialidad y asigna cada uno de forma alterna a **Mayte Vargas** y **Xavier Asan**. El resultado se muestra en una tabla con las primeras filas como vista previa.
   - **Descargar CSV asignado:** guarda el archivo resultante (`ARC_auditores_asignados.csv`) con los datos originales más una columna `AUDITOR` indicando quién auditará cada historia.

## Características

- No requiere servidor ni dependencias externas: funciona únicamente en el navegador.
- Detecta automáticamente el delimitador del CSV (coma, punto y coma, tabulador o barra vertical).
- Permite filtrar los registros por mes (`FECHA_ADMISION` o `FECHA ADMISION`), tomando en cuenta fechas en formatos `dd/mm/yyyy` y `yyyy-mm-dd`.
- Asignación equitativa por especialidad: reparte las historias de cada especialidad de forma alterna entre los dos auditores.
- Previsualización de los primeros 10 registros asignados.

## Limitaciones y notas

1. Esta herramienta asigna **todas** las historias disponibles (o las del mes filtrado) en proporciones iguales. No realiza muestreo ni fraccionamiento. Si requieres calcular una muestra (por ejemplo, el 10 % de cada especialidad), deberás adaptar el código para seleccionar solo una fracción de registros.
2. El archivo de salida utiliza comas como separador y añade una columna llamada `AUDITOR` al final. Si tu CSV de origen tiene comas en los campos, conviene convertirlo previamente a un formato estándar o asegurarte de que el separador sea claro.
3. Las auditoras están codificadas en el script como `Dra. Mayte Vargas` y `Dr. Xavier Asan`. Puedes cambiarlos editando la variable `auditors` en `index.html`.
4. La aplicación no almacena datos en el navegador ni envía la información a un servidor. Todo se procesa en memoria y se descarta cuando recargas la página.

Este módulo cumple con el requisito de una asignación automática y descarga directa en un entorno estático, sin demos ni flujos adicionales. Puedes integrarlo en tu portal existente o personalizarlo según tus necesidades.