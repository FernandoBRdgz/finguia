# Finguia

## Descripción general

`Finguia` es una interfaz conversacional construida con Streamlit que permite a los usuarios consultar reportes financieros, transcripciones y cálculos propios de las herramientas internas a través de LLMs (OpenAI) y fuentes estructuradas de datos (AlphaVantage). El proyecto incluye integración con TTS/ASR de OpenAI, una capa de prompts avanzados y llamadas a funciones para agilizar la investigación financiera.

## Requisitos previos

1. **Python 3.12+**: Este proyecto requiere al menos Python 3.12. Puedes verificar tu versión con `python --version` o `python3 --version`.
2. **CLI `uv`**: El administrador de proyectos recomendado es [uv](https://docs.astral.sh/uv/). Se puede instalar con `curl -LsSf https://astral.sh/uv/install.sh | sh`.
3. **Credenciales para APIs**:
   - `OPENAI_API_KEY`
   - `ALPHAVANTAGE_API_KEY`

## Instalación paso a paso (usando `uv`)

1. **Clonar el repositorio** y moverte al directorio raíz:
   ```bash
   git clone https://github.com/FernandoBRdgz/finguia.git
   cd finguia
   ```
2. **Instalación de dependencias**:
   ```bash
   uv install
   ```

## Configuración de variables de entorno

1. Crea un archivo `.env` en la raíz del proyecto (junto a `pyproject.toml`).
2. Añade estas claves en el archivo:
   ```.env
   OPENAI_API_KEY=sk-...
   ALPHAVANTAGE_API_KEY=XXXXXXXXXXXXXXXX
   ```
3. Evita subir este archivo al repositorio; se recomienda añadirlo a `.gitignore`.

## Cómo tramitar las APIs necesarias

### 1. **OpenAI**

1. Regístrate o inicia sesión en [platform.openai.com](https://platform.openai.com/).
2. Ve a **API Keys** → **Create new secret key**.
3. Copia la clave generada y pégala en tu `.env` como `OPENAI_API_KEY`.
4. Confirma que el modelo `gpt-5.1` (u otro compatible) aparece disponible en tu cuenta y que tienes saldo apropiado.

### 2. **AlphaVantage**

1. Accede a [https://www.alphavantage.co/](https://www.alphavantage.co/).
2. Regístrate con un correo válido y confirma la cuenta.
3. Copia la clave de API que te proveen y agrégala a `.env` como `ALPHAVANTAGE_API_KEY`.
4. Consulta los límites comerciales de la cuenta gratuita para evitar bloquear las solicitudes.

## Ejecución del aplicativo con `uv run`

1. **Preparar el entorno** (solo si es la primera vez):
   ```bash
   uv sync
   ```
2. **Ejecutar la aplicación Streamlit**:
   ```bash
   uv run streamlit run main_07.py
   ```
   Este comando:
   - Lanza `uv` y activa el entorno virtual definido por `pyproject.toml`.
   - Ejecuta `streamlit run main_07.py`.

3. El servidor quedará expuesto en `http://localhost:8501` por defecto; abre esa URL en el navegador.

## Flujo típico después de poner en marcha la app

1. **Interactuar con el chat**: Escribe texto o graba audio en la barra lateral.
2. **Herramientas disponibles**:
   - `get_intrinsic_value`
   - `get_income_statement`
   - `get_balance_sheet`
   - `get_cashflow_statement`
   - `get_earnings`
   - `get_call_transcripts`
   El LLM decide cuándo invocarlas de forma autónoma en base a la conversación; los resultados aparecen como mensajes del asistente.

3. **Conversaciones enriquecidas**: Cada respuesta incluye generación de audio (OpenAI TTS) y anexos si la herramienta lo requiere.

## Consideraciones adicionales

- Recomendamos mantener actualizado `uv`, `streamlit` y `openai` para aprovechar correcciones y nuevas funciones.
- Si estás detrás de un firewall, asegúrate de permitir conexiones salientes hacia `api.openai.com` y `www.alphavantage.co`.
- Para pruebas locales, puedes desactivar temporalmente el uso de audio comentando el bloque correspondiente en `main_07.py`.