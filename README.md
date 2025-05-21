# Next.js Boilerplate: Zustand, TanStack Query, and Supabase Types

This boilerplate provides a modern starting point for Nextjs projects that leverage:

- [**Zustand**](https://zustand.docs.pmnd.rs/) for state management  
- [**TanStack Query**](https://tanstack.com/query/latest/docs/framework/react/overview) for server state/data fetching  
- [**Supabase Types**](https://supabase.com/docs/guides/api/rest/generating-types) for type-safe API integration

---

## ✨ Features

- 🔥 **Minimal setup** with best practices for scalable Nextjs apps  
- ⚡️ **Global state** with Zustand and persistent storage support  
- 👤 Zustand is used for managing the `CurrentUser` global state throughout the app  
- 🚀 **Data fetching**, caching, and mutations with TanStack Query  
  - TanStack Query handles all server-side data fetching and caching
  - Queries are **automatically invalidated** after create/update/delete operations  
- 🔒 **Type-safe API calls** using Supabase-generated types  
- 🧪 Ready for **testing and rapid prototyping**

---

## 🚀 Getting Started

### 1. Install Dependencies

```bash
npm install
# or
yarn install
````

### 2. Set Up Environment Variables

Create a `.env` file with your Supabase credentials:

```env
NEXT_PUBLIC_SUPABASE_URL=your-supabase-url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-supabase-anon-key
```

### 3. Generate Supabase Types

Automatically generate TypeScript types for your Supabase tables:

```bash
npx supabase gen types typescript --project-id "$PROJECT_REF" --schema public > database.types.ts
```

See the [Supabase documentation](https://supabase.com/docs/guides/api/rest/generating-types) for more details.

### 4. Run the App

```bash
npm run dev
# or
yarn dev
```

---

## 📁 Project Structure

```
├── public/
│   └── index.html
├── src/
│   └── app/
│       └── admin/
│       └── auth/
│   └── components/
│   └── hooks/
│   └── lib/
└── middleware.ts
├── .env                      # Environment variables (Supabase keys, etc.)
├── package.json
├── tsconfig.json
├── README.md
```

---

## 🛠️ Usage Examples

### ✅ Zustand Store for `CurrentUser`

```ts
import { useCurrentUserStore } from './store/currentUser';

const currentUser = useCurrentUserStore(state => state.user);
```

### 📡 TanStack Query (with Cache Invalidation)

```ts
import { useQuery, useMutation, useQueryClient } from '@tanstack/react-query';

const queryClient = useQueryClient();

const { data, isLoading } = useQuery(['todos'], fetchTodos);

const mutation = useMutation(createTodo, {
  onSuccess: () => {
    queryClient.invalidateQueries(['todos']); // Invalidate cache on create/update/delete
  },
});
```

### 🔐 Supabase Types

```ts
import { Database, Tables, Enums } from "./database.types.ts";

// Before 😕
let movie: Database['public']['Tables']['movies']['Row'] = // ...

// After 😍
let movie: Tables<'movies'>

```

---

## 📚 Documentation

* Zustand: [https://zustand.docs.pmnd.rs/](https://zustand.docs.pmnd.rs/)
* TanStack Query: [https://tanstack.com/query/latest/docs/framework/react/overview](https://tanstack.com/query/latest/docs/framework/react/overview)
* Supabase Types: [https://supabase.com/docs/guides/api/rest/generating-types](https://supabase.com/docs/guides/api/rest/generating-types)

---
