# Teslo Shop

Pequeña tienda demo construida con React + TypeScript y Vite. Está pensada como proyecto de ejemplo con una sección pública (shop), autenticación simple (auth) y un panel de administración (admin). Los datos de productos son _fixtures_ locales en `src/mocks` (no hay backend integrado).

---

## 🔧 Comandos principales

- Instalar dependencias: `npm install`
- Iniciar dev server (Vite): `npm run dev`
- Construir para producción: `npm run build` (ejecuta `tsc -b && vite build`)
- Previsualizar build: `npm run preview`
- Lint (ESLint): `npm run lint`

> Requisito: Node.js moderno (preferible 18+). Vite maneja el bundling y HMR.

---

## Arquitectura y archivos clave

- `src/TesloShopApp.tsx` — Contiene providers globales (React Query `QueryClientProvider` y `ReactQueryDevtools`).
- `src/app.router.tsx` — Rutas principales, con layouts lazy-loaded (`AuthLayout`, `AdminLayout`).
- `src/shop`, `src/auth`, `src/admin` — Carpetas por área funcional (layouts, pages, components).
- `src/components/ui/*` — Componentes UI compartidos (botones, inputs, tablas) usando `class-variance-authority` (`cva`) y la utilidad `cn` en `src/lib/utils.ts`.
- `src/mocks/products.mock.ts` — Datos de producto usados por la tienda (imagen importadas desde `src/assets`).

## Convenciones del proyecto

- Alias `@` → `src` (configurado en `vite.config.ts` y `tsconfig.json`). Usar `@/...` para importaciones internas.
- UI: seguir el patrón `cva` + `cn` para variantes y composición de clases (ej.: `src/components/ui/button.tsx`). Mantener `className` passthrough en nuevos componentes.
- Layouts grandes deben cargarse con lazy-loading en el router para mejorar el bundle inicial.
- Formularios administrativos (ej.: `src/admin/pages/product/AdminProductPage.tsx`) son actualmente controlados con estado local y manejan subida de archivos con `onDrop`/`onChange` (por ahora hacen `console.log` de los ficheros).

---

## Integración de datos / React Query

- React Query ya está inicializado en `TesloShopApp`. Cuando añadas llamadas a datos:
  - Crea un módulo `src/api/*` o `src/lib/api.ts` para encapsular fetchers con `axios`.
  - Añade hooks con `useQuery` / `useMutation` y organiza las keys de cache de forma consistente.

---

## Buenas prácticas al contribuir

- Respeta el patrón de componentes en `src/components/ui` (usa `cva` + `cn`).
- Añade nuevas páginas como hijo del layout apropiado en `app.router.tsx`.
- Ejecuta `npm run lint` antes de crear PRs; seguir las reglas en `eslint.config.js`.

---
