# Arquitectura — Residente

## Piezas

1. **Sitio público (`astro.residente.mx`)**  
   Astro SSR + islas React. SEO, páginas dinámicas, PWA, widget/chat.

2. **Admin (`admin.residente.mx`)**  
   React + Vite. Dashboard por roles (admin, B2B, vendedor, colaborador…).  
   Formularios, contenidos, métricas, SEO con Gemini, auditoría del chatbot.

3. **API (`react.residente.mx-prueba`)**  
   Express: monolito + microservicios (restaurantes, notas, pagos, usuarios, chatbot, etc.).  
   Sequelize + MySQL/MariaDB. JWT + roles. Stripe. Docker.

## Flujo típico de un cambio

```text
Requerimiento interno
  → reproducir en UI
  → ver request REST (status/body)
  → revisar query/modelo SQL y permisos
  → fix en la capa correcta
  → prueba
  → producción
```

## Auth

- Cookie/JWT compartido en dominio `.residente.mx`
- Rutas protegidas por rol en API y UI

## Infra (alto nivel)

- Linux/Ubuntu + Plesk
- Nginx como gateway
- Cloudflare
- Contenedores Docker (API, chatbot, Qdrant, Ollama, reranker…)
- CI/CD con GitHub Actions
