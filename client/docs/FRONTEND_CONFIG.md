# Frontend Config Reference

## Environment Variables

Create `client/.env`:

```
VITE_API_URL=http://localhost:5000/api
```

The Axios instance in `src/utils/api.js` uses `import.meta.env.VITE_API_URL` (falls back to `http://localhost:5000/api`).

## Vite Config (`client/vite.config.js`)

```js
import { defineConfig } from 'vite'
import tailwindcss from '@tailwindcss/vite'

export default defineConfig({
  plugins: [tailwindcss()],
})
```

No proxy is configured. The client hits the server directly. In production, `vercel.json` rewrites `/api/(.*)` to the Express server.

To add a dev proxy (avoids CORS):

```js
server: { proxy: { '/api': 'http://localhost:5000' } }
```

## Scripts

| Command | Action |
|---------|--------|
| `npm run dev` | dev server on :5173 |
| `npm run build` | builds to `dist/` |
| `npm run lint` | ESLint on all JS/JSX |
| `npm run preview` | preview production build |

## Dependencies

| Package | Purpose |
|---------|---------|
| `react` / `react-dom` | UI framework |
| `react-router-dom` | routing |
| `axios` | HTTP client |
| `tailwindcss` / `@tailwindcss/vite` | styling |
| `lucide-react` | icons |
| `react-hot-toast` | notifications |
| `clsx` / `tailwind-merge` | className utilities |

## Adding a New Page

1. Create file in `src/pages/` (or `src/sections/` for page sections)
2. Add route in `src/App.jsx`:
   - Public → `<Route path="/path" element={<YourPage />} />`
   - Protected (logged in) → wrap in `<Route element={<ProtectedRoute />}>`
   - Admin only → wrap in `<Route element={<ProtectedRoute requireAdmin={true} />}>`
3. Import and add the link in `PublicNavbar.jsx` if needed
