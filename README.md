# Hackathon 1: Asistente inteligente con Llama

Asistente para identificación morfológica de mosquitos de importancia médica desarrollado como proyecto del Módulo 1 de **IA Aplicada a Modelos Abiertos**.

## Objetivo

Construir un asistente basado en Llama que guíe la identificación morfológica de hembras adultas mediante preguntas sucesivas sobre caracteres diagnósticos.

El alcance se restringe a cuatro taxones:

- *Aedes aegypti*
- *Aedes albopictus*
- complejo *Anopheles gambiae*
- *Culex pipiens* sensu lato

## Arquitectura

El asistente integra tres componentes:

- **LoRA:** interpreta respuestas del usuario escritas en lenguaje natural.
- **Motor taxonómico:** controla la identificación mediante reglas explícitas.
- **RAG:** recupera evidencia científica asociada al resultado taxonómico.

Las respuestas explícitas (`si`, `no` y `no_observable`) se envían directamente al motor de reglas. Cuando LoRA interpreta una respuesta libre, su predicción debe ser confirmada por el usuario antes de modificar la ruta de identificación.

## Ajuste del modelo

Se utiliza `TinyLlama/TinyLlama-1.1B-Chat-v1.0` y ajuste supervisado mediante LoRA.

En la ejecución final validada:

| Modelo | Exactitud |
|---|---:|
| Modelo base | 0.00 % |
| Modelo ajustado con LoRA | 75.00 % |

La mejora absoluta observada fue de **75 puntos porcentuales** sobre un conjunto final independiente de 12 respuestas.

El modelo ajustado todavía presentó errores, por lo que LoRA no toma directamente decisiones taxonómicas.

## Ejecución

El proyecto está contenido en el notebook:

`Hackathon_1_Asistente_inteligente_con_Llama.ipynb`

Para ejecutarlo en Google Colab se requiere configurar un Secret denominado:

`HF_TOKEN`

con un token válido de Hugging Face y ejecutar el notebook secuencialmente.

## Fuentes científicas

La clave morfológica y la base RAG se construyeron a partir de Huang (2001), Rueda (2004), Coetzee (2020) y Ferreira-de-Freitas et al. (2020). Las referencias completas se encuentran dentro del notebook.
