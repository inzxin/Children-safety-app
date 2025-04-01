# Code Overview: Kids Safety Learning App

This document provides a quick reference to the main files in the project with brief code explanations.

## Client Side (Frontend)

### Main Application Files

#### `client/src/main.tsx`
```tsx
// Entry point for the React application
// Sets up React Query provider and renders the App component
```

#### `client/src/App.tsx`
```tsx
// Main application component
// Sets up routing with Wouter
// Renders the main layout with navigation

function Router() {
  // Defines all application routes
  // Maps URL paths to page components
}

function App() {
  // Main app component
  // Includes Router, Toaster, and other global components
}
```

#### `client/src/index.css`
```css
/* Main stylesheet with Tailwind imports */
/* Custom global styles and animations */
/* Typography settings including font-family definitions */
```

### Page Components

#### `client/src/pages/home.tsx`
```tsx
// Home page component
// Shows welcome section, featured activities, and topic previews
// Entry point for user navigation
```

#### `client/src/pages/learn.tsx`
```tsx
// Learning topics page
// Displays all safety topics with progress indicators
// Organizes topics into a grid layout
```

#### `client/src/pages/topic.tsx`
```tsx
// Individual topic page
// Shows content for a specific safety topic
// Includes quizzes, games, and learning materials
```

#### `client/src/pages/game.tsx`
```tsx
// Game page component
// Renders different game types based on game ID
// Handles game state, user input, and scoring
```

#### `client/src/pages/badges.tsx`
```tsx
// Badges collection page
// Shows all possible badges and which ones user has earned
// Displays badge details and requirements
```

#### `client/src/pages/profile.tsx`
```tsx
// User profile page
// Shows user stats, progress, and achievements
// Allows customization of profile settings
```

### Key Components

#### `client/src/components/character.tsx`
```tsx
// Animated character component
// Displays mascot with different moods and animations
// Includes speech bubble functionality

interface CharacterProps {
  className?: string;
  animate?: boolean;
  speechText?: string;
  size?: 'sm' | 'md' | 'lg';
  mood?: 'happy' | 'neutral' | 'thinking' | 'excited' | 'waving';
}
```

#### `client/src/components/welcome-section.tsx`
```tsx
// Welcome component for home page
// Shows personalized greeting and recent badges
// Includes character with speech bubble

interface WelcomeSectionProps {
  userName: string;
  badges: BadgeWithDetails[];
  className?: string;
}
```

#### `client/src/components/safety-topics.tsx`
```tsx
// Grid of safety topic cards
// Shows topic progress and icon
// Handles navigation to topic pages

interface SafetyTopicsProps {
  topics: TopicWithProgress[];
  className?: string;
}
```

#### `client/src/components/featured-activity.tsx`
```tsx
// Featured activity component
// Highlights recommended content for user
// Shows attractive preview with animation

interface FeaturedActivityProps {
  topicId: number;
  className?: string;
}
```

#### `client/src/components/game-section.tsx`
```tsx
// Displays available games
// Shows completion status and rating
// Links to game play pages

interface GameSectionProps {
  games: GameWithProgress[];
  className?: string;
}
```

#### `client/src/components/bottom-navigation.tsx`
```tsx
// Mobile navigation bar
// Fixed to bottom of screen with animated tabs
// Handles navigation between main sections
```

#### `client/src/components/header.tsx`
```tsx
// Page header component
// Shows title, progress, and notifications
// Consistent across pages

interface HeaderProps {
  userName?: string;
  progress: number;
  notifications?: number;
  className?: string;
}
```

### Utility Functions

#### `client/src/lib/queryClient.ts`
```tsx
// Sets up React Query client
// Defines API request utilities
// Handles error responses

export async function apiRequest(
  url: string,
  method = "GET",
  data?: unknown
) {
  // Handles API requests with error checking
}

export const queryClient = new QueryClient({
  // Configuration settings for React Query
});
```

#### `client/src/lib/audio.ts`
```ts
// Audio management system
// Handles sound effects and background music
// Text-to-speech for narration

type AudioType = 'buttonClick' | 'celebration' | 'correct' | 'incorrect' | 'background' | 'narration';

class AudioManager {
  // Methods to play different audio types
  // Controls volume and enables/disables audio
}
```

#### `client/src/lib/utils.ts`
```ts
// General utility functions
// Includes className merging with clsx
// Helper functions for data formatting

export function cn(...inputs: ClassValue[]) {
  // Merges Tailwind classes
}
```

## Server Side (Backend)

### Main Server Files

#### `server/index.ts`
```ts
// Express server setup
// Configures middleware and error handling
// Initializes storage and routes
```

#### `server/routes.ts`
```ts
// API endpoint definitions
// Route handlers for data operations
// Validation of request data

export async function registerRoutes(app: Express): Promise<Server> {
  // Registers all API routes
  // Returns HTTP server
}
```

#### `server/storage.ts`
```ts
// Data storage implementation
// Uses in-memory storage (Map objects)
// Implements IStorage interface

export interface IStorage {
  // Defines all data access methods
  // User, Topic, Progress, Badge, Game, Quiz operations
}

export class MemStorage implements IStorage {
  // In-memory implementation of storage interface
  // Uses Maps to store data
  // Includes default data initialization
}
```

### Shared Files

#### `shared/schema.ts`
```ts
// Database schema definitions
// Type definitions for data models
// Zod schemas for validation

// Table definitions with Drizzle
export const users = pgTable("users", { /* columns */ });
export const topics = pgTable("topics", { /* columns */ });
// ... other tables

// Type definitions
export type User = typeof users.$inferSelect;
export type Topic = typeof topics.$inferSelect;
// ... other types

// Extended types with relationships
export type TopicWithProgress = Topic & { progress: number };
export type BadgeWithDetails = Badge & { unlocked: boolean, earnedAt?: Date };
// ... other extended types
```

## Configuration Files

#### `vite.config.ts`
```ts
// Vite bundler configuration
// Sets up development server
// Configures plugins and build settings
```

#### `tsconfig.json`
```json
// TypeScript configuration
// Sets compiler options
// Defines path aliases
```

#### `tailwind.config.ts`
```ts
// Tailwind CSS configuration
// Custom theme settings
// Plugin configurations
```

#### `theme.json`
```json
// Application theme settings
// Defines primary colors and appearance
// Controls UI styling variables
```

#### `drizzle.config.ts`
```ts
// Drizzle ORM configuration
// Database connection settings
// Migration settings
```

## Important Concepts

### Data Flow
1. User interacts with UI
2. React component uses React Query to fetch/update data
3. Request goes to Express API endpoint
4. API handler uses storage interface
5. Data is returned to frontend
6. React Query caches result and updates UI

### Component Hierarchy
- App (Root)
  - Router
    - Page Components (Home, Learn, Topic, etc.)
      - Shared Components (Header, BottomNavigation)
      - Page-specific Components (WelcomeSection, SafetyTopics, etc.)
        - UI Components (Buttons, Cards, Inputs, etc.)

### State Management
- Server state: React Query
- UI state: React useState/useReducer
- Form state: React Hook Form
- Animations: Framer Motion

This overview should help you navigate the codebase and understand how the different pieces fit together.