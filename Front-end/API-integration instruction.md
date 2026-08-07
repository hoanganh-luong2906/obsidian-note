# Template: wiring any REST resource into openapi-fetch + TanStack Query

Generic, copy-pasteable version of
[`api-integration-howto.md`](./api-integration-howto.md). That doc is
CR-specific (real files, real `signals`/`reports` example). This one strips
the domain out so you can reuse the pattern for **any** new resource in this
app, or port the whole stack to a different Next.js + openapi-fetch +
TanStack Query project.

Two things run side by side below: a **placeholder template** (fill in the
blanks) and a **fully worked generic example** using a made-up resource,
`Widget`, so every placeholder has a concrete counterpart to compare against.

---

## Placeholder legend

| Placeholder | Meaning | Example value used below |
| --- | --- | --- |
| `{Domain}` | PascalCase resource name | `Widget` |
| `{domain}` | camelCase resource name | `widget` |
| `{domains}` | camelCase plural | `widgets` |
| `{ID_PARAM}` | backend's path param name for one item | `widget_id` |
| `{BASE_PATH}` | REST collection path | `/api/widgets` |
| `{ITEM_PATH}` | REST item path | `/api/widgets/{widget_id}` |

---

## The layer stack (project-agnostic)

```
generated-schema.ts              ← types generated from the backend's OpenAPI spec
  ↓
lib/api/client.ts                ← ONE openapi-fetch instance (shared, with interceptors)
  ↓
lib/api/{domain}.ts              ← domain module: plain async functions, throw on error
  ↓
lib/hooks/use-{domain}.ts        ← useQuery/useMutation wrapper + {domain}Keys factory
  ↓
lib/api/queries.ts               ← barrel re-export
  ↓
components/*                     ← import hooks ONLY from the barrel
```

The rule that makes this reusable: **each layer only talks to the layer
directly below it.** A component never imports `apiClient`. A domain module
never imports `useQuery`. That's the whole pattern — everything else below
is just what falls out of applying it consistently.

---

## Step 1 — Generate types from the OpenAPI spec

One-time per project setup (`openapi-typescript`), regenerated whenever the
backend spec changes:

```bash
npx openapi-typescript https://your-backend/openapi.json -o src/generated-schema.ts
```

Never hand-edit the output file. If a route/shape is missing, regenerate
against a backend that serves it — don't patch the generated file.

## Step 2 — Types — `lib/types/{domain}.ts`

**Template:**

```ts
import { components } from '@/src/generated-schema';

export type {Domain} = components['schemas']['{Domain}'];
export type {Domain}ListItem = components['schemas']['{Domain}ListItem'];

// Only hand-declare what has no backend schema counterpart
// (query params, UI-only view models).
export interface {Domain}ListQuery {
  status?: string;
  cursor?: string | null;
  limit?: number;
}
```

**Worked example (`lib/types/widget.ts`):**

```ts
import { components } from '@/src/generated-schema';

export type Widget = components['schemas']['Widget'];
export type WidgetListItem = components['schemas']['WidgetListItem'];

export interface WidgetListQuery {
  status?: 'active' | 'archived';
  cursor?: string | null;
  limit?: number;
}
```

Rule of thumb: if the backend already models it, derive it from
`components['schemas']`. If it exists only on the frontend (filters, tab
state, a computed view model), it's a legitimate hand-written `interface`.

## Step 3 — Domain API module — `lib/api/{domain}.ts`

**Template:**

```ts
import { apiClient } from './client';
import { apiErrorMessage } from './errors';
import type { {Domain}, {Domain}ListItem, {Domain}ListQuery } from '@/src/lib/types/{domain}';

export const {domain}Api = {
  async list(params: {Domain}ListQuery = {}) {
    const { data, error } = await apiClient.GET('{BASE_PATH}', {
      params: { query: params as Record<string, unknown> },
    });
    if (error) throw new Error('Failed to fetch {domains}');
    return data as unknown as { items: {Domain}ListItem[]; total: number; has_more: boolean; next_cursor?: string | null };
  },

  async getById(id: string): Promise<{Domain}> {
    const { data, error } = await apiClient.GET('{ITEM_PATH}', {
      params: { path: { {ID_PARAM}: id } },
    });
    if (error) throw new Error('Failed to fetch {domain}');
    return data as unknown as {Domain};
  },

  async update(id: string, body: Partial<{Domain}>): Promise<{Domain}> {
    const { data, error } = await apiClient.PUT('{ITEM_PATH}', {
      params: { path: { {ID_PARAM}: id } },
      body,
    });
    if (error) throw new Error(apiErrorMessage(error, 'Failed to update {domain}'));
    return data as unknown as {Domain};
  },
};
```

**Worked example (`lib/api/widgets.ts`):**

```ts
import { apiClient } from './client';
import { apiErrorMessage } from './errors';
import type { Widget, WidgetListItem, WidgetListQuery } from '@/src/lib/types/widget';

export const widgetsApi = {
  async list(params: WidgetListQuery = {}) {
    const { data, error } = await apiClient.GET('/api/widgets', {
      params: { query: params as Record<string, unknown> },
    });
    if (error) throw new Error('Failed to fetch widgets');
    return data as unknown as { items: WidgetListItem[]; total: number; has_more: boolean; next_cursor?: string | null };
  },

  async getById(id: string): Promise<Widget> {
    const { data, error } = await apiClient.GET('/api/widgets/{widget_id}', {
      params: { path: { widget_id: id } },
    });
    if (error) throw new Error('Failed to fetch widget');
    return data as unknown as Widget;
  },

  async update(id: string, body: Partial<Widget>): Promise<Widget> {
    const { data, error } = await apiClient.PUT('/api/widgets/{widget_id}', {
      params: { path: { widget_id: id } },
      body,
    });
    if (error) throw new Error(apiErrorMessage(error, 'Failed to update widget'));
    return data as unknown as Widget;
  },
};
```

Rules that generalize across any project using this client:
- Path strings passed to `apiClient.GET/POST/PUT/DELETE` must be the
  **literal** OpenAPI path (`'/api/widgets/{widget_id}'`), not a template
  literal you interpolate yourself — that literal is what lets the client
  infer param/response types.
- Every method **throws** on `{error}` and returns the unwrapped success
  type. Nothing above this layer ever sees `{data, error}`.
- Reserve a "translate backend error body → readable string" helper (like
  `apiErrorMessage`) for mutations where the failure reason is
  user-facing (validation errors, business-rule rejections). Reads that
  only need a generic failure string can throw a fixed message.

## Step 4 — Hook — `lib/hooks/use-{domain}.ts`

**Template:**

```ts
import { useMutation, useQuery, useQueryClient } from '@tanstack/react-query';
import { {domain}Api } from '../api/{domain}';

export const {domain}Keys = {
  all: ['{domains}'] as const,
  list: (query: {Domain}ListQuery) => ['{domains}', 'list', query] as const,
  detail: (id: string | null) => ['{domains}', 'detail', id] as const,
};

export function use{Domain}Query(id: string | null) {
  return useQuery({
    queryKey: {domain}Keys.detail(id),
    queryFn: () => {domain}Api.getById(id!),
    enabled: id !== null,
  });
}

export function useUpdate{Domain}Mutation() {
  const queryClient = useQueryClient();
  return useMutation({
    mutationFn: ({ id, body }: { id: string; body: Partial<{Domain}> }) => {domain}Api.update(id, body),
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: {domain}Keys.all });
    },
  });
}
```

**Worked example (`lib/hooks/use-widgets.ts`):**

```ts
import { useMutation, useQuery, useQueryClient } from '@tanstack/react-query';
import { widgetsApi } from '../api/widgets';
import type { Widget, WidgetListQuery } from '@/src/lib/types/widget';

export const widgetKeys = {
  all: ['widgets'] as const,
  list: (query: WidgetListQuery) => ['widgets', 'list', query] as const,
  detail: (id: string | null) => ['widgets', 'detail', id] as const,
};

export function useWidgetQuery(id: string | null) {
  return useQuery({
    queryKey: widgetKeys.detail(id),
    queryFn: () => widgetsApi.getById(id!),
    enabled: id !== null,
  });
}

export function useUpdateWidgetMutation() {
  const queryClient = useQueryClient();
  return useMutation({
    mutationFn: ({ id, body }: { id: string; body: Partial<Widget> }) => widgetsApi.update(id, body),
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: widgetKeys.all });
    },
  });
}
```

**Cursor-paginated list variant** (any endpoint shaped
`{ items, total, limit, has_more, next_cursor }`) — write ONE generic
`useCursorInfiniteQuery<TItem, TParams>` wrapper over `useInfiniteQuery` per
project, then reuse it for every paginated resource instead of hand-rolling
`useInfiniteQuery` per domain:

```ts
// lib/hooks/use-cursor-infinite-query.ts — write once, reuse everywhere
export function useCursorInfiniteQuery<TItem, TParams extends { cursor?: string | null }>(opts: {
  queryKey: readonly unknown[];
  queryFn: (params: TParams) => Promise<{ items: TItem[]; total: number; has_more: boolean; next_cursor?: string | null }>;
  params: Omit<TParams, 'cursor'>;
}) {
  const query = useInfiniteQuery({
    queryKey: opts.queryKey,
    queryFn: ({ pageParam }: { pageParam: string | null }) =>
      opts.queryFn({ ...opts.params, cursor: pageParam } as TParams),
    initialPageParam: null as string | null,
    getNextPageParam: (last) => (last.has_more && last.next_cursor ? last.next_cursor : undefined),
  });
  return {
    items: query.data?.pages.flatMap((p) => p.items) ?? [],
    hasNextPage: query.hasNextPage,
    fetchNextPage: () => void query.fetchNextPage(),
    isFetchingNextPage: query.isFetchingNextPage,
    isPending: query.isPending,
    isError: query.isError,
  };
}

// per-domain usage — no useInfiniteQuery plumbing repeated
export function useWidgetListQuery(query: Omit<WidgetListQuery, 'cursor'>) {
  return useCursorInfiniteQuery<WidgetListItem, WidgetListQuery>({
    queryKey: widgetKeys.list(query),
    queryFn: (params) => widgetsApi.list(params),
    params: query,
  });
}
```

Pair any infinite list with a **generic** "load more when visible" hook
(`IntersectionObserver` on a sentinel `<div>`), written once:

```ts
export function useLoadMoreOnVisible(onVisible: () => void, enabled: boolean) {
  const ref = useRef<HTMLDivElement>(null);
  useEffect(() => {
    if (!enabled || !ref.current) return;
    const observer = new IntersectionObserver(([entry]) => entry.isIntersecting && onVisible(), { rootMargin: '200px' });
    observer.observe(ref.current);
    return () => observer.disconnect();
  }, [enabled, onVisible]);
  return ref;
}
```

## Step 5 — Barrel re-export

```ts
// lib/api/queries.ts
export * from '../hooks/use-{domain}';
```

Components import only from this barrel — never reach into
`lib/hooks/use-{domain}` directly. This is what lets you refactor a hook's
internals (swap `useQuery` for `useSuspenseQuery`, change the key shape)
without touching every call site.

## Step 6 — Consume in a component

```tsx
import { use{Domain}Query, useUpdate{Domain}Mutation } from '@/src/lib/api/queries';

function {Domain}Panel({ id }: { id: string }) {
  const { data, isPending, isError } = use{Domain}Query(id);
  const update = useUpdate{Domain}Mutation();

  if (isPending) return <LoadingSkeleton />;
  if (isError) return <ErrorState />;
  if (!data) return <EmptyState />;

  return <button onClick={() => update.mutate({ id, body: { status: 'archived' } })}>Archive</button>;
}
```

Loading / error / empty as an explicit early-return branch, not a nested
ternary — this generalizes to any component consuming server state,
regardless of resource.

## Step 7 — The shared plumbing every domain module leans on

Write these **once per project**, not once per domain:

**`lib/api/client.ts`** — a single `openapi-fetch` instance with two
middleware hooks:

```ts
import createClient from 'openapi-fetch';
import type { paths } from '@/src/generated-schema';

export const apiClient = createClient<paths>({ baseUrl: '' });

apiClient.use({
  async onRequest({ request }) {
    const token = await getAuthToken(); // however your app gets one
    if (token) request.headers.set('Authorization', `Bearer ${token}`);
    return request;
  },
  async onResponse({ response }) {
    if (response.ok) return response;
    const body = await response.clone().json().catch(() => null);
    const error = new Error(body?.message ?? 'Request failed') as Error & { status?: number; data?: unknown };
    error.status = response.status;
    error.data = body;
    throw error;
  },
});
```

**`lib/api/errors.ts`** — one function that knows your backend's error
shape (adjust the field names to match yours: FastAPI uses `detail`,
NestJS/Express commonly use `message`):

```ts
export function apiErrorMessage(error: unknown, fallback: string): string {
  if (error && typeof error === 'object' && 'detail' in error) {
    const { detail } = error as { detail: unknown };
    if (typeof detail === 'string' && detail.trim()) return detail;
  }
  return fallback;
}
```

Why `baseUrl: ''`: if your Next.js app proxies API calls through its own
route handlers (`app/api/[...path]/route.ts` → real backend), same-origin
requests let that proxy attach auth/headers server-side and keep the real
backend host out of client code. If you call the backend directly
cross-origin instead, set `baseUrl` to that origin and handle CORS/auth
there — the pattern still holds, only this one config line changes.

---

## Testing template

Mock the client, not `fetch` — one layer above the transport:

```ts
const mockGET = jest.fn();
jest.mock('@/src/lib/api/client', () => ({
  apiClient: { GET: (...a: unknown[]) => mockGET(...a) },
}));

it('throws a readable message on failure', async () => {
  mockGET.mockResolvedValue({ data: null, error: { detail: 'Widget not found' } });
  await expect(widgetsApi.getById('w-1')).rejects.toThrow(/Widget not found|Failed to fetch widget/);
});
```

---

## Checklist (generic)

- [ ] Types derived from `components['schemas']`, no hand-rolled duplicates of backend shapes
- [ ] Domain module throws `Error` on `{error}`, returns the unwrapped success type
- [ ] Hook has a `{domain}Keys` factory; paginated lists reuse the one generic cursor-pagination hook
- [ ] Mutations invalidate the domain-wide key, not just the narrow one that changed
- [ ] Re-exported from the barrel; components import only from there
- [ ] Loading/error/empty handled as explicit branches
- [ ] Test mocks the client module, not `fetch`
- [ ] No second `apiClient` instance created anywhere

Concrete, CR-specific version of all of this: [`api-integration-howto.md`](./api-integration-howto.md).
Full architecture rationale: [`frontend-design-patterns.md`](./frontend-design-patterns.md).
