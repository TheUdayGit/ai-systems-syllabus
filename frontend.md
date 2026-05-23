 ## File: frontend-engineering-react-nextjs-syllabus.md

# Frontend Engineering (React/Next.js)

## A World-Class, University-Level, Industry-Grade Technical Syllabus & Engineering Learning Roadmap

---

## Table of Contents

1. [Course Overview & Philosophy](#1-course-overview--philosophy)
2. [Target Audience & Prerequisites](#2-target-audience--prerequisites)
3. [Learning Objectives & Outcomes](#3-learning-objectives--outcomes)
4. [Module 0: Foundations & Mathematical Preliminaries](#module-0-foundations--mathematical-preliminaries)
5. [Module 1: React Deep Foundations](#module-1-react-deep-foundations)
6. [Module 2: The React Rendering Engine — Virtual DOM, Reconciliation & Fiber](#module-2-the-react-rendering-engine--virtual-dom-reconciliation--fiber)
7. [Module 3: React Hooks — Semantics, Implementation & Patterns](#module-3-react-hooks--semantics-implementation--patterns)
8. [Module 4: TypeScript for Production React](#module-4-typescript-for-production-react)
9. [Module 5: Next.js App Router Architecture](#module-5-nextjs-app-router-architecture)
10. [Module 6: React Server Components (RSC) — Theory, Execution Model & Production](#module-6-react-server-components-rsc--theory-execution-model--production)
11. [Module 7: Streaming, Suspense & Partial Prerendering (PPR)](#module-7-streaming-suspense--partial-prerendering-ppr)
12. [Module 8: Server Actions, Data Mutation & Form Architecture](#module-8-server-actions-data-mutation--form-architecture)
13. [Module 9: Caching Architecture in Next.js — Request Memoization, Data Cache, Full Route Cache & Router Cache](#module-9-caching-architecture-in-nextjs)
14. [Module 10: State Management at Scale — From Local to Global](#module-10-state-management-at-scale)
15. [Module 11: Performance Engineering — Core Web Vitals, Bundle Analysis & Optimization](#module-11-performance-engineering)
16. [Module 12: Testing Strategy — Unit, Integration, E2E & Visual Regression](#module-12-testing-strategy)
17. [Module 13: Production Architecture — Feature-Sliced Design, Monorepos & Micro-Frontends](#module-13-production-architecture)
18. [Module 14: Security, Authentication & Authorization](#module-14-security-authentication--authorization)
19. [Module 15: Observability, Monitoring & Debugging](#module-15-observability-monitoring--debugging)
20. [Module 16: AI-Integrated Frontend Engineering](#module-16-ai-integrated-frontend-engineering)
21. [Capstone Project](#capstone-project)
22. [Appendix A: Reading List & References](#appendix-a-reading-list--references)
23. [Appendix B: Tooling & Ecosystem](#appendix-b-tooling--ecosystem)
24. [Appendix C: Interview Preparation](#appendix-c-interview-preparation)

---

## 1. Course Overview & Philosophy

This syllabus treats Frontend Engineering not as a craft of assembling UI components, but as a **systems discipline** at the intersection of:

- **Computer Science**: algorithms, data structures, complexity theory, and formal semantics
- **Mathematics**: category theory (functors, monads), graph theory (dependency graphs), and linear algebra (for animation/GPU)
- **Systems Engineering**: distributed rendering, streaming protocols, caching hierarchies, and edge computing
- **Production AI Infrastructure**: how frontend systems serve ML models, inference UIs, and real-time data pipelines

The modern frontend is no longer a thin client. With React Server Components, edge computing, streaming SSR, and AI-driven interfaces, the frontend has become a **distributed system** with server-client boundaries, caching layers, and real-time data flows that rival traditional backend architecture in complexity.

This course progresses from **beginner** → **intermediate** → **advanced** → **production-grade mastery**, with each module building a complete mental model that connects theory to implementation to systems to infrastructure.

---

## 2. Target Audience & Prerequisites

### Target Audience
- AI Systems Engineers building inference UIs and model dashboards
- ML Infrastructure Engineers serving frontend interfaces for training pipelines
- LLM Engineers building chat interfaces, prompt playgrounds, and agent UIs
- MLOps Engineers creating monitoring dashboards and experiment trackers
- Distributed Systems Engineers extending into frontend systems
- Backend Engineers transitioning to full-stack with production rigor
- Staff-level infrastructure candidates preparing for frontend architecture interviews

### Prerequisites
- **Solid JavaScript/TypeScript**: closures, prototypes, async/await, generators, type systems
- **Computer Science Fundamentals**: algorithms, data structures, complexity analysis
- **Web Platform**: HTTP, DOM, browser event loop, CORS, cookies, Web APIs
- **Basic React**: JSX, components, props, state (we will rebuild these from first principles)
- **Mathematics**: basic set theory, functions, graphs (advanced linear algebra for Module 11)

---

## 3. Learning Objectives & Outcomes

By the end of this course, you will be able to:

1. **Architect** production-grade React/Next.js applications with server-first mental models
2. **Debug** React's rendering lifecycle, hydration mismatches, and streaming failures at the engine level
3. **Optimize** Core Web Vitals (LCP, INP, CLS, TTFB, FCP) through systematic measurement and intervention
4. **Design** caching strategies across four layers (request memoization, data cache, full route cache, router cache)
5. **Implement** React Server Components with correct boundaries, data fetching patterns, and error handling
6. **Build** streaming UIs with Suspense boundaries, loading states, and progressive hydration
7. **Engineer** state management systems that scale from local component state to global stores with minimal re-renders
8. **Secure** frontend applications with proper auth flows, CSRF protection, and XSS mitigation
9. **Monitor** frontend performance with real user metrics (RUM), distributed tracing, and error tracking
10. **Integrate** AI capabilities (LLM streaming, real-time inference UIs) into production frontend systems

---

## Module 0: Foundations & Mathematical Preliminaries

### 0.1 The Lambda Calculus & Functional Programming Foundations
- **Lambda calculus**: variables, abstractions, applications, beta-reduction
- **Church encoding**: booleans, numbers, pairs as pure functions
- **Y combinator**: fixed-point combinators and recursion in the lambda calculus
- **Connection to React**: React components as pure functions (props → UI), immutability as lambda calculus values

### 0.2 Category Theory for Frontend Engineers
- **Categories**: objects and morphisms
- **Functors**: mapping between categories (Array.map, Promise.then)
- **Monads**: Maybe, Promise, State — the monad laws (left identity, right identity, associativity)
- **React as a monad**: `useState` as State monad, `useEffect` as IO monad
- **Practical application**: why React's compositional model is mathematically sound

### 0.3 Graph Theory for Component Trees
- **Directed acyclic graphs (DAGs)**: component trees as DAGs
- **Topological sorting**: render order, effect execution order
- **Dependency graphs**: module bundling, tree shaking, dead code elimination
- **Reachability**: which components re-render when state changes

### 0.4 Complexity Analysis for UI
- **Time complexity**: O(n) list rendering, O(log n) virtual DOM diffing
- **Space complexity**: closure memory, memoization tradeoffs
- **Amortized analysis**: React's reconciliation as amortized O(n)
- **Big-O of re-renders**: why `React.memo` is O(1) vs full re-render O(n)

### 0.5 The Event Loop & Concurrency Model
- **JavaScript event loop**: call stack, task queue, microtask queue
- **Macrotasks vs microtasks**: `setTimeout` vs `Promise.then`
- **Render phase vs commit phase**: how React schedules work
- **Concurrent React**: time slicing, priority lanes, interruptible rendering

### 0.6 Reading
- *Structure and Interpretation of Computer Programs* (SICP), Ch. 1-2
- *Category Theory for Programmers* by Bartosz Milewski, Ch. 1-3
- React Source Code: `packages/react-reconciler/src/ReactFiberWorkLoop.js`

---

## Module 1: React Deep Foundations

### 1.1 JSX: Syntax Sugar and the Transformation Pipeline
- **JSX as syntactic sugar**: `React.createElement(type, props, ...children)`
- **Babel transformation**: JSX → `createElement` calls → React elements
- **The React Element**: `{ type, props, key, ref }` — a plain object, not a DOM node
- **Custom JSX transforms**: `@jsx` pragma, automatic runtime (React 17+)
- **TypeScript JSX**: `jsx: "react-jsx"`, `jsxImportSource`

### 1.2 Components as Functions: Pure vs Impure
- **Pure components**: same props → same output, no side effects
- **Impure components**: side effects, external state, I/O
- **Referential transparency**: why it matters for memoization
- **Component contracts**: input (props), output (React elements), effects (side effects)

### 1.3 Props, State, and the Data Flow
- **Unidirectional data flow**: props down, events up
- **Lifting state up**: shared state ownership
- **Props drilling**: the problem and solutions (context, composition)
- **State as a snapshot**: why `setState` is async and batched
- **The closure stale state problem**: capturing state in callbacks, `useRef` as escape hatch

### 1.4 The Component Lifecycle (Class vs Function)
- **Class components**: `constructor`, `render`, `componentDidMount`, `componentDidUpdate`, `componentWillUnmount`
- **Function components + Hooks**: mapping class lifecycle to hooks
- **The mental model shift**: from lifecycle methods to synchronization

### 1.5 Composition Patterns
- **Containment**: `children` prop, `render props`
- **Specialization**: `Dialog` → `AlertDialog`
- **Higher-Order Components (HOCs)**: `withRouter`, `withAuth` — when to use, when to avoid
- **Custom Hooks**: extracting stateful logic, the rules of hooks
- **The "composition over inheritance" principle**: why React favors composition

### 1.6 Controlled vs Uncontrolled Components
- **Controlled**: React owns the state (`value` + `onChange`)
- **Uncontrolled**: DOM owns the state (`defaultValue`, `ref`)
- **When to use which**: forms, inputs, external libraries
- **The `key` prop as reset mechanism**: forcing remount with changing keys

### 1.7 Lab: Build a Mini-React
- Implement `createElement`, `render`, and a naive reconciliation algorithm
- Build a virtual DOM diffing algorithm (simplified)
- Understand why React's reconciliation is O(n) not O(n³)

---

## Module 2: The React Rendering Engine — Virtual DOM, Reconciliation & Fiber

### 2.1 The Virtual DOM: Design Rationale & Data Structure
- **Why virtual DOM?**: abstraction over browser DOM, cross-platform rendering
- **React Element tree**: immutable, lightweight description of UI
- **Fiber tree**: mutable, persistent data structure for work-in-progress
- **Double buffering**: current tree vs work-in-progress tree

### 2.2 The Reconciliation Algorithm
- **Diffing heuristics**:
  1. Different element types → rebuild subtree
  2. Same element type → update props
  3. Keys for list reconciliation
- **O(n) complexity proof**: why the heuristic works in practice
- **The key prop**: identity and stability, why index as key is dangerous
- **Reconciliation vs rendering**: reconciliation produces the new tree, rendering applies changes

### 2.3 React Fiber Architecture
- **Fiber as a unit of work**: `{ type, key, stateNode, child, sibling, return, alternate, effectTag, ... }`
- **The Fiber tree structure**: linked list traversal (child → sibling → return)
- **Work phases**:
  - **Render phase** (reconciliation): can be interrupted, no side effects
  - **Commit phase** (DOM mutations): synchronous, side effects allowed
- **Time slicing**: breaking work into chunks, `shouldYield()` checks
- **Priority lanes**: different priorities for different updates (user input > data fetching > offscreen)

### 2.4 The Render Phase Deep Dive
- **Begin work**: processing a fiber node, calling the component function
- **Complete work**: finishing a fiber node, building the effect list
- **Bailout**: skipping work when props/state haven't changed
- **Context propagation**: how context updates traverse the tree

### 2.5 The Commit Phase Deep Dive
- **Pre-commit**: `getSnapshotBeforeUpdate`
- **Mutation**: DOM updates, `useLayoutEffect` fires
- **Layout**: `componentDidMount`, `componentDidUpdate`
- **Passive effects**: `useEffect` fires asynchronously

### 2.6 Concurrent Features
- **Concurrent Mode**: interruptible rendering, priority-based scheduling
- **Transitions**: `useTransition`, marking updates as non-urgent
- **Deferred values**: `useDeferredValue`, delaying re-renders of non-critical UI
- **Suspense**: throwing promises to pause rendering

### 2.7 Hydration: SSR to CSR Bridge
- **What is hydration?**: attaching event listeners to server-rendered HTML
- **Hydration mismatch**: why it happens, how to debug
- **Progressive hydration**: hydrating components incrementally
- **Selective hydration**: React 18's streaming hydration

### 2.8 Lab: Profile and Optimize Re-renders
- Use React DevTools Profiler to identify unnecessary re-renders
- Implement `React.memo`, `useMemo`, `useCallback` with correct dependency arrays
- Measure before/after with `performance.now()` and React Profiler

---

## Module 3: React Hooks — Semantics, Implementation & Patterns

### 3.1 The Rules of Hooks
- **Call hooks at the top level**: why the call order matters
- **Call hooks from React functions only**: enforcing the rules with ESLint
- **The hooks array**: how React stores hook state in fiber nodes
- **Hook indices**: why conditional hooks break everything

### 3.2 useState: The State Hook
- **Implementation**: `mountState` vs `updateState`
- **Batched updates**: automatic batching in React 18+
- **Functional updates**: `setState(prev => prev + 1)`
- **Lazy initialization**: `useState(() => expensiveComputation())`
- **State as snapshot**: closures and stale state

### 3.3 useEffect: The Side Effect Hook
- **Semantics**: synchronize with external systems
- **Dependency array**: when effects run, the exhaustive-deps rule
- **Cleanup functions**: subscription patterns, race conditions
- **The `useEffect` mental model**: not lifecycle, but synchronization
- **Common pitfalls**: missing dependencies, infinite loops, stale closures

### 3.4 useRef: The Mutable Ref Hook
- **Persistent mutable values**: surviving re-renders without causing them
- **DOM refs**: `ref={element => { ... }}`
- **Previous value tracking**: `usePrevious` custom hook
- **Imperative handles**: `useImperativeHandle`, `forwardRef`

### 3.5 useMemo & useCallback: Memoization Hooks
- **useMemo**: memoizing expensive computations
- **useCallback**: memoizing function references
- **When to use**: measure first, optimize second
- **The reference equality trap**: why `useCallback` is needed for stable references
- **Memoization invalidation**: dependency arrays and referential stability

### 3.6 useReducer: The State Machine Hook
- **Reducer pattern**: `(state, action) => newState`
- **Complex state logic**: when `useState` is not enough
- **Dispatch function**: stable reference, no need for `useCallback`
- **Lazy initialization**: `useReducer(reducer, initialArg, init)`
- **Comparison to Redux**: local vs global state machines

### 3.7 useContext: The Context Hook
- **Context API**: `createContext`, `Provider`, `Consumer`
- **Performance implications**: context splits, preventing unnecessary re-renders
- **Context selectors**: why React doesn't have them, workarounds
- **Multiple contexts**: composing providers, the provider hell problem

### 3.8 Custom Hooks: Design Patterns
- **Naming convention**: `useSomething`
- **Encapsulation**: hiding implementation details
- **Composition**: combining multiple hooks
- **Testing**: mocking hooks, testing hook logic in isolation
- **Common patterns**: `useFetch`, `useLocalStorage`, `useDebounce`, `useThrottle`

### 3.9 Advanced Hooks
- **useLayoutEffect**: synchronous layout effects, when to use vs `useEffect`
- **useId**: generating unique IDs for accessibility
- **useSyncExternalStore**: subscribing to external stores (TanStack Query, Zustand)
- **useInsertionEffect**: CSS-in-JS injection timing

### 3.10 Lab: Build a State Management Library
- Implement `createStore`, `useStore` using `useSyncExternalStore`
- Add selectors, actions, and middleware
- Compare performance with Redux and Zustand

---

## Module 4: TypeScript for Production React

### 4.1 Type System Foundations
- **Structural typing**: TypeScript vs nominal typing
- **Type inference**: when TypeScript can and cannot infer
- **Generics**: `<T>`, constraints, default types
- **Conditional types**: `T extends U ? X : Y`
- **Mapped types**: `{ [K in keyof T]: V }`
- **Template literal types**: type-safe string manipulation

### 4.2 React-Specific TypeScript Patterns
- **Component types**: `React.FC` vs explicit props interfaces
- **Props with children**: `PropsWithChildren`, `ReactNode` vs `ReactElement`
- **Event types**: `MouseEvent`, `ChangeEvent`, `FormEvent`
- **Ref types**: `RefObject`, `MutableRefObject`, `ForwardedRef`
- **Context types**: creating typed contexts

### 4.3 Advanced Type Patterns
- **Discriminated unions**: type-safe state machines
- **Branded types**: nominal typing in structural system
- **Function overloads**: multiple signatures for flexibility
- **Type guards**: `is` keyword, narrowing types
- **Assertion functions**: `asserts` keyword

### 4.4 Type-Safe API Integration
- **Generating types from OpenAPI**: `openapi-typescript`
- **Runtime validation**: `zod`, `valibot` with TypeScript
- **End-to-end type safety**: tRPC, GraphQL Codegen

### 4.5 Monorepo TypeScript Configuration
- **Project references**: `tsconfig.json` references
- **Path mapping**: `baseUrl`, `paths`
- **Strict mode**: `strict`, `noImplicitAny`, `strictNullChecks`
- **Declaration files**: `.d.ts`, publishing types

### 4.6 Lab: Type-Safe Design System
- Build a component library with full TypeScript coverage
- Implement polymorphic components (`as` prop) with type safety
- Create compound component patterns with strict typing

---

## Module 5: Next.js App Router Architecture

### 5.1 App Router vs Pages Router: The Platform Shift
- **Pages Router**: request/response mindset, `getServerSideProps`, `getStaticProps`
- **App Router**: server-first, streaming-by-default, React Server Components
- **File-system routing**: `page.tsx`, `layout.tsx`, `loading.tsx`, `error.tsx`, `template.tsx`
- **Route groups**: `(group)` for layout grouping without URL segments
- **Parallel routes**: `@folder` for simultaneous page views
- **Intercepting routes**: `(.)`, `(..)`, `(...)` for modal patterns

### 5.2 The Server-First Mental Model
- **Default server components**: all components are server components unless marked
- **The `"use client"` directive**: opt-in to client-side execution
- **Server-client boundary**: where the split happens, implications for imports
- **Data proximity**: fetching close to where data is used

### 5.3 Layout Architecture
- **Root layout**: `app/layout.tsx`, global chrome, HTML structure
- **Nested layouts**: layout composition, shared UI across segments
- **Layout persistence**: layouts don't re-render on navigation
- **Template re-renders**: `template.tsx` vs `layout.tsx`
- **Layout as server component**: data fetching in layouts

### 5.4 Navigation & Routing
- **`<Link>` component**: prefetching, client-side navigation
- **`useRouter`**: programmatic navigation, `push`, `replace`, `refresh`
- **Route segments**: `[id]`, `[...slug]`, `[[...optional]]`
- **Middleware**: `middleware.ts`, route protection, rewrites, redirects

### 5.5 Error Boundaries & Loading States
- **`error.tsx`**: route-level error boundaries
- **`global-error.tsx`**: root error boundary
- **`loading.tsx`**: route-level Suspense boundaries
- **Error handling strategy**: graceful degradation, retry logic

### 5.6 Lab: Build a Multi-Tenant Dashboard
- Implement nested layouts for admin/user roles
- Use parallel routes for split-pane views
- Add intercepting routes for modal detail views
- Implement middleware for auth and localization

---

## Module 6: React Server Components (RSC) — Theory, Execution Model & Production

### 6.1 What Are React Server Components?
- **Definition**: components that render exclusively on the server, shipping zero JS to the client
- **The RSC payload**: serialized component output (not HTML, not JSON)
- **Streaming format**: newline-delimited JSON (NDJSON) for progressive delivery
- **Zero bundle size**: server components don't contribute to client bundle

### 6.2 The Execution Model
- **Server render path**: request → server component tree → RSC payload → client
- **Client render path**: RSC payload → React reconciler → DOM (or hydration)
- **The server-client boundary**: where serialization happens, what can cross it
- **Async components**: `async function` in server components, `await` directly in JSX

### 6.3 Server vs Client Components: Decision Matrix

| Criterion | Server Component | Client Component |
|-----------|-----------------|------------------|
| Data fetching | ✅ Direct DB/API access | ❌ Must use API/client fetch |
| Bundle size | ✅ Zero client JS | ❌ Ships JS to browser |
| Interactivity | ❌ No state/events | ✅ Full React features |
| Browser APIs | ❌ No `window`, `document` | ✅ Full browser access |
| Secrets | ✅ Safe to use | ❌ Never expose secrets |
| Heavy dependencies | ✅ Server-side only | ❌ Bundled to client |

### 6.4 The Server-Client Boundary Rules
- **Server can render client**: server component can import and render client components
- **Client cannot render server**: client components cannot import server components
- **Passing server components as props**: the "children as props" pattern
- **Serialization constraints**: functions, classes, and symbols cannot cross the boundary

### 6.5 Data Fetching in Server Components
- **Direct data access**: ORM queries, file system reads, internal API calls
- **No API ping-pong**: fetch data where it's rendered, not from the client
- **Parallel fetching**: `Promise.all` for independent data sources
- **Sequential fetching**: when data dependencies are chained
- **The data dependency graph**: designing components around data, not visuals

### 6.6 Production Best Practices
- **Design around data dependencies first**: identify parallel vs sequential data needs
- **Keep client components explicit and minimal**: shallow in the tree, well-documented
- **Treat server components as default**: client components are exceptions
- **Instrument server render path**: measure server render latency, backend fan-out, cache behavior

### 6.7 Lab: Migrate a CSR App to RSC Architecture
- Identify server-renderable components
- Move data fetching from client to server
- Implement proper server-client boundaries
- Measure bundle size reduction and LCP improvement

---

## Module 7: Streaming, Suspense & Partial Prerendering (PPR)

### 7.1 Streaming Fundamentals
- **Chunked transfer encoding**: HTTP/1.1 chunked encoding, HTTP/2 streams
- **Progressive HTML delivery**: sending parts of the page as they become ready
- **TTFB vs FCP vs TTI**: streaming improves all three metrics
- **The streaming protocol**: how React serializes and streams component trees

### 7.2 Suspense Boundaries
- **The Suspense component**: `<Suspense fallback={<Loading />}>` 
- **Throwing promises**: how components "suspend" rendering
- **Error boundaries**: catching errors in suspended components
- **Nested Suspense**: hierarchical loading states

### 7.3 Next.js Streaming Patterns
- **`loading.tsx`**: page-level streaming with automatic Suspense
- **Component-level Suspense**: manual `<Suspense>` boundaries
- **Staggered loading**: prioritizing critical content
- **Skeleton UI**: loading placeholders that match final layout (reducing CLS)

### 7.4 Partial Prerendering (PPR)
- **Concept**: static shell at build time + dynamic holes at request time
- **Static shell**: cacheable, CDN-delivered, instant first paint
- **Dynamic holes**: streaming in personalized/real-time content
- **PPR enablement**: configuration, route-level control
- **Authoring for PPR**: making shells static, wrapping dynamic parts in Suspense

### 7.5 Streaming with Data Fetching Libraries
- **TanStack Query + streaming**: prefetching, dehydration, hydration
- **Pending queries**: dehydrating unresolved queries for streaming
- **The `use` API**: React 19's `use(promise)` for reading promises in components

### 7.6 Lab: Build a Streaming E-Commerce Product Page
- Static shell: product images, title, description
- Dynamic holes: live price, stock level, personalized recommendations
- Implement skeleton UI for each dynamic section
- Measure TTFB, LCP, and CLS improvements

---

## Module 8: Server Actions, Data Mutation & Form Architecture

### 8.1 Server Actions Fundamentals
- **Definition**: async functions that run on the server, callable from components
- **`"use server"` directive**: marking server actions
- **Progressive enhancement**: forms work without JavaScript
- **HTTP streaming**: server action responses stream in chunks

### 8.2 Form Architecture with Server Actions
- **The `action` prop**: `<form action={serverAction}>`
- **FormData handling**: `formData.get()`, type-safe form parsing
- **Validation**: server-side validation with `zod`, client-side with `react-hook-form`
- **Error handling**: returning error states from server actions
- **Optimistic updates**: `useOptimistic` for immediate UI feedback

### 8.3 Server Actions vs Route Handlers
- **Server Actions**: direct server function calls, form submissions, mutations
- **Route Handlers**: `app/api/**/route.ts`, RESTful endpoints, external API proxying
- **When to use which**: mutation complexity, API surface area, client needs

### 8.4 Advanced Server Action Patterns
- **Composed actions**: calling server actions from other server actions
- **Revalidation**: `revalidatePath`, `revalidateTag` for cache invalidation
- **Redirecting**: `redirect()` from server actions
- **Cookies and headers**: accessing request context in server actions

### 8.5 Security Considerations
- **CSRF protection**: built-in origin validation
- **Input validation**: never trust client input
- **Rate limiting**: preventing abuse of server actions
- **Authorization**: checking permissions before mutations

### 8.6 Lab: Build a Full-Stack CRUD Application
- Create, read, update, delete with server actions
- Implement optimistic updates and error handling
- Add form validation with `zod` and `react-hook-form`
- Implement revalidation strategies

---

## Module 9: Caching Architecture in Next.js

### 9.1 The Four Caching Layers

| Layer | Scope | Mechanism | Control |
|-------|-------|-----------|---------|
| **Request Memoization** | Per-request | `React.cache()` | Automatic |
| **Data Cache** | Persistent | `fetch()` with `next.revalidate` | `cache`, `revalidateTag` |
| **Full Route Cache** | Route-level | Static generation, ISR | `revalidate`, `dynamic` |
| **Router Cache** | Client-side | In-memory, navigation | `router.refresh()` |

### 9.2 Request Memoization
- **`React.cache()`**: deduplicating requests within a single render
- **Why it matters**: preventing duplicate database queries
- **Scope**: single request, single render pass
- **Automatic**: Next.js applies this automatically to `fetch`

### 9.3 Data Cache
- **`fetch()` caching**: `cache: 'force-cache'`, `cache: 'no-store'`
- **`next.revalidate`**: time-based revalidation
- **`unstable_cache`**: caching function results
- **Cache tags**: `revalidateTag()` for on-demand invalidation
- **Cache keys**: how Next.js generates cache keys from fetch options

### 9.4 Full Route Cache (Static & ISR)
- **Static generation**: `generateStaticParams()`, build-time rendering
- **ISR**: incremental static regeneration, stale-while-revalidate
- **Dynamic routes**: `dynamic = 'force-dynamic'`, `dynamic = 'auto'`
- **The `revalidate` export**: route-level revalidation configuration

### 9.5 Router Cache (Client-Side)
- **In-memory caching**: cached route segments in the browser
- **Prefetching**: `<Link prefetch>` warming the cache
- **Cache invalidation**: `router.refresh()`, `router.push()`
- **Soft navigation**: client-side transitions without full page reloads

### 9.6 Cache Invalidation Strategies
- **Time-based**: `revalidate = 3600` (seconds)
- **On-demand**: `revalidatePath()`, `revalidateTag()`
- **Webhook-driven**: external systems triggering revalidation
- **Selective invalidation**: tag-based vs path-based

### 9.7 Lab: Design a Cache Architecture for a News Site
- Static shell with ISR for articles
- Dynamic comments with request memoization
- On-demand revalidation via webhooks
- Measure cache hit rates and stale content windows

---

## Module 10: State Management at Scale

### 10.1 Local State Patterns
- **`useState`**: simple component state
- **`useReducer`**: complex state logic, state machines
- **Lifting state up**: shared ownership
- **State colocation**: keeping state as close to usage as possible

### 10.2 React Context for Medium Scale
- **When context is enough**: theme, auth, locale
- **Context splits**: preventing unnecessary re-renders
- **Context selectors**: memoized selectors, split contexts
- **The provider pattern**: composing multiple providers

### 10.3 External State Management Libraries

#### 10.3.1 Zustand
- **Simple, unopinionated**: store as hook
- **Selectors**: subscribing to specific slices
- **Middleware**: persistence, devtools, immer
- **TypeScript support**: full type inference

#### 10.3.2 TanStack Query (React Query)
- **Server state management**: caching, synchronization, deduplication
- **Queries**: `useQuery`, `useInfiniteQuery`
- **Mutations**: `useMutation`, optimistic updates
- **Prefetching**: `queryClient.prefetchQuery`
- **Dehydration/hydration**: SSR support

#### 10.3.3 Jotai / Recoil
- **Atomic state**: atoms as units of state
- **Derived state**: selectors, atom families
- **Fine-grained reactivity**: component updates only when specific atoms change

#### 10.3.4 Redux Toolkit (RTK)
- **When to still use Redux**: complex state machines, time-travel debugging
- **RTK Query**: built-in data fetching and caching
- **Middleware ecosystem**: saga, thunk, observable

### 10.4 State Architecture Decision Framework
- **Server state vs client state**: different concerns, different tools
- **URL as state**: `useSearchParams`, `usePathname`
- **Form state**: `react-hook-form`, `formik`
- **Derived state**: computed values, memoization

### 10.5 Signals and Fine-Grained Reactivity
- **Signals pattern**: fine-grained subscriptions, bypassing React's render cycle
- **Preact Signals**: `@preact/signals-react`
- **React Compiler (React 19)**: automatic memoization, signal-like optimization
- **When signals matter**: high-frequency updates, real-time data

### 10.6 Lab: Build a Real-Time Collaboration Board
- Implement optimistic updates with TanStack Query
- Add Zustand for local UI state
- Use Jotai for fine-grained cursor position tracking
- Measure re-render performance with React Profiler

---

## Module 11: Performance Engineering

### 11.1 Core Web Vitals Deep Dive

| Metric | Target | Measurement | Optimization |
|--------|--------|-------------|------------|
| **LCP** | < 2.5s | Largest Contentful Paint | Image optimization, preloading, font loading |
| **INP** | < 200ms | Interaction to Next Paint | Event handlers, main thread blocking, debouncing |
| **CLS** | < 0.1 | Cumulative Layout Shift | Image dimensions, font loading, dynamic content |
| **TTFB** | < 600ms | Time to First Byte | Edge deployment, caching, streaming |
| **FCP** | < 1.8s | First Contentful Paint | Critical CSS, resource hints, preconnect |

### 11.2 Bundle Optimization
- **Code splitting**: `dynamic(() => import(...))`, route-based splitting
- **Tree shaking**: ES modules, `sideEffects` in `package.json`
- **Dependency analysis**: `webpack-bundle-analyzer`, `@next/bundle-analyzer`
- **Dead code elimination**: `terser`, `esbuild` minification
- **Third-party scripts**: lazy loading, `next/script`, `strategy` prop

### 11.3 Image Optimization
- **`next/image`**: automatic optimization, WebP/AVIF, responsive images
- **Priority loading**: `priority` prop for LCP images
- **Placeholder strategies**: blur, color, empty
- **Art direction**: `sizes`, `srcSet`, `media` queries

### 11.4 Font Optimization
- **`next/font`**: automatic font optimization, zero layout shift
- **Font display**: `swap`, `optional`, `block`
- **Variable fonts**: single file, multiple weights
- **Self-hosting**: vs Google Fonts CDN

### 11.5 CSS Optimization
- **Critical CSS**: inlining above-the-fold styles
- **CSS-in-JS**: styled-components, emotion, CSS modules
- **Tailwind CSS**: utility-first, purge optimization
- **CSS containment**: `contain` property for render isolation

### 11.6 Runtime Performance
- **React.memo**: shallow comparison, custom comparators
- **useMemo / useCallback**: when they help, when they hurt
- **Virtualization**: `react-window`, `react-virtualized` for long lists
- **Debouncing and throttling**: input handlers, scroll events
- **Web Workers**: offloading heavy computation

### 11.7 Lab: Optimize a Slow Dashboard
- Profile with Lighthouse, WebPageTest, and React DevTools
- Implement code splitting for heavy charts
- Optimize images and fonts
- Reduce INP by debouncing interactions
- Target all Core Web Vitals in the "good" range

---

## Module 12: Testing Strategy

### 12.1 Testing Pyramid for Frontend

```
        /\
       /  \  E2E (Cypress, Playwright)
      /____\     ~10% of tests
     /      \
    /        \  Integration (RTL + MSW)
   /__________\     ~30% of tests
  /            \
 /              \  Unit (Jest, Vitest)
/________________\     ~60% of tests
```

### 12.2 Unit Testing
- **Jest / Vitest**: test runner, mocking, coverage
- **React Testing Library (RTL)**: testing behavior, not implementation
- **Component testing**: rendering, user interactions, assertions
- **Hook testing**: `renderHook` for custom hooks
- **Snapshot testing**: when useful, when harmful

### 12.3 Integration Testing
- **Mock Service Worker (MSW)**: intercepting HTTP requests
- **Testing data fetching**: mocking `fetch`, TanStack Query
- **Testing forms**: user events, validation, submission
- **Testing routing**: Next.js router mocking

### 12.4 E2E Testing
- **Playwright**: cross-browser, parallel execution, trace viewer
- **Cypress**: real browser, time-travel debugging
- **Visual regression**: Chromatic, Percy, Loki
- **Accessibility testing**: axe-core, automated a11y checks

### 12.5 Performance Testing
- **Lighthouse CI**: automated performance audits
- **Bundle size monitoring**: `bundlesize`, GitHub Actions
- **Load testing**: k6, Artillery for frontend stress testing

### 12.6 Lab: Build a Comprehensive Test Suite
- Unit tests for components and hooks
- Integration tests for data fetching flows
- E2E tests for critical user journeys
- Visual regression tests for design system components

---

## Module 13: Production Architecture

### 13.1 Feature-Sliced Design (FSD)
- **Layers**: `app` (routes), `pages` (compositions), `widgets`, `features`, `entities`, `shared`
- **Slices**: feature-based modules within layers
- **Segments**: `ui`, `model`, `lib`, `api`, `config` within slices
- **Public API**: explicit exports, encapsulation
- **Dependency rule**: layers can only import from lower layers

```
src/
├── app/                    # Application initialization, providers, routes
├── pages/                  # Page components, route handlers
├── widgets/                # Independent UI blocks (header, sidebar)
├── features/               # User scenarios (auth, cart, search)
│   └── cart/
│       ├── ui/             # Components
│       ├── model/          # State, hooks
│       ├── api/            # API calls, server actions
│       └── lib/            # Utilities
├── entities/               # Business entities (user, product, order)
│   └── product/
│       ├── model/          # Types, stores
│       ├── api/            # Queries, mutations
│       └── ui/             # Entity components
└── shared/                 # Reusable code, design system
    ├── ui/                 # Design system components
    ├── api/                # Base API client
    ├── config/             # Environment config
    └── lib/                # Utilities
```

### 13.2 Monorepo Architecture
- **Turborepo**: build pipeline, remote caching, task orchestration
- **Nx**: dependency graph, affected commands, code generators
- **pnpm workspaces**: workspace protocols, shared dependencies
- **Package boundaries**: design system as separate package, versioning strategy

### 13.3 Micro-Frontends
- **Module Federation**: webpack 5, runtime integration
- **Build-time integration**: package-based, monorepo
- **Edge composition**: stitching at the CDN level
- **When to use**: team autonomy, independent deployments, massive scale
- **When not to use**: coordination overhead, shared state complexity

### 13.4 Design Systems
- **Component library**: atomic design, compound components
- **Token system**: colors, typography, spacing, breakpoints
- **Documentation**: Storybook, MDX, interactive examples
- **Distribution**: npm packages, versioning, breaking changes

### 13.5 Lab: Architect a Production-Scale Application
- Implement FSD folder structure
- Create a shared design system package
- Set up Turborepo with remote caching
- Implement feature-based code splitting

---

## Module 14: Security, Authentication & Authorization

### 14.1 Authentication Architecture
- **Session-based**: cookies, server-side sessions
- **Token-based**: JWT, localStorage, `Authorization` header
- **OAuth 2.0 / OIDC**: social login, identity providers
- **NextAuth.js / Auth.js**: framework-agnostic auth

### 14.2 Next.js Auth Patterns
- **Middleware auth**: `middleware.ts` for route protection
- **Server component auth**: session validation in server components
- **Client component auth**: token refresh, auth context
- **Server Actions auth**: validating sessions in mutations

### 14.3 Authorization Patterns
- **RBAC**: Role-Based Access Control
- **ABAC**: Attribute-Based Access Control
- **Route guards**: protecting pages and API routes
- **Component-level auth**: conditional rendering based on permissions

### 14.4 Security Best Practices
- **XSS prevention**: sanitizing user input, CSP headers
- **CSRF protection**: SameSite cookies, CSRF tokens
- **Clickjacking**: `X-Frame-Options`, CSP `frame-ancestors`
- **Secure headers**: HSTS, X-Content-Type-Options, Referrer-Policy
- **Dependency security**: `npm audit`, Snyk, Dependabot

### 14.5 Lab: Implement Enterprise-Grade Auth
- OAuth 2.0 with Auth.js
- Role-based route protection
- Secure session management
- CSP and security headers

---

## Module 15: Observability, Monitoring & Debugging

### 15.1 Frontend Observability
- **Real User Monitoring (RUM)**: Core Web Vitals from real users
- **Error tracking**: Sentry, LogRocket, Rollbar
- **Performance monitoring**: Web Vitals library, custom metrics
- **Session replay**: capturing user interactions for debugging

### 15.2 Next.js-Specific Monitoring
- **Server render metrics**: measuring RSC render time
- **Streaming metrics**: time to first chunk, streaming completion
- **Cache metrics**: hit rates, revalidation timing
- **Build metrics**: bundle size trends, build time monitoring

### 15.3 Logging Strategy
- **Structured logging**: JSON format, correlation IDs
- **Client-side logging**: batching, sampling, privacy
- **Server-side logging**: request logs, error logs, audit logs
- **Log aggregation**: centralized logging with ELK, Datadog, or Grafana

### 15.4 Debugging Methodology
- **React DevTools**: component tree, props, hooks, profiler
- **Network debugging**: HAR analysis, request/response inspection
- **Performance profiling**: Chrome DevTools Performance tab, flame graphs
- **Memory debugging**: heap snapshots, memory leaks in closures

### 15.5 Lab: Set Up Production Monitoring
- Integrate Sentry for error tracking
- Implement Web Vitals reporting
- Create a custom dashboard for frontend metrics
- Set up alerting for performance regressions

---

## Module 16: AI-Integrated Frontend Engineering

### 16.1 LLM Streaming Interfaces
- **Server-Sent Events (SSE)**: streaming text generation
- **WebSockets**: real-time bidirectional communication
- **React Suspense + streaming**: displaying LLM output progressively
- **Token-by-token rendering**: optimizing for perceived speed

### 16.2 AI-Powered UI Patterns
- **Chat interfaces**: message history, streaming responses, markdown rendering
- **Prompt engineering UIs**: templates, variables, preview
- **Agent interfaces**: tool calling, function results, streaming JSON
- **RAG interfaces**: source citations, document chunks, relevance scores

### 16.3 Performance for AI UIs
- **Virtualized chat**: rendering thousands of messages efficiently
- **Optimistic updates**: immediate UI feedback for AI actions
- **Skeleton states**: streaming placeholders for AI-generated content
- **Cancellation**: aborting in-flight AI requests

### 16.4 AI Developer Experience
- **AI-assisted code generation**: Copilot, Cursor, V0
- **Intelligent profiling**: AI-identified performance bottlenecks
- **Automated accessibility**: AI-powered a11y audits
- **Design-to-code**: AI converting designs to React components

### 16.5 Lab: Build an LLM Chat Interface
- Streaming response with SSE
- Markdown rendering with syntax highlighting
- Message virtualization for long conversations
- Optimistic updates for user messages

---

## Capstone Project

### Project: Production-Grade AI Dashboard Platform

Build a comprehensive dashboard platform for monitoring and interacting with AI/ML systems:

**Requirements:**
1. **Multi-tenant architecture**: Organization-based access control
2. **Real-time metrics**: WebSocket streaming for live training metrics
3. **LLM playground**: Chat interface with model selection, parameter tuning, and streaming responses
4. **Experiment tracking**: CRUD for ML experiments with server actions
5. **Performance targets**: LCP < 2s, INP < 200ms, CLS < 0.1
6. **Testing coverage**: >80% unit, integration tests for critical paths, E2E for core flows
7. **Monitoring**: Full observability with RUM, error tracking, and performance metrics
8. **Documentation**: Architecture Decision Records (ADRs), API documentation, deployment guide

**Architecture:**
- Next.js 15 App Router with React Server Components
- Feature-Sliced Design folder structure
- TanStack Query for server state, Zustand for client state
- Server Actions for mutations with optimistic updates
- Streaming for LLM responses and real-time metrics
- Comprehensive caching strategy with on-demand revalidation

---

## Appendix A: Reading List & References

### Foundational Computer Science
- *Structure and Interpretation of Computer Programs* — Abelson & Sussman
- *Introduction to Algorithms* — Cormen, Leiserson, Rivest, Stein
- *Category Theory for Programmers* — Bartosz Milewski

### React & Frontend Systems
- *React Design Patterns and Best Practices* — Michele Bertoli
- *Building Large-Scale Web Apps* — Addy Osmani
- *The Design of Web APIs* — Arnaud Lauret

### Next.js & Production
- Official Next.js Documentation (nextjs.org/docs)
- *Full Stack React TypeScript* — Nico Martin
- *Production-Ready Next.js* — Michele Riva

### Performance
- *High Performance Browser Networking* — Ilya Grigorik
- *Web Performance in Action* — Jeremy Wagner
- Google's Web Vitals documentation

### Systems & Architecture
- *Designing Data-Intensive Applications* — Martin Kleppmann
- *Building Micro-Frontends* — Michael Geers
- *Software Architecture: The Hard Parts* — Ford, Richards, Sadalage, Dehghani

---

## Appendix B: Tooling & Ecosystem

### Core Stack
- **Framework**: Next.js 15 (App Router)
- **Language**: TypeScript 5.x
- **Styling**: Tailwind CSS, CSS Modules
- **State**: TanStack Query, Zustand
- **Forms**: react-hook-form, zod
- **Testing**: Vitest, React Testing Library, Playwright

### Development Tools
- **Linting**: ESLint, Prettier
- **Git hooks**: Husky, lint-staged
- **Type checking**: tsc --noEmit
- **Bundle analysis**: @next/bundle-analyzer

### Deployment & Infrastructure
- **Platform**: Vercel, AWS, or self-hosted
- **CDN**: Cloudflare, Vercel Edge Network
- **Database**: PostgreSQL (Vercel Postgres, Supabase)
- **Monitoring**: Sentry, Datadog, Vercel Analytics

---

## Appendix C: Interview Preparation

### System Design: Frontend Architecture
- Design a real-time collaborative editor
- Design a video streaming platform frontend
- Design a social media feed with infinite scroll
- Design an e-commerce site with SSR and personalization

### React Deep Dives
- Explain React Fiber architecture and time slicing
- How does React's reconciliation algorithm work?
- When should you use Server Components vs Client Components?
- Design a caching strategy for a news application

### Performance Engineering
- How would you optimize LCP for a content-heavy page?
- What causes hydration mismatches and how do you fix them?
- Design a bundle optimization strategy for a large application
- How do you measure and improve INP?

### Coding Challenges
- Implement a virtualized list from scratch
- Build a custom hook for infinite scrolling
- Create a type-safe polymorphic component
- Implement a state machine with `useReducer`

---

## Course Timeline

| Phase | Duration | Modules | Focus |
|-------|----------|---------|-------|
| **Foundation** | 2 weeks | 0-1 | JavaScript, React basics, virtual DOM |
| **Core React** | 3 weeks | 2-4 | Fiber, hooks, TypeScript |
| **Next.js Deep Dive** | 4 weeks | 5-9 | App Router, RSC, streaming, caching |
| **Production Engineering** | 3 weeks | 10-13 | State management, performance, architecture |
| **Advanced Topics** | 2 weeks | 14-16 | Security, monitoring, AI integration |
| **Capstone** | 2 weeks | — | Production-grade project |

**Total Duration: 16 weeks (4 months) full-time, or 8 months part-time**

---

*This syllabus is a living document. The frontend ecosystem evolves rapidly. Always refer to the latest official documentation for React, Next.js, and related libraries. The principles of computer science, systems engineering, and architectural reasoning remain constant.*