## Phase 1: Core Foundation (P0 - Critical)

  ### Authentication
  - [ ] Connect login screen to backend API
  - [ ] Connect register screen to backend API
  - [ ] JWT token storage in expo-secure-store
  - [ ] Auto-login on app relaunch
  - [ ] Logout functionality
  - [ ] Handle auth errors (invalid credentials, network errors)

  ### Achievement CRUD
  - [ ] Fetch achievements with React Query
  - [ ] Create achievement via POST mutation
  - [ ] Edit achievement via PUT mutation
  - [ ] Delete (soft delete) via DELETE mutation
  - [ ] Optimistic updates for instant feedback

  ### Error Handling
  - [ ] Error boundaries for crash protection
  - [ ] API error handling (401 → logout)
  - [ ] Network error handling with user message
  - [ ] Form validation (required fields, input limits)
  - [ ] User-friendly error messages

  ### Loading & Empty States
  - [ ] Loading spinners/skeletons during fetches
  - [ ] Empty state for "No achievements yet"
  - [ ] Pull-to-refresh with actual refetch

  ## Phase 2: Discovery & UX (P1 - Important)

  ### Client-Side Search
  - [ ] Filter cached achievements by title/description
  - [ ] Debounced input (300ms)
  - [ ] Search results highlighting
  - [ ] Persist recent searches locally

  ### Category Filtering
  - [ ] Filter achievements by selected category
  - [ ] Clear filter option
  - [ ] Badge counts per category

  ### Toast Notifications
  - [ ] Install react-native-toast-message
  - [ ] Replace alert() with toast
  - [ ] Success/error/info toast variants

  ### Profile
  - [ ] Real stats from API (total, this month, categories)

  ## Phase 3: Push Notifications (P1 - User Priority)

  - [ ] Install expo-notifications
  - [ ] Request permission on first launch
  - [ ] Get and store push token
  - [ ] Register token with backend
  - [ ] Handle incoming notifications
  - [ ] Weekly achievement reminder

  ## Already Complete ✅

  - [x] All screen UI mockups (login, register, achievements, search, categories, profile)
  - [x] Dark mode support (system preference detection)
  - [x] Bottom tab navigation
  - [x] Expo Router file-based routing
  - [x] TanStack Query + Zustand infrastructure setup
  - [x] API client configuration (ready but unused)
  - [x] TypeScript type definitions
  - [x] NativeWind/Tailwind styling
  - [x] Category color-coding system


in0410