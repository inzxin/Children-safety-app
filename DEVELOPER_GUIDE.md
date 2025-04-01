# Developer Guide: Kids Safety Learning App

This document provides technical details for developers who want to understand, modify, or extend the Kids Safety Learning App.

## Development Environment Setup

### Local Development

1. **Clone the repository**
```bash
git clone [repository-url]
cd kids-safety-app
```

2. **Install dependencies**
```bash
npm install
```

3. **Start the development server**
```bash
npm run dev
```

This starts:
- An Express server for the backend API
- A Vite development server for the React frontend
- Both run on the same port with API requests proxied to the Express server

### Key Development Files

- `package.json` - Project dependencies and scripts
- `vite.config.ts` - Vite configuration
- `tsconfig.json` - TypeScript configuration
- `tailwind.config.ts` - Tailwind CSS configuration
- `theme.json` - Application theme settings

## Architecture Overview

The application follows a modern full-stack JavaScript architecture:

### Frontend Architecture

- Built with React and TypeScript
- Uses functional components with React hooks
- State management primarily through React Query
- Routing via Wouter
- UI components from ShadCN UI and custom components
- Styling with Tailwind CSS
- Animations with Framer Motion

### Backend Architecture

- Express.js REST API
- TypeScript for type safety
- In-memory storage (can be replaced with a database)
- Zod for validation
- Shared types between frontend and backend

### Data Flow

1. React components make API requests through React Query
2. Requests are sent to Express endpoints
3. Express routes use the storage interface
4. Data is returned as JSON
5. React Query caches the responses
6. UI is updated with the data

## Key Components

### App Structure

- `App.tsx` - Main application component with the router
- `pages/*.tsx` - Page components
- `components/*.tsx` - Reusable UI components

### Data Model

The data model is defined in `shared/schema.ts` and includes:

- **Users**: Application users (children)
- **Topics**: Safety topics (fire, road, stranger, internet safety)
- **UserProgress**: Tracks user progress in topics
- **Badges**: Achievement badges
- **UserBadges**: Tracks which badges a user has earned
- **Games**: Mini-games related to safety topics
- **UserGames**: Tracks user progress in games
- **QuizQuestions**: Questions for topic quizzes
- **UserQuiz**: Tracks user quiz attempts

### API Endpoints

The API endpoints are defined in `server/routes.ts`:

- `/api/users/:id` - Get user information
- `/api/users` - Create a new user
- `/api/topics` - Get all safety topics
- `/api/users/:userId/topics` - Get topics with user progress
- `/api/progress` - Update user topic progress
- `/api/users/:userId/badges` - Get user badges
- `/api/badges` - Award a badge to a user
- `/api/games` - Get all games
- `/api/games/:id` - Get a specific game
- `/api/topics/:topicId/games` - Get games for a specific topic
- `/api/users/:userId/games` - Get games with user progress
- `/api/games/progress` - Update user game progress
- `/api/topics/:topicId/quiz` - Get quiz questions for a topic
- `/api/topics/:topicId/quiz/random` - Get a random quiz question
- `/api/quiz/answer` - Save a user's quiz answer
- `/api/users/:userId/topics/:topicId/quiz/results` - Get user quiz results

## UI Component Library

The application uses a combination of:

- **ShadCN UI Components**: Base components like buttons, forms, etc.
- **Custom Components**: Application-specific components

Key custom components:

- `Character.tsx` - Animated character with speech bubbles
- `SafetyTopics.tsx` - Topic selection grid
- `FeaturedActivity.tsx` - Featured activity card
- `GameSection.tsx` - Game listing component
- `BadgeItem.tsx` - Achievement badge display
- `BottomNavigation.tsx` - Mobile navigation bar

## Animation System

Animations are implemented with Framer Motion:

- Page transitions
- Component animations
- Interactive elements
- Feedback animations

Example animation pattern:
```tsx
<motion.div
  initial={{ opacity: 0, y: 20 }}
  animate={{ opacity: 1, y: 0 }}
  transition={{ duration: 0.5 }}
>
  {/* Component content */}
</motion.div>
```

## State Management

The application uses:

- **React Query**: For server state (API data)
- **React useState/useReducer**: For local component state
- **Custom hooks**: For shared logic

### Example React Query Pattern

```tsx
// Define query
const { data: topics, isLoading } = useQuery({
  queryKey: ['/api/topics'],
});

// Define mutation
const mutation = useMutation({
  mutationFn: (data) => apiRequest('/api/progress', 'POST', data),
  onSuccess: () => {
    // Invalidate queries that should refetch
    queryClient.invalidateQueries({ queryKey: ['/api/users', userId, 'topics'] });
  },
});
```

## Extending the Application

### Adding a New Safety Topic

1. Add the topic data in `server/storage.ts` initializeDefaultData function
2. Create related games, badges, and quiz questions
3. Update the UI components to display the new topic

### Adding a New Game Type

1. Add the game data in `server/storage.ts`
2. Create a new game component in the client
3. Add routing for the new game
4. Implement game logic and UI

### Implementing Database Storage

To replace the in-memory storage with a database:

1. Update `server/storage.ts` to implement the IStorage interface with your database
2. Create database migration files if needed
3. Update environment variables for database connection

## Deployment

### Build Process

```bash
npm run build
```

This creates:
- Frontend static files in the `dist` directory
- Compiled backend files

### Deployment Options

- **Replit**: Use the Deploy button
- **Vercel/Netlify**: Connect to GitHub repository
- **Traditional hosting**: Deploy dist folder and run server

### Environment Variables

- `PORT`: Server port (defaults to 5000)
- `NODE_ENV`: Environment (development/production)

## Best Practices

### Coding Standards

- Use TypeScript types for all functions and components
- Follow React hooks rules
- Use the shared schema for data validation
- Keep components small and focused
- Use consistent naming conventions

### Performance Considerations

- Use React Query's caching to minimize API calls
- Implement proper loading states
- Optimize animations for mobile devices
- Lazy load page components
- Minimize dependencies

### Accessibility

- Maintain proper contrast ratios
- Use semantic HTML
- Provide alternative text for images
- Make sure the application is keyboard navigable
- Test with screen readers

## Troubleshooting

### Common Issues

- **API returns 404**: Check route paths and method (GET/POST)
- **React Query not updating**: Check invalidation keys
- **CSS not applying**: Check for conflicting Tailwind classes
- **Animations not working**: Check if framer-motion is properly installed

### Debugging Tools

- Browser Developer Tools
- React Developer Tools
- Network monitoring for API requests
- Console logs on both client and server

## Resources

- [React Documentation](https://reactjs.org/docs/getting-started.html)
- [TypeScript Documentation](https://www.typescriptlang.org/docs/)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [Framer Motion Documentation](https://www.framer.com/motion/)
- [TanStack Query Documentation](https://tanstack.com/query/latest)
- [Express.js Documentation](https://expressjs.com/)

---

This guide covers the core technical aspects of the Kids Safety Learning App. For more detailed information on specific components or features, refer to the code comments and README files in the respective directories.