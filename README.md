# Sistema de Consulta SQL con LLM

Un sistema de consulta en lenguaje natural para bases de datos SQLite que utiliza modelos de lenguaje grande (LLM) para convertir preguntas en consultas SQL.

## Descripción

Este proyecto implementa un asistente de consulta que permite realizar preguntas en lenguaje natural sobre una base de datos SQLite (Chinook). El sistema utiliza modelos de lenguaje (LLM) y técnicas de recuperación para convertir automáticamente las preguntas del usuario en consultas SQL válidas y ejecutarlas para obtener resultados.

### Características principales

- Conversión de preguntas en lenguaje natural a consultas SQL
- Uso de técnicas de few-shot learning con ejemplos de consultas
- Sistema de recuperación de nombres propios para mejorar la precisión
- Compatible con la base de datos Chinook (música, artistas, álbumes, etc.)
- Implementado con LangChain y LangGraph para un flujo estructurado de razonamiento

## Requisitos

Este proyecto está diseñado para ejecutarse principalmente en Google Colab.

### Dependencias

- langchain-huggingface
- langchain-core
- faiss-cpu
- python-dotenv
- langchain-community
- langgraph
- langchain-groq

## Configuración

### 1. Preparación del entorno

1. Sube la base de datos SQLite `Chinook_v2.db` a tu Google Drive en una carpeta llamada `tp2_tpfinal/`.
2. Crea un archivo `.env` en la raíz de tu Google Drive con la siguiente variable:
   ```
   GROP_API_KEY=tu_api_key_de_groq
   ```
3. Abre el notebook en Google Colab.

### 2. Montar Google Drive

El notebook automáticamente montará tu Google Drive para acceder a la base de datos y al archivo de variables de entorno.

### 3. Instalación de dependencias

El notebook incluye los comandos necesarios para instalar todas las dependencias requeridas.

## Uso

### Ejecución del notebook

1. Ejecuta todas las celdas del notebook secuencialmente para configurar el entorno.
2. Una vez configurado, puedes utilizar las funciones `pretty_answer()` o `print_answer()` para realizar consultas.

### Ejemplos de consultas

```python
print_answer("Which country's customers spent the most?")
print_answer("List all albums by AC/DC")
print_answer("What is the average duration of tracks in the Rock genre?")
```

### Funciones principales

- `pretty_answer(question)`: Devuelve la respuesta generada por el agente para una pregunta dada.
- `print_answer(question)`: Imprime la pregunta y la respuesta con un formato claro y visual.
- `answer(question)`: Función de depuración interna que muestra todos los pasos de razonamiento del agente.

## Estructura del proyecto

- **Inicialización de la base de datos**: Conexión a la base de datos SQLite Chinook.
- **Configuración del modelo LLM**: Utiliza Llama a través de Groq como proveedor del LLM.
- **Few-shot learning**: Configuración de ejemplos de pares (pregunta, consulta SQL) para guiar al modelo.
- **Sistema de recuperación**: Índices vectoriales FAISS para nombres propios y ejemplos.
- **Flujo de ejecución**: Utiliza un agente ReAct para seguir un proceso estructurado de razonamiento.

## Flujo de trabajo del agente

El agente sigue este orden para procesar cada pregunta:
1. Lista las tablas disponibles en la base de datos
2. Obtiene el esquema de las tablas relevantes
3. Recupera ejemplos similares de consultas SQL
4. Busca nombres propios si es necesario
5. Formula y ejecuta la consulta SQL final

## Base de datos

El proyecto utiliza la base de datos Chinook, que contiene información sobre una tienda de música, incluyendo:
- Artistas
- Álbumes
- Canciones
- Clientes
- Facturas
- Empleados
- Géneros musicales

## Notas adicionales

- El modelo utiliza la API de Groq, que requiere una clave de API válida.
- El sistema está diseñado para consultas de solo lectura y no permite operaciones DML (INSERT/UPDATE/DELETE).
- Para mejores resultados, formule preguntas claras y específicas sobre la información contenida en la base de datos.