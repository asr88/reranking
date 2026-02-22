# Tutorial RAG: Query Rewriting y Reranking

Proyecto de backend para un sistema RAG (Retrieval-Augmented Generation) que combina **query rewriting** y **reranking** sobre documentos Markdown, con orquestación del flujo mediante LangGraph.

## Contenido del tutorial

| Notebook | Descripción |
|----------|-------------|
| **03_rag_base.ipynb** | Base del RAG: carga y segmentación de documentos (MarkdownHeaderTextSplitter), índice FAISS con embeddings Google y retriever por similitud. |
| **04_query_rewriting.ipynb** | Técnicas de reescritura de consultas: zero-shot, few-shot, sub-queries, step-back e HyDE. |
| **05_reranking.ipynb** | Reranking con cross-encoder (sentence-transformers), retriever con k=10 y selección de top-k por relevancia. |
| **06_integration.ipynb** | Flujo completo integrado con LangGraph: reescritura → recuperación → reranking → generación de respuesta. |

## Requisitos

- Python 3.10+
- Clave de API de Google (Gemini) para embeddings y modelo de lenguaje

## Instalación

```bash
python -m venv venv
# Windows:
venv\Scripts\activate
# Linux/macOS:
# source venv/bin/activate

pip install -r requirements.txt
```

## Configuración

1. Cree un archivo **`.env`** en la raíz del proyecto con su clave de Google:

   ```
   GOOGLE_API_KEY=su_clave_aqui
   ```

2. Coloque los documentos Markdown en la carpeta **`data/`**. Si no existe, créela y añada archivos `.md`. El notebook 03 los cargará y segmentará por encabezados. Ver `data/README.md` para más detalle.

## Uso

1. Abra y ejecute **03_rag_base.ipynb** en orden. Esto genera la carpeta `faiss_index` con el índice vectorial.
2. Opcional: ejecute **04_query_rewriting.ipynb** y **05_reranking.ipynb** para explorar cada técnica por separado.
3. Ejecute **06_integration.ipynb** para correr el pipeline completo (reescritura + recuperación + reranking + respuesta).

Los notebooks están pensados para ejecutarse de forma incremental; se recomienda revisar la salida de cada celda.

## Estructura del proyecto

```
Backend/
├── README.md           # Este archivo
├── requirements.txt
├── .env                # GOOGLE_API_KEY (no versionado)
├── data/               # Documentos .md a indexar
│   └── README.md
├── faiss_index/        # Índice FAISS (generado por 03, no versionado)
├── 03_rag_base.ipynb
├── 04_query_rewriting.ipynb
├── 05_reranking.ipynb
└── 06_integration.ipynb
```

## Dependencias principales

- **LangChain** (langchain-google-genai, langchain-community, langchain-text-splitters, langchain-core): embeddings, splits, FAISS, prompts y cadenas.
- **LangGraph**: grafo de estados para el flujo RAG integrado.
- **sentence-transformers**: cross-encoder para reranking (p. ej. ms-marco-MiniLM-L-6-v2).
- **faiss-cpu**: índice vectorial.
- **python-dotenv**: carga de variables desde `.env`.
