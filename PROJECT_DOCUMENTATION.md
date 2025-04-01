# Kids Safety Learning App 🛡️

A mobile-friendly interactive web application designed to teach children aged 6-12 about important safety topics.

## Overview

This application provides an engaging platform for children to learn safety concepts through:
- Interactive lessons
- Fun mini-games
- Achievement badges
- Progress tracking
- Child-friendly user interface

## Project Structure

The project follows a fullstack JavaScript architecture with client and server components:

```
├── client/                  # Frontend React application
│   ├── src/
│   │   ├── components/      # Reusable UI components
│   │   ├── hooks/           # Custom React hooks
│   │   ├── lib/             # Utility functions and services
│   │   ├── pages/           # Page components for routing
│   │   ├── App.tsx          # Main application component
│   │   └── main.tsx         # Entry point for the React app
│   └── index.html           # HTML template
├── server/                  # Backend Express application
│   ├── index.ts             # Express server setup
│   ├── routes.ts            # API endpoint definitions
│   ├── storage.ts           # Data storage implementation
│   └── vite.ts              # Vite server integration
├── shared/                  # Shared code between client and server
│   └── schema.ts            # Database schema and types
└── package.json             # Project dependencies and scripts
```

## Technologies Used

### Frontend
- **React**: UI library for building the interface
- **TypeScript**: Type-safe JavaScript
- **Tailwind CSS**: Utility-first CSS framework
- **Framer Motion**: Animation library
- **Wouter**: Lightweight routing
- **React Hook Form**: Form state management
- **TanStack React Query**: Data fetching and caching
- **ShadCN UI**: Component library

### Backend
- **Node.js**: JavaScript runtime
- **Express**: Web server framework
- **Drizzle ORM**: Database ORM
- **Zod**: Schema validation

## Safety Topics Covered

The application covers several essential safety topics for children:

1. **Fire Safety** 🔥
   - Fire prevention
   - How to respond to fires
   - Evacuation planning
   - Stop, drop, and roll

2. **Road Safety** 🚦
   - Crossing streets safely
   - Traffic signals
   - Pedestrian safety
   - Bicycle safety

3. **Stranger Safety** 👥
   - Identifying trusted adults
   - What to do if approached by strangers
   - Safe places to seek help
   - Personal boundaries

4. **Internet Safety** 💻
   - Online privacy
   - Appropriate online behavior
   - Recognizing online dangers
   - Reporting suspicious activity

## Features

### Interactive Learning
- Engaging lessons with animated characters
- Simple, age-appropriate explanations
- Progress tracking across topics

### Gamification
- Mini-games that reinforce safety concepts
- Achievement badges for completing activities
- Star ratings to encourage replaying games

### Child-Friendly Design
- Colorful, appealing interface
- Simple navigation suitable for young users
- Animated feedback and encouragement
- Audio support for non-readers

## Running the Application Locally

### Prerequisites
- Node.js (version 18 or 20)
- npm (comes with Node.js)

### Installation Steps

1. Clone or download the project
```bash
# If using git
git clone [repository-url]

# If downloaded as ZIP
# Extract the ZIP file to a folder
```

2. Navigate to the project directory
```bash
cd kids-safety-app
```

3. Install dependencies
```bash
npm install
```

4. Start the development server
```bash
npm run dev
```

5. Open your browser and navigate to http://localhost:5000

## Data Storage

The application currently uses in-memory storage, which means:
- Data is not persistent between server restarts
- Suitable for development and demonstration
- For production use, a database implementation would be needed

## Color Scheme

The application uses a topic-based color scheme:
- **Fire Safety**: Red/Orange (#FF6B4A)
- **Road Safety**: Green (#4AFF6B)
- **Stranger Safety**: Yellow/Gold (#FFC04A)
- **Internet Safety**: Blue (#4A6BFF)

## Future Enhancements

Potential areas for expansion:
- Additional safety topics
- Parent/teacher dashboard
- More complex games
- Multi-language support
- Accessibility improvements
- Integration with educational standards

## License

This project is intended for educational purposes.

---

Created with ❤️ for child safety education