# Documentos para el sistema RAG

Esta carpeta debe contener los **archivos Markdown** (`.md`) que el tutorial carga y segmenta para construir el índice vectorial.

## Uso

- Coloque aquí todos los `.md` que desee indexar.
- El notebook `03_rag_base.ipynb` (y el flujo integrado en `06_integration.ipynb`) leen desde esta carpeta por defecto.
- La segmentación se hace con `MarkdownHeaderTextSplitter` usando los encabezados `#`, `##`, `###` y `####`.

## Otra ubicación

Si prefiere usar otra ruta o nombre de carpeta, cambie el parámetro `data_folder` en:

- `load_documents(data_folder="data")` en el notebook 03.

## Estructura recomendada

Los archivos pueden estar directamente en `data/` (p. ej. `data/doc1.md`, `data/doc2.md`). No es necesario crear subcarpetas; el código recorre todos los `.md` de la carpeta indicada.
