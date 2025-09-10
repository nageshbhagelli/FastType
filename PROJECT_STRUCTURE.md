# FastType - Project Structure

## 📁 Current Project Structure

```
fasttype/
├── PROJECT_STRUCTURE.md           # This file - project organization guide
├── ROADMAP.md                     # Development roadmap and phases
├── README.md                      # Project documentation
├── .gitignore                     # Git ignore rules
├── docker-compose.yml             # Docker configuration
├── package.json                   # Root package.json for workspace
└── docs/                          # Documentation
    ├── api/                       # API documentation
    ├── deployment/                # Deployment guides
    └── design/                    # UI/UX design specs
```

## 🎯 Planned Full Structure (To be created during development)

```
fasttype/
├── PROJECT_STRUCTURE.md           # ✅ This file
├── ROADMAP.md                     # 📋 Development roadmap
├── README.md                      # 📖 Project documentation
├── .gitignore                     # 🚫 Git ignore rules
├── docker-compose.yml             # 🐳 Docker configuration
├── package.json                   # 📦 Root workspace config
│
├── frontend/                      # 🎨 React TypeScript Frontend
│   ├── public/
│   │   ├── index.html
│   │   ├── favicon.ico
│   │   └── manifest.json
│   ├── src/
│   │   ├── components/            # React components
│   │   │   ├── TypingTest/
│   │   │   │   ├── TypingArea.tsx
│   │   │   │   ├── TextDisplay.tsx
│   │   │   │   ├── Caret.tsx
│   │   │   │   └── index.ts
│   │   │   ├── Statistics/
│   │   │   │   ├── StatsBar.tsx
│   │   │   │   ├── ResultsModal.tsx
│   │   │   │   ├── PerformanceChart.tsx
│   │   │   │   └── index.ts
│   │   │   ├── Settings/
│   │   │   │   ├── SettingsPanel.tsx
│   │   │   │   ├── ThemeSelector.tsx
│   │   │   │   ├── TestModeSelector.tsx
│   │   │   │   └── index.ts
│   │   │   ├── Auth/
│   │   │   │   ├── LoginForm.tsx
│   │   │   │   ├── RegisterForm.tsx
│   │   │   │   ├── UserProfile.tsx
│   │   │   │   └── index.ts
│   │   │   ├── UI/
│   │   │   │   ├── Button.tsx
│   │   │   │   ├── Modal.tsx
│   │   │   │   ├── CommandPalette.tsx
│   │   │   │   ├── Header.tsx
│   │   │   │   ├── Footer.tsx
│   │   │   │   └── index.ts
│   │   │   └── Layout/
│   │   │       ├── MainLayout.tsx
│   │   │       ├── AuthLayout.tsx
│   │   │       └── index.ts
│   │   ├── hooks/                 # Custom React hooks
│   │   │   ├── useTypingTest.ts
│   │   │   ├── useKeyboard.ts
│   │   │   ├── useStats.ts
│   │   │   ├── useTheme.ts
│   │   │   ├── useAuth.ts
│   │   │   └── useLocalStorage.ts
│   │   ├── stores/                # State management
│   │   │   ├── typingStore.ts
│   │   │   ├── userStore.ts
│   │   │   ├── settingsStore.ts
│   │   │   └── index.ts
│   │   ├── utils/                 # Utility functions
│   │   │   ├── calculations.ts    # WPM, accuracy calculations
│   │   │   ├── textGenerator.ts   # Text generation logic
│   │   │   ├── keyboardUtils.ts   # Keyboard event handling
│   │   │   ├── validation.ts      # Input validation
│   │   │   ├── formatters.ts      # Data formatting
│   │   │   └── constants.ts       # App constants
│   │   ├── types/                 # TypeScript type definitions
│   │   │   ├── typing.ts
│   │   │   ├── user.ts
│   │   │   ├── stats.ts
│   │   │   ├── settings.ts
│   │   │   └── api.ts
│   │   ├── styles/                # Styling files
│   │   │   ├── globals.css
│   │   │   ├── themes/
│   │   │   │   ├── dark.css
│   │   │   │   ├── light.css
│   │   │   │   ├── monokai.css
│   │   │   │   └── index.ts
│   │   │   └── components/        # Component-specific styles
│   │   ├── data/                  # Static data
│   │   │   ├── wordLists/
│   │   │   │   ├── english-200.json
│   │   │   │   ├── english-1000.json
│   │   │   │   └── quotes.json
│   │   │   └── languages/
│   │   ├── assets/                # Static assets
│   │   │   ├── images/
│   │   │   ├── sounds/
│   │   │   └── fonts/
│   │   ├── App.tsx                # Main App component
│   │   ├── main.tsx               # Entry point
│   │   └── vite-env.d.ts          # Vite type definitions
│   ├── package.json               # Frontend dependencies
│   ├── tsconfig.json              # TypeScript config
│   ├── vite.config.ts             # Vite configuration
│   ├── tailwind.config.js         # Tailwind CSS config
│   ├── postcss.config.js          # PostCSS config
│   └── .env.example               # Environment variables template
│
├── backend/                       # 🚀 Node.js Express Backend
│   ├── src/
│   │   ├── routes/                # API routes
│   │   │   ├── auth.ts
│   │   │   ├── users.ts
│   │   │   ├── tests.ts
│   │   │   ├── leaderboards.ts
│   │   │   └── index.ts
│   │   ├── controllers/           # Route controllers
│   │   │   ├── authController.ts
│   │   │   ├── userController.ts
│   │   │   ├── testController.ts
│   │   │   └── leaderboardController.ts
│   │   ├── middleware/            # Express middleware
│   │   │   ├── auth.ts
│   │   │   ├── validation.ts
│   │   │   ├── errorHandler.ts
│   │   │   ├── rateLimit.ts
│   │   │   └── cors.ts
│   │   ├── models/                # Database models (if using non-Prisma)
│   │   │   └── index.ts
│   │   ├── services/              # Business logic
│   │   │   ├── authService.ts
│   │   │   ├── userService.ts
│   │   │   ├── testService.ts
│   │   │   └── statisticsService.ts
│   │   ├── utils/                 # Backend utilities
│   │   │   ├── jwt.ts
│   │   │   ├── bcrypt.ts
│   │   │   ├── validation.ts
│   │   │   ├── logger.ts
│   │   │   └── database.ts
│   │   ├── types/                 # Backend type definitions
│   │   │   ├── auth.ts
│   │   │   ├── user.ts
│   │   │   ├── test.ts
│   │   │   └── api.ts
│   │   ├── config/                # Configuration files
│   │   │   ├── database.ts
│   │   │   ├── jwt.ts
│   │   │   └── environment.ts
│   │   ├── app.ts                 # Express app setup
│   │   └── server.ts              # Server entry point
│   ├── prisma/                    # Database schema and migrations
│   │   ├── schema.prisma
│   │   ├── migrations/
│   │   └── seed.ts
│   ├── tests/                     # Backend tests
│   │   ├── unit/
│   │   ├── integration/
│   │   └── e2e/
│   ├── package.json               # Backend dependencies
│   ├── tsconfig.json              # TypeScript config
│   ├── .env.example               # Environment variables template
│   └── Dockerfile                 # Docker configuration
│
├── shared/                        # 🔄 Shared types and utilities
│   ├── types/                     # Shared TypeScript types
│   │   ├── user.ts
│   │   ├── test.ts
│   │   ├── stats.ts
│   │   └── api.ts
│   ├── utils/                     # Shared utility functions
│   │   ├── calculations.ts
│   │   ├── validation.ts
│   │   └── constants.ts
│   └── package.json               # Shared package config
│
├── docs/                          # 📚 Documentation
│   ├── api/                       # API documentation
│   │   ├── openapi.yaml
│   │   ├── endpoints.md
│   │   └── authentication.md
│   ├── deployment/                # Deployment guides
│   │   ├── docker.md
│   │   ├── production.md
│   │   └── environment.md
│   ├── development/               # Development guides
│   │   ├── setup.md
│   │   ├── contributing.md
│   │   └── testing.md
│   └── design/                    # Design specifications
│       ├── ui-components.md
│       ├── themes.md
│       └── user-flow.md
│
├── scripts/                       # 🛠️ Build and deployment scripts
│   ├── build.sh
│   ├── deploy.sh
│   ├── setup-dev.sh
│   └── test.sh
│
└── tests/                         # 🧪 End-to-end tests
    ├── e2e/
    │   ├── typing-test.spec.ts
    │   ├── user-auth.spec.ts
    │   └── settings.spec.ts
    ├── fixtures/
    └── playwright.config.ts
```

## 📋 Development Phase Structure

### Phase 1: Foundation (Weeks 1-2)
```
fasttype/
├── frontend/src/
│   ├── components/TypingTest/     # Basic typing components
│   ├── utils/calculations.ts      # WPM calculations
│   ├── hooks/useTypingTest.ts     # Core typing logic
│   └── styles/globals.css         # Basic styling
```

### Phase 2: Enhanced Functionality (Weeks 3-4)
```
fasttype/
├── frontend/src/
│   ├── components/Statistics/     # Stats and charts
│   ├── components/Settings/       # Customization panel
│   ├── stores/                    # State management
│   └── data/wordLists/           # Word lists and quotes
```

### Phase 3: Backend & User System (Weeks 5-6)
```
fasttype/
├── backend/                       # Complete backend structure
├── shared/                        # Shared types
└── frontend/src/components/Auth/  # Authentication UI
```

### Phase 4: Advanced Features (Weeks 7-8)
```
fasttype/
├── frontend/src/components/UI/CommandPalette.tsx
├── backend/src/routes/leaderboards.ts
└── docs/                          # Complete documentation
```

## 🔄 Update Instructions

This file should be updated at the end of each development phase to reflect:

1. **Completed Structure**: Mark completed directories/files with ✅
2. **In Progress**: Mark current work with 🚧
3. **Planned**: Keep future items unmarked
4. **Changes**: Document any structural changes from the original plan

## 📝 Notes

- **Monorepo Structure**: Using a monorepo approach for better code sharing
- **TypeScript**: Consistent TypeScript usage across frontend and backend
- **Modular Design**: Components and utilities are highly modular for maintainability
- **Testing**: Comprehensive testing structure for quality assurance
- **Documentation**: Extensive documentation for development and deployment

## 🎯 Next Steps

1. Initialize the basic project structure (Phase 1)
2. Set up the frontend React + TypeScript project
3. Configure Tailwind CSS and basic styling
4. Create the core typing test components
5. Update this file as development progresses

---

**Last Updated**: 2025-09-10 22:13:32 IST  
**Phase**: Planning & Structure Definition  
**Status**: Project structure defined, ready for implementation
