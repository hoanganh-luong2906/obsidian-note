# Frontend Design Patterns & Conventions

  

Onboarding reference for the Competitive Radar (CR 2.1) frontend. Everything

below was verified directly against the current codebase (not assumed from

templates or generic Next.js/React best practice) as of 2026-08-05. Where a

convention is documented elsewhere but the code has since diverged, that is

called out explicitly in [Known documentation drift](#known-documentation-drift)

so you don't get misled by a stale doc.

  

Read this alongside the repo root `CLAUDE.md` (domain concepts, delivery

phases, branch/PR workflow) — this doc is scoped to **how the frontend code

itself is organized and written**, not product/domain rules.

  

---

  

## 1. Tech stack at a glance

  

| Concern | Choice | Notes |

|---|---|---|

| Framework | **Next.js 16.2** (App Router) | Has breaking changes vs. training-data Next.js. Read `node_modules/next/dist/docs/01-app` before touching routing/layout code — see `frontend/AGENTS.md`. |

| UI runtime | **React 19.2** | |

| Styling | **Tailwind CSS v4** | CSS-first config — no `tailwind.config.ts`. All tokens live in `app/globals.css`. |

| Components | **shadcn/ui**, style `new-york` | Copy-in Radix primitives in `src/components/ui/`. Config: `components.json`. Icons: `lucide-react`. |

| Server state | **TanStack Query v5** (`@tanstack/react-query`) | Configured in `app/providers.tsx`. |

| HTTP client | **openapi-fetch** | Fully typed from `src/generated-schema.ts`. |

| Auth | **MSAL** (`@azure/msal-browser`, `@azure/msal-react`) | Azure AD / Entra ID. |

| Dates | **dayjs** (+ `relativeTime` plugin) | |

| Charts | **recharts** | |

| Validation | **zod** | Form schemas (e.g. add/update competitor). |

| Class merging | **clsx** + **tailwind-merge** via `cn()` | `src/lib/utils.ts` |

| Unit/component tests | **Jest** (`next/jest`) + **React Testing Library** | |

| E2E + visual | **Playwright** | |

| Package manager | **pnpm** (`pnpm@11.13.0` pinned in `package.json`) | Never use npm/yarn — `pnpm-lock.yaml` is committed. |

  

---

  

## 2. Directory structure (annotated, real paths)

  

```

frontend/

├── app/                              # Next.js App Router — routes & layouts only

│   ├── layout.tsx                    # Root layout: fonts, <Providers>, globals.css import

│   ├── providers.tsx                 # Client providers: QueryClient, Auth, SessionExpired, Toaster

│   ├── globals.css                   # Tailwind v4 CSS-first config + design tokens

│   ├── page.tsx                      # `/` route

│   ├── not-found.tsx

│   ├── login/page.tsx

│   ├── account-not-registered/page.tsx

│   ├── api/[...path]/route.ts        # Catch-all proxy → backend API (see §7.1)

│   └── (private)/                    # Route group: authenticated app shell

│       ├── layout.tsx                # Sidebar + top bar + RequireAuth gate

│       ├── constants/

│       ├── radar-signals/

│       │   ├── page.tsx

│       │   └── components/           # Route-local components (NOT in src/components)

│       │       ├── kpi-strip.tsx

│       │       ├── signal-heatmap.tsx

│       │       ├── source-breakdown.tsx

│       │       ├── active-competitors.tsx

│       │       ├── group-signal-dialog/

│       │       │   ├── index.tsx

│       │       │   └── target-row.tsx

│       │       └── signal-feed/       # Deeply-nested feature folder

│       │           ├── index.tsx      # Owns state, composes the rest

│       │           ├── hooks.ts       # Route-local hooks (NOT re-exported globally)

│       │           ├── signal-card.tsx

│       │           ├── signal-card-skeleton.tsx

│       │           ├── signal-status-select.tsx

│       │           ├── dismiss-reason-dialog.tsx

│       │           ├── feed-tabs.tsx

│       │           ├── feed-error.tsx

│       │           └── group-signal-card.tsx

│       ├── brand-atlas/

│       │   ├── page.tsx

│       │   ├── loading.tsx

│       │   └── components/

│       ├── configuration/

│       │   ├── page.tsx

│       │   ├── configuration-mocks.ts

│       │   └── components/

│       │       └── alerts-settings/

│       └── components/                # Shared *within* the (private) group, cross-route

│           ├── signal-details/         # Signal Detail slide-over panel (used by radar feed + brand atlas)

│           │   ├── index.tsx

│           │   ├── sections/

│           │   ├── constants.ts

│           │   └── format.ts

│           ├── unmatched-cta/

│           └── add-update-competitor/

│               └── hooks/

├── src/

│   ├── generated-schema.ts           # ⛔ AUTO-GENERATED — never hand-edit (see §8)

│   ├── codegen.mjs                    # Regenerates generated-schema.ts from backend OpenAPI

│   ├── components/                    # Global, route-agnostic components

│   │   ├── ui/                        # shadcn primitives (button, card, dialog, select, …)

│   │   ├── common/                    # App-specific but reusable: empty-state, confirm-dialog,

│   │   │                              #   market-tag, image-with-fallback, tab-switcher

│   │   ├── layout/                    # App shell: app-sidebar, top-bar, page-title, global-search

│   │   ├── icons/                     # Custom SVG icons with no lucide equivalent

│   │   └── auth/                      # session-expired-provider

│   ├── lib/

│   │   ├── api/                       # Layer 2: domain API modules (see §7)

│   │   │   ├── client.ts              # Single openapi-fetch instance + auth/error interceptors

│   │   │   ├── errors.ts              # apiErrorMessage() — FastAPI error body → string

│   │   │   ├── signals.ts, atlas.ts, groups.ts, competitors.ts, alerts.ts, insights.ts, search.ts, users.ts

│   │   │   └── queries.ts             # Layer 4 barrel — re-exports all hooks (import from here)

│   │   ├── hooks/                     # Layer 3: TanStack Query hooks

│   │   │   ├── use-signals.ts, use-atlas.ts, use-competitors.ts, use-groups.ts, use-insights.ts,

│   │   │   │   use-alerts.ts, use-search.ts, use-users.ts

│   │   │   ├── use-cursor-infinite-query.ts   # Generic cursor-pagination wrapper over useInfiniteQuery

│   │   │   ├── use-load-more-on-visible.ts    # IntersectionObserver "load more" sentinel

│   │   │   ├── use-filter-state.ts            # URL ⇄ sessionStorage filter sync (feature pattern reference)

│   │   │   ├── use-permission.tsx             # RBAC: Role/Permission enums, useAuthorize, PermissionGate

│   │   │   └── use-url-tab.ts

│   │   ├── auth/                      # msal.ts, use-auth.tsx, require-auth.tsx

│   │   ├── types/                     # signal.ts, atlas.ts, pagination.ts — schema-derived types (see §8)

│   │   ├── unmatched/                 # cta-seed.ts

│   │   ├── feed.ts                    # Pure client-side feed helpers (filterByTab, tabCounts)

│   │   └── utils.ts                   # cn(), date/format helpers, label maps

│   ├── e2e/                            # Playwright specs + visual snapshot baselines

│   │   ├── *.spec.ts

│   │   └── *.spec.ts-snapshots/

│   └── docs/

│       ├── tech-stack.md

│       └── routes/                     # Per-route technical docs (older set)

├── docs/

│   ├── routes/                         # Per-route technical docs (newer set — see §11)

│   └── design-pattern/                 # ← this document

├── __tests__/                          # ALL Jest/RTL tests — flat, not colocated (see §10.1)

├── components.json                     # shadcn/ui config

├── eslint.config.mjs                   # ESLint flat config (+ Stylistic — see §9)

├── jest.config.ts

├── playwright.config.ts

├── tsconfig.json                       # `@/*` → repo root

└── package.json

```

  

**The two-tree component split is the single most important structural fact

to internalize:**

  

1. **`src/components/`** — global, reusable, route-agnostic (`ui/`, `common/`,

   `layout/`, `icons/`, `auth/`). Import via `@/src/components/...`.

2. **`app/(private)/<route>/components/`** — feature/route-local. Lives next

   to the `page.tsx` that owns it. Import via `@/app/(private)/<route>/components/...`.

   A component only gets promoted to `src/components/common/` once a second

   route needs it (e.g. `EmptyState`, `MarketTag`).

  

There is a **third tier**: `app/(private)/components/` (no route segment) —

shared across routes *within* the private group but not global enough for

`src/components/` (e.g. `signal-details/`, the Signal Detail panel, is used

by both Radar Feed and Brand Atlas).

  

---

  

## 3. Naming conventions

  

Verified from the actual file listing — these are consistent, not aspirational:

  

- **Files**: kebab-case for everything — `signal-card.tsx`, `use-cursor-infinite-query.ts`, `use-filter-state.ts`. No PascalCase or camelCase filenames anywhere in `src/` or `app/`.

- **Components**: PascalCase export, matching the file's subject — `signal-card.tsx` exports `SignalCard`.

- **Feature folders with multiple files**: an `index.tsx` as the folder's public entry point (`group-signal-dialog/index.tsx`, `signal-details/index.tsx`, `unmatched-cta/index.tsx`, `add-update-competitor/index.tsx`). Import the folder, not the file: `@/app/(private)/components/signal-details` (see `signal-feed/index.tsx` line 3).

- **Hooks**: `use-*.ts`/`use-*.tsx`, exporting a `use*` camelCase function — file and export name always align (`use-permission.tsx` → `usePermission`, `useAuthorize`, `PermissionGate`).

- **Query key factories**: one `{domain}Keys` object per hook module, colocated with the hooks that use it — `signalKeys` in `use-signals.ts`, `atlasKeys` in `use-atlas.ts`. Never inline ad-hoc key arrays in components.

- **Types**: PascalCase, always re-derived from `components['schemas'][...]` when a backend shape exists (§8).

- **Constants**: SCREAMING_SNAKE_CASE for true constants (`SESSION_KEY`, `NULL_BODY_STATUSES`), PascalCase-suffix `_TABS`/`_STATUS` for typed lookup tables (`FEED_TABS`, `TAB_STATUS`, `ROLE_PERMISSIONS`, `ROLE_LABELS`).

- **Test files**: `<subject>.test.ts(x)`, always under `__tests__/` at the frontend root — see §10.1.

  

---

  

## 4. Routing (App Router)

  

- **Route groups**: `(private)` wraps every authenticated route. It does not

  appear in the URL. `app/(private)/layout.tsx` renders `RequireAuth` →

  `PageTitleProvider` → sidebar/top-bar shell → `{children}`.

- **Public routes** live directly under `app/`: `/login`, `/account-not-registered`, `/` (root — actually a thin redirect/landing, distinct from the (private) radar-signals page).

- **API proxy route**: `app/api/[...path]/route.ts` is a catch-all that

  forwards every method (GET/POST/PUT/PATCH/DELETE) to `process.env.API_URI`,

  stripping hop-by-hop and `x-*` headers, streaming the body through

  (`duplex: 'half'` for streamed request bodies), and special-casing 204/205/304

  as null-body responses. **This is why `apiClient` in `src/lib/api/client.ts`

  uses `baseUrl: ''`** — every request goes to the same origin, and this route

  relays it server-side. Never call the backend directly from the browser.

- **Client vs Server Components**: default to Server Components; a file gets

  `'use client'` only when it's interactive or touches browser-only APIs

  (hooks, event handlers, `sessionStorage`, `IntersectionObserver`,

  `next/navigation` hooks). Every hook, every provider, and every

  interactive leaf component in this codebase carries `'use client'` as its

  first line — verify this is still true before assuming a new file needs it.

- **URL as state**: filters, active tab, and the selected signal id (`?signal_id=`)

  all live in the URL via `useSearchParams`/`usePathname`, not local

  component state alone. See §6.3 for why `history.pushState` is used

  directly instead of `router.push` in one specific case.

  

---

  

## 5. Component patterns

  

### 5.1 Composition over configuration

  

`SignalFeed` (`app/(private)/radar-signals/components/signal-feed/index.tsx`)

is the reference "owner" component: it holds no rendering logic of its own

beyond branching on `loading`/`error`/`empty`/`loaded`, and composes ~8

child components/hooks, each responsible for one slice (tabs, detail panel,

group dialog, unmatched-CTA host, card, skeleton, error, empty). Copy this

shape for any new feed/list-like feature:

  

```

FeatureRoot (index.tsx)

 ├─ useXFilters()        — URL-derived filter/tab state

 ├─ useSelectedXId()     — URL-derived selection state

 ├─ useXQuery(...)       — TanStack Query data

 ├─ useLoadMoreOnVisible — infinite-scroll sentinel, if paginated

 └─ renders: Tabs | Error | Skeleton×N | EmptyState | Card[] | DetailPanel | Dialogs

```

  

### 5.2 `Readonly<Props>` on every component

  

Every component signature in this codebase wraps its props type in

`Readonly<...>` — `SignalCard({ signal, ... }: Readonly<SignalCardProps>)`,

`RootLayout({ children }: Readonly<{ children: React.ReactNode }>)`. Follow

this even for trivial components; it's not optional stylistic noise, it's

applied uniformly.

  

### 5.3 Loading / error / empty as an explicit branch, not nested ternaries

  

`SignalFeed` computes a single `feedBody: React.ReactNode` via sequential

`if`/`else if` (error → loading → empty → loaded), assigned once, rendered

once at the bottom. Prefer this over inlining three-way ternaries in JSX —

it keeps each branch readable and testable in isolation.

  

### 5.4 `data-testid` on the elements tests actually assert against

  

Not sprinkled everywhere — only on the nodes a test needs to select

unambiguously (`data-testid="signal-card"`, `"signal-title"`,

`"signal-score"`, `"signal-segment"`, `"feed-empty"`). Text content

(`getByText`, `getByRole`) is preferred first; `data-testid` is the fallback

for nodes with no unique accessible text.

  

### 5.5 Local-only vs. globally re-exported hooks

  

`signal-feed/hooks.ts` (`useSelectedSignalId`, `useFeedFilters`, `useGroupingFlow`)

is **not** re-exported through `src/lib/api/queries.ts` — it's UI-state, not

server-state, and it's specific to this one feature. Only put a hook in

`src/lib/hooks/` + the `queries.ts` barrel if it wraps TanStack Query and is

(or plausibly will be) used by more than one route.

  

---

  

## 6. State management

  

### 6.1 Server state — TanStack Query, always through the layer stack

  

Never call `fetch`/`apiClient` directly from a component. The stack (bottom

to top) is:

  

```

generated-schema.ts        ← OpenAPI-generated types: paths, components, operations

  ↓

lib/api/client.ts           ← one openapi-fetch instance (auth header + 401/error interceptor)

  ↓

lib/api/{domain}.ts         ← domain module: signalsApi.list(), signalsApi.advance(id), ...

  ↓

lib/hooks/use-{domain}.ts   ← useQuery/useMutation wrapper + {domain}Keys factory

  ↓

lib/api/queries.ts          ← barrel: `export * from '../hooks/use-signals'` etc.

```

  

Components import **only from the barrel**: `import { useSignalFeedQuery } from '@/src/lib/api/queries'`.

  

Concrete example, `signalsApi.advance` → `useUpdateSignalStatus`:

  

```ts

// lib/api/signals.ts

async advance(id: string): Promise<SignalListSingle> {

  const { data, error } = await apiClient.POST('/api/signals/{signal_id}/advance', {

    params: { path: { signal_id: id } },

  });

  if (error) throw new Error(apiErrorMessage(error, 'Failed to advance signal'));

  return data as unknown as SignalListSingle;

}

  

// lib/hooks/use-signals.ts

export function useUpdateSignalStatus() {

  const queryClient = useQueryClient();

  return useMutation({

    mutationFn: transition,               // routes to advance/restore/dismiss by `to`

    onSuccess: (_signal, vars) => {

      queryClient.invalidateQueries({ queryKey: signalKeys.all });

      toast.success(transitionSuccessMessage(vars));

    },

    onError: (error) => {

      toast.error('Status update failed', { description: error.message });

    },

  });

}

```

  

Conventions this encodes:

- API modules return `Promise<SchemaType>`, throw `Error` on failure — they

  never return a discriminated `{data, error}` result to the caller.

  `apiErrorMessage(error, fallback)` (`lib/api/errors.ts`) extracts a FastAPI

  `{detail: string}` or `{detail: [{msg}]}` body into a readable string.

- `data as unknown as X` casts appear throughout the API layer — this is a

  known, deliberate gap (openapi-fetch's inferred response type doesn't

  always line up 1:1 with the hand-picked domain type), not something to

  silently "fix" by weakening types elsewhere.

- Mutations invalidate by **domain-wide key** (`signalKeys.all`), not by the

  narrow key that changed — the feed, KPI strip, and tab counts all depend

  on the same underlying data and must all refetch together.

- User-facing success/error feedback is a **toast** (`sonner`, mounted once

  in `app/providers.tsx`), triggered from the mutation's `onSuccess`/`onError`,

  never from the component calling the mutation.

- `app/providers.tsx` sets **aggressive defaults**: `staleTime: 0`,

  `refetchOnWindowFocus: 'always'`, `refetchOnMount: 'always'`, and a

  `MutationCache.onSuccess` that calls `client.invalidateQueries()` with

  **no key filter at all** — every mutation success invalidates the entire

  cache. Combined with per-hook `staleTime: 60_000` overrides (e.g. KPIs),

  this is a deliberate "always-fresh over cache-efficient" trade-off — see

  `docs/superpowers/specs/2026-07-31-always-fresh-data-fetching-design.md`

  for the reasoning if you're tempted to "optimize" it.

  

### 6.2 Cursor pagination — one generic hook, never reimplemented per feature

  

`useCursorInfiniteQuery<TItem, TParams>` (`lib/hooks/use-cursor-infinite-query.ts`)

wraps `useInfiniteQuery` for any endpoint shaped `{ items, total, limit,

has_more, next_cursor }`. It flattens pages into `items`, and exposes

`hasNextPage`/`fetchNextPage`/`isFetchingNextPage` directly (no `.pages`

plumbing leaks into components). Pair it with `useLoadMoreOnVisible(onVisible,

enabled)` — an `IntersectionObserver`-based sentinel ref with a `200px`

`rootMargin`, wired as `<div ref={sentinelRef} />` at the bottom of the list

(see `signal-feed/index.tsx` line 42 + 106). **Any new paginated list must use

this pair, not a hand-rolled "load more" button or scroll listener.**

  

### 6.3 URL + sessionStorage state (filters, tabs, selection)

  

`useFilterState` (`lib/hooks/use-filter-state.ts`) is the canonical pattern

for state that must be: shareable via URL, restorable within a session, and

reactive to back/forward navigation. It:

1. Reads initial state from the URL; if the URL has nothing, falls back to

   `sessionStorage` (key `cr-signal-filter-state`).

2. On first mount, if state came from session (not URL), writes it into the

   URL via `router.replace` (no scroll jump, no history entry).

3. On every `setFilter`, updates both the URL and `sessionStorage` together.

4. Wraps every `sessionStorage` call in try/catch — SSR and private-browsing

   modes can throw; failures degrade silently to "no persistence", never a

   crash.

  

A related but distinct pattern lives in `signal-feed/hooks.ts`

(`useSelectedSignalId`, `useFeedFilters`): these write the URL via

**`history.pushState` directly**, not `router.push`/`router.replace`. The

code comment there explains why — this route is statically prerendered, and

a same-pathname soft navigation via the App Router's `router.push` silently

no-ops in production once the page has hard-loaded with query params

already present. If you add URL-driven state to a statically-rendered

route, check whether this workaround applies before assuming

`router.push` is safe.

  

### 6.4 Client-side derivation over redundant server calls

  

`lib/feed.ts` (`filterByTab`, `tabCounts`) computes tab counts/filters from

the **already-fetched** page set client-side, rather than issuing a separate

request per tab. Reach for this when the data is already in hand and the

derivation is cheap and pure — don't add a new endpoint for something the

already-fetched list can answer.

  

---

  

## 7. API integration details

  

### 7.1 Request path: browser → Next.js proxy → backend

  

```

Browser

  → apiClient.GET/POST (openapi-fetch, baseUrl: '')

  → Next.js same-origin request

  → app/api/[...path]/route.ts (server-side proxy)

  → process.env.API_URI (actual backend)

```

  

`apiClient` (`lib/api/client.ts`) is a **single shared instance**, augmented

with `.use()` middleware:

- `onRequest`: silently acquires an MSAL token (`acquireTokenSilent`) for the

  active/first account and sets `Authorization: Bearer <idToken>`. If silent

  acquisition fails with an interaction-required error, it emits a

  `window.dispatchEvent(new CustomEvent('auth:session-expired'))` — picked up

  by `SessionExpiredProvider` — rather than throwing into the caller.

- `onResponse`: on non-2xx, attempts to parse a JSON error body (tolerating

  non-JSON), special-cases `401` into the same session-expired event, and

  otherwise throws an `Error` annotated with `.status`/`.data` so callers

  (via `apiErrorMessage`) can extract a real message.

  

### 7.2 Type source of truth: `generated-schema.ts`

  

**Never hand-edit `src/generated-schema.ts`.** It's regenerated by

`pnpm generate-schema` (→ `src/codegen.mjs`, which calls

`openapi-typescript` against `${API_URI}/api/openapi.json`) and is excluded

from ESLint entirely (`eslint.config.mjs` `globalIgnores`). If a backend

route/shape you need isn't in it yet, regenerate against a backend that

exposes it — don't hand-add the type.

  

Rule for every new type in `lib/types/*.ts`:

  

```ts

// ✅ derive from schema

export type SignalDetail = components['schemas']['SignalDetail'];

  

// ❌ never re-declare a backend shape by hand

export interface SignalDetail { id: string; title: string; ... }

```

  

`lib/types/atlas.ts` is the **one documented, deliberate exception** — it

still hand-declares `BrandOut`/`CompetitorOut`-derived view-model types

(`AtlasBrand`, `AtlasVariant`, `AtlasCompetitor`) with UI-only extra fields

(`category_label`, `market_note`, `signal_count`) that the backend doesn't

serialize yet, each annotated with *why* and a note to delete the override

once the backend catches up. It also hand-declares multipart form payload

types (`CompetitorCreateInput` et al.) because OpenAPI only exposes

`multipart/form-data` JSON fields as an opaque `string` type — there's

nothing to derive. **Follow this exception's shape (extend/omit from the

schema type, comment the gap, note the removal condition) if you ever need

a similar override — don't silently duplicate a whole schema type by hand.**

  

Purely frontend-only concepts (`FilterState`, `FeedTab`, `TrendDay`,

`ConfidenceCounts`) are legitimately hand-declared `interface`s — there is no

backend schema for them, by design.

  

---

  

## 8. Auth & RBAC

  

- **`msalInstance`** (`lib/auth/msal.ts`) is the single MSAL client instance.

- **`AuthProvider`** wraps the app in `MsalProvider`.

- **`useAuth()`** (`lib/auth/use-auth.tsx`) composes MSAL account state +

  `useCurrentUserRecordQuery` (backend user lookup) + a Graph-API profile

  photo fetch (silently swallowed on failure — avatar falls back to

  initials) into one `{ user, ready, registered, login, logout }` shape.

  `registered` is a three-state (`true`/`false`/`null`-while-checking) flag,

  not a boolean — don't collapse it.

- **`RequireAuth`** (`lib/auth/require-auth.tsx`) is the route gate: redirects

  to `/login` if unauthenticated, to `/account-not-registered` if

  authenticated-but-not-`registered`, renders `null` while any of that is

  still resolving, else renders `children`. It wraps every route inside

  `app/(private)/layout.tsx`.

- **RBAC model** (`lib/hooks/use-permission.tsx`): `Role` (`Viewer` /

  `Editor` / `Admin`) and `Permission` (`signal.read`, `signal.update`,

  `atlas.read`, `atlas.update`, `config.read`, `config.update`) are separate

  enums, joined by a `ROLE_PERMISSIONS` lookup table. Per the domain model

  in the root `CLAUDE.md`, **Editor and Admin currently have identical

  permission sets** — this mirrors the product's "Analyst" role; "Leadership"

  (read-only) maps to `Viewer`.

  - `useAuthorize()` returns `{ user, roles, isViewer, isEditor, isAdmin, can }`.

  - `usePermission(permission)` — boolean hook for a single check.

  - `<PermissionGate permission={...}>` — declarative conditional render,

    used inline in JSX (see `SignalCard`'s Group/Ungroup button, gated on

    `Permission.SignalUpdate`). **Prefer `PermissionGate` over `usePermission`

    + a manual `{cond && <X/>}`** when the gated thing is a self-contained

    subtree, for consistency.

  

---

  

## 9. Styling conventions

  

- **Tailwind v4, CSS-first** — all config lives in `app/globals.css`:

  `@import 'tailwindcss'`, `@source` globs pointing at `app/`, `src/`,

  `components/`, a `@custom-variant dark`, `:root` HSL/hex custom properties,

  and a `@theme inline` block mapping them to Tailwind color/radius/font

  tokens. **There is no `tailwind.config.ts` — don't create one.**

- **Token discipline (from the root `CLAUDE.md`, verified in practice)**:

  the spacing scale is 4px/unit; prefer `p-6`, `p-6.5`, `p-7` over arbitrary

  `p-[24px]`. Half-step Tailwind v4 scale values (`2.5`, `3.5`, `6.5`) are

  valid — use them before reaching for `[Npx]`. Only use `p-[Npx]` for a

  value with no scale equivalent (e.g. `p-[17px]`), and only use an

  arbitrary value at all when no named token exists.

- **Two token systems coexist deliberately**: the semantic shadcn/Tailwind

  tokens (`--background`, `--primary`, `--sidebar`, …) for structural UI, and

  a parallel **Figma-exported token block** (`--color-figma-primary`,

  `--color-darkgreen-*`, `--color-black-*`, `--color-text-*`,

  `--color-geekblue-*`, etc., explicitly commented "Figma design tokens" with

  the source file key) for pixel-matching specific design specs. Both are

  valid Tailwind utilities (`bg-darkgreen-6`, `text-text-description`). Use

  the semantic tokens by default; reach for a Figma token when a screen must

  match a specific Figma frame exactly.

- **shadcn/ui first, always** (see root `CLAUDE.md` "Styling" section): use

  `Button`/`Select`/`Dialog`/`RadioGroup`/`Slider`/the shadcn `Toaster`

  before a native `<button>`/`<select>`/raw `<input>`/a hand-rolled toast.

  Only drop to native elements when no shadcn primitive covers the case.

- **`cn(...)`** (`clsx` + `tailwind-merge`, `lib/utils.ts`) is the only

  class-merging utility used — every conditional/combined `className` in the

  codebase goes through it (`cn('rounded-2xl p-5', isMember && 'border-[#c2e1c2]')`).

  Don't string-concatenate classNames or use template literals for

  conditional classes.

- **One-off design-spec colors** (e.g. `border-[#79A4D4]`, `text-[#2A6EBB]`

  in `signal-card.tsx`) appear as arbitrary hex values when a Figma spec

  calls for an exact color with no existing token — acceptable, but check

  `globals.css` first in case the color already has a token.

- **Global base-layer rules** in `globals.css` (`@layer base`) apply

  `cursor: pointer` to every interactive ARIA role app-wide (button, `role=

  button/menuitem/tab/option`, unless `disabled`/`aria-disabled`) — don't

  re-add `cursor-pointer` utility classes on components already covered by

  this; only add it where a custom clickable element falls outside those

  selectors.

  

---

  

## 10. Testing conventions

  

### 10.1 Unit / component — Jest + React Testing Library

  

- **All tests live in one flat `__tests__/` directory at the frontend root**

  (`frontend/__tests__/*.test.[jt]sx?`) — **not** colocated next to source

  files. `jest.config.ts`'s `testMatch` enforces this

  (`**/__tests__/**/*.test.[jt]s?(x)`).

- Naming mirrors the subject under test, not its full path:

  `signal-card.test.tsx`, `use-cursor-infinite-query.test.tsx`,

  `competitor-form-schema.test.ts`, `client.test.ts`.

- Component tests import the real component from its actual location

  (`app/(private)/radar-signals/components/signal-feed/signal-card`), wrap

  it in a fresh `QueryClientProvider` per test file

  (`new QueryClient({ defaultOptions: { queries: { retry: false } } })`) when

  the component touches TanStack Query — even indirectly — and assert via

  `getByText`/`getByRole` first, `getByTestId` as the fallback for

  non-textual nodes.

- Coverage scope (`jest.config.ts` `collectCoverageFrom`): `src/lib/**`,

  `src/components/**`, `app/**`, excluding `*.d.ts` and `layout.tsx` files.

  Reporters emit both `lcov`/`text` and SonarQube-compatible

  (`jest-sonar-reporter`, `jest-junit`) output — this repo's CI runs a

  SonarQube quality gate, so `pnpm test:cov` (not plain `pnpm test`) is the

  command to run before considering frontend work done (per root `CLAUDE.md`

  "Before Finishing Any Frontend Task").

  

### 10.2 E2E + visual — Playwright

  

- Spec + snapshot location: **`src/e2e/`** (`playwright.config.ts`

  `testDir: './src/e2e'`), with baseline images in adjacent

  `*.spec.ts-snapshots/` folders (verified present for `configuration`,

  `signal-detail`, `visual`).

- Runs against a **production build** (`webServer.command: 'pnpm build &&

  pnpm start'`), not the dev server — the comment in `playwright.config.ts`

  explains this is specifically to avoid the Next.js dev-tools indicator and

  HMR overlays polluting visual snapshots.

- Visual assertions use `toHaveScreenshot` at a fixed `1440×1024` viewport,

  `maxDiffPixelRatio: 0.02`, animations disabled. Update baselines

  deliberately via `pnpm e2e:update` — never regenerate them to "make a

  failing test pass" without confirming the visual change is intentional.

  

---

  

## 11. Documentation conventions

  

- **Per-route doc is mandatory** (root `CLAUDE.md` "Documentation upkeep"):

  every route needs a technical doc — purpose, components table, data hooks,

  states, tests — updated **in the same commit** as any change to that

  route's logic, endpoints, components, states, or tests.

- **Docs currently live in two places** — check both before assuming a route

  is undocumented:

  - `frontend/docs/routes/` — `configuration.md`, `brand-atlas.md`,

    `login.md`, `account-not-registered.md`

  - `frontend/src/docs/routes/` — `radar-feed.md`, `signal-detail.md`

  - New route docs should go under `frontend/docs/routes/` per the root

    `CLAUDE.md` — the `src/docs/routes/` location is the older set.

- When a change spans multiple routes or a shared component (e.g. anything

  in `app/(private)/components/`), update every affected route doc, not just

  one.

  

---

  

## 12. Linting, formatting, and build tooling

  

- **ESLint flat config** (`eslint.config.mjs`) layers `eslint-config-next`

  (core-web-vitals + TypeScript) with `@stylistic/eslint-plugin`, configured

  to match the existing codebase style: **single quotes, 2-space indent,

  semicolons, 1tbs brace style, arrow-paren always**. Stylistic rules are

  downgraded to **warnings**, deliberately, so `pnpm lint` (CI) stays green

  on not-yet-normalized files while editor format-on-save

  (`source.fixAll.eslint`, per `.vscode/settings.json`) still auto-fixes them

  incrementally. **Prettier is not used** — don't add a `.prettierrc` or run

  `prettier --write`; formatting is entirely ESLint's job here.

- `src/generated-schema.ts` is excluded from lint (`globalIgnores`) — never

  add lint-disable comments inside it; regenerate instead.

- **`pnpm generate-schema`** is the only sanctioned way to update

  `generated-schema.ts` (see §7.2). It requires a reachable backend exposing

  `/api/openapi.json` at `API_URI` (`.env`, defaults to

  `http://localhost:8002` in `codegen.mjs` if unset).

- **Path alias**: `@/*` → frontend root (`tsconfig.json`). Imports inside

  `src/` still commonly go through the full `@/src/lib/...` form rather than

  a shorter `@/lib/...` — match whichever existing sibling files in the

  folder you're editing use.

  

---

  

## 13. Do / Don't checklist for new work

  

**Do:**

- Add new server-state hooks under `lib/hooks/use-{domain}.ts`, re-export

  them from `lib/api/queries.ts`, and give them a `{domain}Keys` factory.

- Put route-only components under `app/(private)/<route>/components/`;

  promote to `src/components/common/` only once a second route needs it.

- Derive every backend-shaped type from `components['schemas'][...]` in

  `generated-schema.ts`; only hand-declare a type for a UI-only concept.

- Use `useCursorInfiniteQuery` + `useLoadMoreOnVisible` for any new

  paginated/infinite list.

- Gate role-sensitive UI with `<PermissionGate permission={Permission.X}>`.

- Use `cn(...)` for every conditional className; reach for a named Tailwind

  token before an arbitrary value.

- Write the Jest test into `frontend/__tests__/`, not colocated.

- Update the route's doc (`frontend/docs/routes/<route>.md`) in the same

  commit as any behavior change.

- Run `pnpm test:cov`, `pnpm lint`, `pnpm exec tsc --noEmit` before calling

  frontend work done (root `CLAUDE.md` "Verification").

  

**Don't:**

- Hand-edit `src/generated-schema.ts` — regenerate it.

- Call `apiClient`/`fetch` directly from a component — go through the domain

  API module + hook.

- Invalidate a mutation's *own* narrow query key only — invalidate the

  domain-wide key (`{domain}Keys.all`) so dependent views stay in sync,

  matching this app's always-fresh-over-cache-efficient stance.

- Create a `tailwind.config.ts` — all Tailwind v4 config is CSS-first in

  `app/globals.css`.

- Add a `.prettierrc` or run Prettier — ESLint Stylistic owns formatting.

- Use `router.push`/`router.replace` for query-string-only navigation on a

  statically-prerendered route without checking whether the

  `history.pushState` workaround in `signal-feed/hooks.ts` applies.

  

---

  

## 14. Known documentation drift

  

Two existing docs were found to describe an **earlier version of the app**

than what's on disk today. This doc was written against the real current

code; if you're cross-referencing the older docs, mind the gap:

  

- **`frontend/src/docs/tech-stack.md`** describes a "mock data layer" phase

  (`lib/mock/signals.ts`, `fetchSignals()` as "the future-backend seam") and

  routes under `app/(app)/...` / `components/radar/`. The app is now

  **wired to the live backend** through the proxy route (§7.1), and the

  authenticated route group is **`app/(private)/...`**, with feature

  components colocated under each route's own `components/` folder rather

  than a shared `components/radar/`. `src/e2e/` (not `frontend/e2e/`) is the

  real Playwright root.

- **`frontend/src/docs/routes/radar-feed.md`** likewise references

  `app/(app)/layout.tsx` and `app/(app)/radar-signals/...` — the current

  path is `app/(private)/radar-signals/...`. Several files it lists

  (`feed-filter.tsx`, `feed-empty.tsx`) were not found under that name in the

  current tree — treat that doc's file table as historical intent, not a

  live index, and prefer `frontend/docs/routes/` (§11) for current per-route

  documentation practice going forward.

  

If you touch either route, this is a good opportunity to bring its doc back

in line with reality per the "Documentation upkeep" rule in the root

`CLAUDE.md` — just don't assume its current contents are accurate before you

do.