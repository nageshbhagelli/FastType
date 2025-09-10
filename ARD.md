# FastType - Architecture Requirements Document (ARD)

**Document Version**: 1.0  
**Created**: 2025-09-10  
**Last Updated**: 2025-09-10  
**Author**: Development Team  
**Status**: Draft  

---

## 📋 Executive Summary

This Architecture Requirements Document (ARD) defines the technical architecture, system design, and implementation strategy for FastType, a modern typing test web application. The architecture emphasizes performance, scalability, maintainability, and user experience.

### Architecture Goals
- **Performance**: Sub-50ms keystroke latency with real-time feedback
- **Scalability**: Support 10,000+ concurrent users
- **Maintainability**: Modular, testable, and well-documented codebase
- **Security**: Secure user data handling and authentication
- **Accessibility**: WCAG 2.1 AA compliant design

---

## 🏗️ System Architecture Overview

### Architecture Pattern
**Microservices-Inspired Monolith**: Modular monolithic architecture with clear service boundaries, enabling future microservices migration if needed.

### Deployment Model
**Containerized Multi-Tier**: Separate containers for frontend, backend, and database with orchestrated deployment.

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Frontend      │    │    Backend      │    │    Database     │
│   (React SPA)   │◄──►│  (Node.js API)  │◄──►│  (PostgreSQL)   │
│   Port: 3000    │    │   Port: 5000    │    │   Port: 5432    │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         ▼                       ▼                       ▼
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│     Vercel      │    │    Railway      │    │   Railway DB    │
│  (Production)   │    │  (Production)   │    │  (Production)   │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

---

## 🎯 Technical Stack & Justification

### Frontend Stack

#### Core Framework
- **React 18.2+** with **TypeScript 5.0+**
  - *Justification*: Mature ecosystem, excellent TypeScript support, concurrent features for smooth UI
  - *Alternatives Considered*: Vue.js, Svelte (chosen React for ecosystem and team expertise)

#### Build & Development Tools
- **Vite 4.0+**: Fast development server and optimized production builds
- **Tailwind CSS 3.0+**: Utility-first CSS for rapid UI development
- **ESLint + Prettier**: Code quality and formatting consistency

#### State Management
- **Zustand**: Lightweight state management for typing test state
  - *Justification*: Simpler than Redux, better performance than Context API for frequent updates
  - *Alternative*: Redux Toolkit (overkill for current requirements)

#### UI & Visualization
- **Lucide React**: Consistent icon library
- **Chart.js 4.0+**: Performance charts and statistics visualization
- **Framer Motion**: Smooth animations for caret and UI transitions

### Backend Stack

#### Runtime & Framework
- **Node.js 18+ LTS** with **Express.js 4.18+**
  - *Justification*: JavaScript ecosystem consistency, excellent performance for I/O operations
  - *Alternatives Considered*: Python/FastAPI, Go/Gin (chosen Node.js for team consistency)

#### Database & ORM
- **PostgreSQL 15+**: Primary database for user data and statistics
- **Prisma 5.0+**: Type-safe database access and migrations
  - *Justification*: Excellent TypeScript integration, automatic migrations, query optimization

#### Authentication & Security
- **JWT (jsonwebtoken)**: Stateless authentication tokens
- **bcrypt**: Password hashing
- **helmet**: Security headers
- **cors**: Cross-origin resource sharing configuration

### Infrastructure & DevOps

#### Containerization
- **Docker**: Application containerization
- **Docker Compose**: Local development orchestration

#### Deployment
- **Frontend**: Vercel (optimized for React, global CDN)
- **Backend**: Railway (simple deployment, integrated database)
- **Database**: Railway PostgreSQL (managed service)

#### Monitoring & Analytics
- **Sentry**: Error tracking and performance monitoring
- **Google Analytics 4**: User behavior analytics
- **Uptime Robot**: Service availability monitoring

---

## 🏛️ System Architecture Design

### Frontend Architecture

#### Component Architecture
```
src/
├── components/
│   ├── TypingTest/          # Core typing functionality
│   │   ├── TypingArea.tsx   # Main typing interface
│   │   ├── TextDisplay.tsx  # Text rendering with highlighting
│   │   ├── Caret.tsx        # Animated typing caret
│   │   └── InputHandler.tsx # Keyboard event processing
│   ├── Statistics/          # Performance tracking
│   │   ├── StatsBar.tsx     # Real-time stats display
│   │   ├── ResultsModal.tsx # Post-test results
│   │   └── Charts/          # Performance visualization
│   ├── Settings/            # User preferences
│   └── Auth/                # Authentication UI
├── hooks/                   # Custom React hooks
│   ├── useTypingTest.ts     # Core typing logic
│   ├── useKeyboard.ts       # Keyboard event handling
│   ├── useStats.ts          # Statistics calculations
│   └── usePerformance.ts    # Performance optimization
├── stores/                  # State management
│   ├── typingStore.ts       # Typing test state
│   ├── userStore.ts         # User session state
│   └── settingsStore.ts     # User preferences
└── utils/                   # Utility functions
    ├── calculations.ts      # WPM, accuracy algorithms
    ├── textGenerator.ts     # Test text generation
    └── performance.ts       # Performance utilities
```

#### State Management Strategy
```typescript
// Typing Test State (Zustand)
interface TypingState {
  // Test Configuration
  mode: 'time' | 'words' | 'quote' | 'custom';
  duration: number;
  wordCount: number;
  
  // Test Progress
  currentText: string;
  userInput: string;
  currentIndex: number;
  startTime: number | null;
  endTime: number | null;
  
  // Real-time Statistics
  wpm: number;
  rawWpm: number;
  accuracy: number;
  consistency: number;
  
  // Actions
  startTest: () => void;
  updateInput: (input: string) => void;
  completeTest: () => void;
  resetTest: () => void;
}
```

### Backend Architecture

#### Service Layer Architecture
```
src/
├── routes/                  # API endpoint definitions
│   ├── auth.ts             # Authentication endpoints
│   ├── tests.ts            # Test management
│   ├── users.ts            # User management
│   └── leaderboards.ts     # Competition features
├── controllers/            # Request handling logic
├── services/               # Business logic layer
│   ├── AuthService.ts      # Authentication logic
│   ├── TestService.ts      # Test processing
│   ├── UserService.ts      # User management
│   └── StatsService.ts     # Statistics calculations
├── middleware/             # Express middleware
│   ├── auth.ts            # JWT verification
│   ├── validation.ts      # Request validation
│   ├── rateLimit.ts       # Rate limiting
│   └── errorHandler.ts    # Error processing
└── utils/                 # Utility functions
    ├── jwt.ts             # Token management
    ├── validation.ts      # Data validation
    └── calculations.ts    # Server-side calculations
```

#### Database Schema Design
```sql
-- Users table
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  email VARCHAR(255) UNIQUE NOT NULL,
  username VARCHAR(50) UNIQUE NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Test results table
CREATE TABLE test_results (
  id SERIAL PRIMARY KEY,
  user_id INTEGER REFERENCES users(id),
  test_type VARCHAR(20) NOT NULL,
  duration INTEGER,
  word_count INTEGER,
  wpm DECIMAL(5,2) NOT NULL,
  raw_wpm DECIMAL(5,2) NOT NULL,
  accuracy DECIMAL(5,2) NOT NULL,
  consistency DECIMAL(5,2) NOT NULL,
  character_stats JSONB,
  created_at TIMESTAMP DEFAULT NOW()
);

-- User preferences table
CREATE TABLE user_preferences (
  id SERIAL PRIMARY KEY,
  user_id INTEGER REFERENCES users(id) UNIQUE,
  theme VARCHAR(50) DEFAULT 'dark',
  font_family VARCHAR(50) DEFAULT 'mono',
  caret_style VARCHAR(20) DEFAULT 'line',
  sound_enabled BOOLEAN DEFAULT false,
  preferences JSONB,
  updated_at TIMESTAMP DEFAULT NOW()
);
```

---

## ⚡ Performance Requirements & Optimization

### Frontend Performance

#### Keystroke Latency Optimization
```typescript
// Optimized input handling with debouncing
const useOptimizedInput = () => {
  const [input, setInput] = useState('');
  const deferredInput = useDeferredValue(input);
  
  const handleKeyPress = useCallback((e: KeyboardEvent) => {
    // Immediate UI update for responsiveness
    setInput(prev => prev + e.key);
    
    // Deferred validation and statistics calculation
    startTransition(() => {
      validateInput(deferredInput);
      updateStatistics(deferredInput);
    });
  }, []);
  
  return { input, handleKeyPress };
};
```

#### Rendering Optimization
- **Virtual Scrolling**: For long texts and test history
- **React.memo**: Prevent unnecessary re-renders
- **useMemo/useCallback**: Expensive calculations and event handlers
- **Code Splitting**: Lazy load non-critical components

#### Bundle Optimization
- **Tree Shaking**: Remove unused code
- **Dynamic Imports**: Load features on demand
- **Asset Optimization**: Compress images and fonts
- **CDN**: Serve static assets from global CDN

### Backend Performance

#### Database Optimization
```sql
-- Indexes for common queries
CREATE INDEX idx_test_results_user_created ON test_results(user_id, created_at DESC);
CREATE INDEX idx_test_results_wpm ON test_results(wpm DESC);
CREATE INDEX idx_users_email ON users(email);
```

#### API Performance
- **Connection Pooling**: PostgreSQL connection pool (max 20 connections)
- **Query Optimization**: Use Prisma query optimization
- **Caching**: Redis for session storage and leaderboards
- **Rate Limiting**: Prevent API abuse (100 requests/minute per user)

#### Response Time Targets
- **Authentication**: <100ms
- **Test Data Retrieval**: <50ms
- **Statistics Calculation**: <200ms
- **Leaderboard Queries**: <300ms

---

## 🔒 Security Architecture

### Authentication & Authorization
```typescript
// JWT Token Structure
interface JWTPayload {
  userId: number;
  email: string;
  iat: number;
  exp: number; // 24 hour expiration
}

// Authorization Middleware
const authenticateToken = (req: Request, res: Response, next: NextFunction) => {
  const token = req.headers.authorization?.split(' ')[1];
  
  if (!token) {
    return res.status(401).json({ error: 'Access token required' });
  }
  
  jwt.verify(token, process.env.JWT_SECRET!, (err, payload) => {
    if (err) return res.status(403).json({ error: 'Invalid token' });
    req.user = payload as JWTPayload;
    next();
  });
};
```

### Data Protection
- **Password Hashing**: bcrypt with salt rounds 12
- **Input Validation**: Joi schema validation for all endpoints
- **SQL Injection Prevention**: Prisma ORM with parameterized queries
- **XSS Protection**: Content Security Policy headers
- **CSRF Protection**: SameSite cookies and CSRF tokens

### Privacy Considerations
- **Data Minimization**: Only collect necessary user data
- **Anonymization**: No storage of actual typed content
- **GDPR Compliance**: User data export and deletion capabilities
- **Audit Logging**: Track data access and modifications

---

## 📊 Data Architecture

### Data Flow Architecture
```
User Input → Frontend Validation → Real-time UI Update
     ↓
Keystroke Events → Performance Calculation → State Update
     ↓
Test Completion → Results Processing → Backend API
     ↓
Data Validation → Database Storage → Response
     ↓
Statistics Update → Cache Update → UI Refresh
```

### Data Models

#### Frontend Data Models
```typescript
interface TypingTest {
  id: string;
  mode: TestMode;
  text: string;
  startTime: number;
  endTime: number;
  userInput: string;
  results: TestResults;
}

interface TestResults {
  wpm: number;
  rawWpm: number;
  accuracy: number;
  consistency: number;
  characterStats: CharacterStats;
  timeData: TimePoint[];
}

interface CharacterStats {
  correct: number;
  incorrect: number;
  missed: number;
  extra: number;
}
```

#### Backend Data Models
```typescript
// Prisma Schema Models
model User {
  id          Int       @id @default(autoincrement())
  email       String    @unique
  username    String    @unique
  passwordHash String   @map("password_hash")
  createdAt   DateTime  @default(now()) @map("created_at")
  updatedAt   DateTime  @updatedAt @map("updated_at")
  
  testResults TestResult[]
  preferences UserPreferences?
}

model TestResult {
  id            Int      @id @default(autoincrement())
  userId        Int      @map("user_id")
  testType      String   @map("test_type")
  wpm           Decimal  @db.Decimal(5, 2)
  rawWpm        Decimal  @map("raw_wpm") @db.Decimal(5, 2)
  accuracy      Decimal  @db.Decimal(5, 2)
  consistency   Decimal  @db.Decimal(5, 2)
  characterStats Json    @map("character_stats")
  createdAt     DateTime @default(now()) @map("created_at")
  
  user User @relation(fields: [userId], references: [id])
}
```

---

## 🚀 Deployment Architecture

### Development Environment
```yaml
# docker-compose.dev.yml
version: '3.8'
services:
  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
    volumes:
      - ./frontend:/app
    environment:
      - VITE_API_URL=http://localhost:5000
  
  backend:
    build: ./backend
    ports:
      - "5000:5000"
    volumes:
      - ./backend:/app
    environment:
      - DATABASE_URL=postgresql://user:pass@db:5432/fasttype
      - JWT_SECRET=dev-secret
    depends_on:
      - db
  
  db:
    image: postgres:15
    environment:
      - POSTGRES_DB=fasttype
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=pass
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data
```

### Production Environment
```yaml
# Production deployment configuration
Frontend (Vercel):
  - Build Command: npm run build
  - Output Directory: dist
  - Environment Variables:
    - VITE_API_URL: https://api.fasttype.com
    - VITE_GA_ID: G-XXXXXXXXXX

Backend (Railway):
  - Build Command: npm run build
  - Start Command: npm start
  - Environment Variables:
    - DATABASE_URL: ${{Railway.POSTGRESQL_URL}}
    - JWT_SECRET: ${{Railway.JWT_SECRET}}
    - NODE_ENV: production
```

### CI/CD Pipeline
```yaml
# .github/workflows/deploy.yml
name: Deploy FastType
on:
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
      - run: npm ci
      - run: npm run test
      - run: npm run lint
  
  deploy-frontend:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Deploy to Vercel
        uses: amondnet/vercel-action@v20
  
  deploy-backend:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Deploy to Railway
        uses: railway-app/railway-action@v1
```

---

## 🧪 Testing Strategy

### Frontend Testing
```typescript
// Component Testing (React Testing Library)
describe('TypingArea Component', () => {
  it('should handle keystroke input correctly', () => {
    render(<TypingArea text="hello world" />);
    
    fireEvent.keyDown(screen.getByRole('textbox'), {
      key: 'h',
      code: 'KeyH'
    });
    
    expect(screen.getByText('h')).toHaveClass('correct');
  });
  
  it('should calculate WPM accurately', () => {
    const { result } = renderHook(() => useTypingTest());
    
    act(() => {
      result.current.startTest();
      // Simulate typing 'hello' in 12 seconds (25 WPM)
      result.current.updateInput('hello');
      jest.advanceTimersByTime(12000);
      result.current.completeTest();
    });
    
    expect(result.current.wpm).toBe(25);
  });
});
```

### Backend Testing
```typescript
// API Testing (Jest + Supertest)
describe('POST /api/tests', () => {
  it('should save test results for authenticated user', async () => {
    const token = generateTestToken(testUser.id);
    
    const response = await request(app)
      .post('/api/tests')
      .set('Authorization', `Bearer ${token}`)
      .send({
        wpm: 65.5,
        accuracy: 96.2,
        testType: 'time',
        duration: 60
      });
    
    expect(response.status).toBe(201);
    expect(response.body.wpm).toBe(65.5);
  });
});
```

### E2E Testing
```typescript
// Playwright E2E Tests
test('complete typing test flow', async ({ page }) => {
  await page.goto('/');
  
  // Start typing test
  await page.click('[data-testid="start-test"]');
  
  // Type text
  await page.keyboard.type('hello world');
  
  // Wait for completion
  await page.waitForSelector('[data-testid="results-modal"]');
  
  // Verify results
  const wpm = await page.textContent('[data-testid="wpm-result"]');
  expect(parseInt(wpm!)).toBeGreaterThan(0);
});
```

---

## 📈 Monitoring & Observability

### Application Monitoring
```typescript
// Error Tracking (Sentry)
import * as Sentry from '@sentry/react';

Sentry.init({
  dsn: process.env.REACT_APP_SENTRY_DSN,
  environment: process.env.NODE_ENV,
  tracesSampleRate: 0.1,
});

// Performance Monitoring
const performanceObserver = new PerformanceObserver((list) => {
  list.getEntries().forEach((entry) => {
    if (entry.entryType === 'measure' && entry.name === 'keystroke-latency') {
      // Track keystroke latency
      analytics.track('keystroke_latency', {
        duration: entry.duration,
        timestamp: entry.startTime
      });
    }
  });
});
```

### Infrastructure Monitoring
- **Uptime Monitoring**: Uptime Robot (5-minute intervals)
- **Performance Metrics**: Core Web Vitals tracking
- **Error Rates**: Sentry error rate alerts
- **Database Performance**: Railway built-in monitoring

### Key Metrics Dashboard
```typescript
interface SystemMetrics {
  // Performance Metrics
  keystrokeLatency: number;      // Target: <50ms
  pageLoadTime: number;          // Target: <2s
  apiResponseTime: number;       // Target: <200ms
  
  // User Metrics
  dailyActiveUsers: number;
  sessionDuration: number;       // Target: >5min
  testCompletionRate: number;    // Target: >80%
  
  // System Health
  uptime: number;                // Target: 99.9%
  errorRate: number;             // Target: <0.1%
  databaseConnections: number;   // Monitor: <80% of pool
}
```

---

## 🔄 Scalability Considerations

### Horizontal Scaling Strategy
```yaml
# Future Kubernetes Configuration
apiVersion: apps/v1
kind: Deployment
metadata:
  name: fasttype-backend
spec:
  replicas: 3
  selector:
    matchLabels:
      app: fasttype-backend
  template:
    spec:
      containers:
      - name: backend
        image: fasttype/backend:latest
        resources:
          requests:
            memory: "256Mi"
            cpu: "250m"
          limits:
            memory: "512Mi"
            cpu: "500m"
```

### Database Scaling
- **Read Replicas**: For analytics and leaderboard queries
- **Connection Pooling**: PgBouncer for connection management
- **Caching Layer**: Redis for session storage and frequent queries
- **Partitioning**: Partition test_results by date for performance

### CDN & Caching Strategy
- **Static Assets**: Vercel Edge Network
- **API Responses**: Redis caching for leaderboards and user stats
- **Database Queries**: Query result caching with TTL
- **Browser Caching**: Aggressive caching for static resources

---

## 🛡️ Disaster Recovery & Backup

### Backup Strategy
```yaml
Database Backups:
  - Frequency: Daily automated backups
  - Retention: 30 days point-in-time recovery
  - Location: Railway automated backup system
  - Testing: Monthly backup restoration tests

Application Backups:
  - Code: Git repository (GitHub)
  - Configuration: Environment variables in secure storage
  - Dependencies: Package-lock files in version control
```

### Recovery Procedures
1. **Database Recovery**: Restore from Railway backup within 4 hours
2. **Application Recovery**: Redeploy from Git within 30 minutes
3. **Configuration Recovery**: Restore environment variables within 15 minutes
4. **DNS Recovery**: Update DNS records within 1 hour

---

## 📋 Architecture Decision Records (ADRs)

### ADR-001: Frontend Framework Selection
- **Decision**: React with TypeScript
- **Rationale**: Team expertise, ecosystem maturity, performance features
- **Alternatives**: Vue.js, Svelte
- **Status**: Accepted

### ADR-002: State Management Solution
- **Decision**: Zustand for client state
- **Rationale**: Lightweight, performant for frequent updates
- **Alternatives**: Redux Toolkit, Context API
- **Status**: Accepted

### ADR-003: Database Selection
- **Decision**: PostgreSQL with Prisma ORM
- **Rationale**: ACID compliance, excellent TypeScript integration
- **Alternatives**: MongoDB, MySQL
- **Status**: Accepted

### ADR-004: Deployment Strategy
- **Decision**: Vercel (frontend) + Railway (backend)
- **Rationale**: Optimized for respective technologies, cost-effective
- **Alternatives**: AWS, Google Cloud, self-hosted
- **Status**: Accepted

---

**Document Status**: Living document, updated with architectural changes  
**Next Review**: End of each development phase  
**Approval Required**: Technical Lead and Senior Developer sign-off
