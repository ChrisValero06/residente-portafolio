# Residente — Case Study / Portafolio

**Christopher Valero** · Full Stack & IA aplicada · Monterrey, N.L.  
Contacto: christophervalero05@hotmail.com · GitHub: [ChrisValero06](https://github.com/ChrisValero06)

> Case study de una plataforma web **en producción** (`residente.mx`): sitio público, admin y API.  
> El código completo pertenece a la empresa y vive en repos privados/de organización. Aquí documento **mi rol, arquitectura y resultados** para entrevistas.

---

## Qué es Residente

Plataforma editorial/gastronómica con:

- Sitio público (SSR)
- Dashboard admin (roles, contenidos, B2B, pagos)
- Backend REST (monolito + microservicios)
- Asistente de IA (**Resi**) con RAG sobre datos reales
- Automatización SEO con Gemini

---

## Mi rol

Único responsable técnico en periodos clave: tomar requerimientos internos, reproducir bugs, implementar cambios de punta a punta (UI → API → SQL → deploy) y dejarlos en producción.

También diseñé/implementé piezas de IA:

- Chatbot **Resi** (RAG híbrido)
- SEO asistido por Gemini en el admin
- Desarrollo asistido con Cursor / Claude (con revisión humana antes de subir)

---

## Stack

| Capa | Tecnología |
|------|------------|
| Sitio público | Astro (SSR) + React + TypeScript + Tailwind |
| Admin | React + Vite + Tailwind |
| API | Node.js + Express + Sequelize |
| Base de datos | MySQL / MariaDB (+ Redis) |
| IA / RAG | Ollama (embeddings), Qdrant, reranker BGE, LLM Gemini/DeepSeek |
| Infra | Docker, Nginx, Linux/Ubuntu, Plesk, Cloudflare, GitHub Actions |
| Pagos | Stripe |

> En producción el admin/sitio usan **React 19**. La base (hooks, componentes, consumo de APIs) aplica igual a React 18.

---

## Arquitectura (vista rápida)

```text
[Astro SSR + islas React]     [Admin React]
            \                   /
             \                 /
              v               v
           API Gateway / Nginx
                      |
      +---------------+---------------+
      |               |               |
  Monolito REST   Microservicios   Chatbot (RAG)
  (Express)       (pagos, notas…)  + Qdrant + Ollama
                      |
                   MySQL/MariaDB
```

Detalle: [`docs/arquitectura.md`](docs/arquitectura.md) · RAG: [`docs/rag-resi.md`](docs/rag-resi.md)

---

## Qué resolvía en el día a día (tipo “tickets de sistemas”)

1. Reproducir el problema con el usuario interno  
2. Ubicar la capa: pantalla / API / SQL / permisos  
3. Implementar el fix o el cambio pequeño de punta a punta  
4. Probar el caso y casos cercanos  
5. Dejarlo en producción y documentar lo aprendido  

Eso es exactamente el flujo de un rol de sistemas/ERP: **código real que usa la empresa al día siguiente**.

---

## IA en producción (evidencia de enfoque)

### RAG — asistente Resi
- Intent por reglas (zona, precio, categoría…)
- Retrieval híbrido: SQL/filtros + Fuse.js + vectores en **Qdrant**
- Fusión RRF + **reranker BGE**
- Respuesta con **LLM** (Gemini o DeepSeek) en streaming
- Embeddings con **Ollama** (`nomic-embed-text`) + fallback Gemini

### SEO con Gemini
- Desde el admin: títulos, metas, alt text y smart tags para acelerar el flujo editorial

### Cómo uso IA para codear
Contexto → generación → **revisión** → prueba → PR/deploy. No copio ciego.

---

## APIs REST

He **consumido** APIs desde React/Astro y **construido** endpoints en Express:

- Auth JWT + roles
- CRUD de contenidos
- Integraciones (Stripe, chatbot, SEO)
- Respuestas JSON + manejo de errores/status

---

## SQL

Experiencia real con MySQL/MariaDB:

- Lectura de esquemas (PKs, FKs, relaciones)
- Joins para reportes y bugs
- Ajustes/migraciones al agregar campos o reglas
- Integridad de datos en flujos editoriales y B2B

PostgreSQL: misma base relacional; lo adapto rápido en un ERP.

---

## Por qué este repo no tiene el monorepo completo

El código de producción es propiedad de Residente Restaurant Media y está en repositorios de la organización/equipo.

Este portafolio existe para mostrar:

- Qué construí
- Cómo está armado
- Cómo pienso tickets, APIs, SQL e IA

En entrevista puedo profundizar con ejemplos concretos y, con permiso de la empresa, compartir acceso privado o walkthrough del código.

---

## Qué busco

Roles donde:

- Se resuelven tickets/cambios que llegan a producción
- Hay review de PRs y aprendizaje rápido
- Hay camino hacia **agentes de IA** sobre procesos reales (postventa, cobranza, trámites, etc.)

---

## Links

- Producto: [residente.mx](https://residente.mx)
- Este repo: [residente-portafolio](https://github.com/ChrisValero06/residente-portafolio)
