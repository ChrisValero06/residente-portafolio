# RAG — Asistente Resi

## Objetivo

Responder preguntas de usuarios con **datos reales** del catálogo (restaurantes, notas, cupones, eventos, recetas), no con texto inventado.

## Pipeline

```text
Pregunta del usuario
  → extractIntent (reglas: zona, precio, categoría…)
  → retrieval híbrido
       • filtros / SQL
       • Fuse.js (fuzzy)
       • Qdrant (vectores)
  → fusión RRF
  → reranker BGE
  → prompt con contexto
  → LLM (Gemini o DeepSeek) + streaming SSE
  → UI Astro (chat widget / Resi / B2B)
```

## Roles de cada pieza

| Pieza | Para qué |
|-------|----------|
| **Ollama** | Embeddings locales (`nomic-embed-text`) al indexar |
| **Qdrant** | Guardar vectores y buscar por similitud |
| **MySQL** | Datos estructurados de negocio |
| **Reranker** | Reordenar candidatos antes del LLM |
| **LLM** | Generar la respuesta final con el contexto recuperado |

## Operación

- Reindexación (cron + hooks al crear/editar contenido)
- Ingest de documentos B2B a Qdrant
- Panel de auditoría/feedback en admin

## Lo que no es (honestidad técnica)

- No es MCP de producto
- No es function calling nativo del modelo (el intent va por heurísticas)
- No es un framework de agents: es un **pipeline RAG determinista** listo para evolucionar a agentes con tools
