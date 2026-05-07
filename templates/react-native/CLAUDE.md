# CLAUDE.md — React Native / Expo

## Project overview
[Project name] is a [brief description]. Built with React Native (Expo) and TypeScript.

## Tech stack
- **Framework:** React Native + Expo (managed workflow)
- **Language:** TypeScript (strict mode)
- **Navigation:** Expo Router (file-based)
- **State:** Zustand (global), React Query (server state)
- **Styling:** NativeWind (Tailwind for RN) / StyleSheet.create
- **API:** REST / GraphQL with code generation
- **Storage:** expo-secure-store (sensitive), AsyncStorage (preferences)
- **Testing:** Jest + React Native Testing Library + Detox (e2e)

## Project structure
```
src/
├── app/                # Expo Router screens and layouts
│   ├── (tabs)/         # Tab navigator group
│   ├── (auth)/         # Auth flow screens
│   ├── _layout.tsx     # Root layout
│   └── index.tsx       # Entry screen
├── components/
│   ├── ui/             # Reusable primitives (Button, Input, Card)
│   └── features/       # Feature-specific components
├── hooks/              # Custom hooks
├── lib/                # API client, utilities, constants
├── stores/             # Zustand stores
├── types/              # TypeScript definitions
└── assets/             # Images, fonts
```

## Development commands
```bash
npx expo start           # Start Expo dev server
npx expo start --ios     # Start on iOS simulator
npx expo start --android # Start on Android emulator
npm run lint             # ESLint
npm run test             # Jest tests
npm run test:e2e         # Detox e2e tests
npx expo prebuild        # Generate native projects
eas build                # Cloud build for distribution
```

## Code style and conventions
- Functional components only
- File naming: `kebab-case.tsx`
- Use Expo SDK modules over bare RN or third-party when available
- Platform-specific code: `*.ios.tsx` / `*.android.tsx` only when necessary
- Avoid inline styles — use `StyleSheet.create` or NativeWind classes
- Navigation: use typed routes with Expo Router's `useRouter` and `Link`
- No `any` types — define proper types for navigation params, API responses

## Mobile-specific patterns
- Lists: always use `FlashList` or `FlatList`, never `ScrollView` for dynamic data
- Images: use `expo-image` with caching, specify width/height
- Keyboard: wrap forms in `KeyboardAvoidingView` with platform-specific behavior
- Safe areas: use `SafeAreaView` from `react-native-safe-area-context`
- Haptics: use `expo-haptics` for tactile feedback on important actions
- Deep links: configure in `app.json` and handle in root layout

## Offline and data
- React Query with `persistQueryClient` for offline-first reads
- Optimistic updates for mutations
- Network status: `@react-native-community/netinfo` to show offline banner
- Sensitive tokens in `expo-secure-store`, preferences in `AsyncStorage`
- Never store sensitive data in AsyncStorage

## Performance
- Memoize expensive list items with `React.memo`
- Avoid anonymous functions in `renderItem`
- Use `useCallback` for event handlers passed to lists
- Lazy load screens with `React.lazy` + Suspense
- Profile with Flipper / React DevTools — fix re-renders before adding memoization

## Testing
- Unit: hooks and utilities with Jest
- Component: render with RNTL, test user interactions
- E2e: Detox for critical flows (onboarding, auth, purchase)
- Mock native modules in `jest.setup.ts`
- Test on both iOS and Android — platform bugs are real
