# PhishGuard 🛡️

[![Next.js](https://img.shields.io/badge/Next.js-15.5.5-black?style=flat-square&logo=next.js)](https://nextjs.org/)
[![React](https://img.shields.io/badge/React-19.1.0-blue?style=flat-square&logo=react)](https://reactjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue?style=flat-square&logo=typescript)](https://www.typescriptlang.org/)
[![MongoDB](https://img.shields.io/badge/MongoDB-8.19.1-green?style=flat-square&logo=mongodb)](https://www.mongodb.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](LICENSE)

**PhishGuard** is an intelligent, AI-powered phishing detection platform built with Next.js and Google Gemini AI. It provides real-time analysis of emails, URLs, and text content to identify phishing attempts, educate users through interactive games, and maintain comprehensive detection history.

---

## 📋 Table of Contents

- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Architecture](#-architecture)
- [Getting Started](#-getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Environment Variables](#environment-variables)
  - [Running the Application](#running-the-application)
- [Project Structure](#-project-structure)
- [API Documentation](#-api-documentation)
- [Database Schema](#-database-schema)
- [Authentication Flow](#-authentication-flow)
- [Key Features Deep Dive](#-key-features-deep-dive)
- [Development](#-development)
- [Testing](#-testing)
- [Deployment](#-deployment)
- [Contributing](#-contributing)
- [Troubleshooting](#-troubleshooting)
- [License](#-license)

---

## ✨ Features

### 🔍 AI-Powered Detection
- **Multi-Format Analysis**: Analyze emails, URLs, and plain text for phishing indicators
- **Google Gemini AI Integration**: Advanced AI model for accurate threat detection
- **Real-time Risk Assessment**: Instant confidence scores (0-100) and risk levels (Low/Medium/High/Critical)
- **Technique Identification**: Detects specific phishing tactics (urgency, impersonation, suspicious links, etc.)
- **Actionable Recommendations**: Personalized security guidance based on analysis

### 👤 User Management
- **JWT Authentication**: Secure token-based authentication with httpOnly cookies
- **User Registration & Login**: Encrypted password storage using bcrypt
- **Session Management**: Automatic token refresh and expiration handling
- **Multi-user Support**: Complete data isolation per user account

### 📊 Detection History & Analytics
- **Per-User History**: Stores all detection analyses linked to user accounts
- **Advanced Filtering**: Filter by detection type (email/URL/text) and risk level
- **Pagination Support**: Efficient data loading with customizable page sizes
- **Detailed View**: Comprehensive breakdown of each detection with techniques, explanations, and recommendations
- **Statistics Dashboard**: Aggregated metrics including total detections, phishing rate, and risk trends

### 🎮 Interactive Learning
- **Phishing Training Games**: Gamified learning experiences to identify phishing attempts
- **Achievement System**: Badges and rewards for progress tracking
- **Leaderboard**: Competitive scoring to encourage learning
- **Progress Tracking**: Monitor improvement over time

### 🤖 AI Assistant
- **Conversational Interface**: Chat with AI about phishing and security topics
- **Context-Aware Responses**: Understands security concepts and provides guidance
- **Educational Support**: Explains detection results and security best practices

### 🎨 Modern UI/UX
- **Responsive Design**: Mobile-first approach with tablet and desktop optimization
- **Dark/Light Mode**: Theme switching with next-themes
- **Glass Morphism**: Modern UI effects and animations
- **Accessibility**: WCAG-compliant components using Radix UI
- **Tailwind CSS 4**: Utility-first styling with custom animations

---

## 🛠️ Tech Stack

### Frontend
- **Framework**: [Next.js 15.5.5](https://nextjs.org/) (App Router with Turbopack)
- **UI Library**: [React 19.1.0](https://reactjs.org/)
- **Language**: [TypeScript 5](https://www.typescriptlang.org/)
- **Styling**: [Tailwind CSS 4](https://tailwindcss.com/)
- **Component Library**: [Radix UI](https://www.radix-ui.com/)
- **Icons**: [Lucide React](https://lucide.dev/)
- **Animations**: [Framer Motion 12](https://www.framer.com/motion/)
- **State Management**: [Redux Toolkit](https://redux-toolkit.js.org/)

### Backend
- **Runtime**: Node.js (via Next.js API Routes)
- **Database**: [MongoDB](https://www.mongodb.com/) with [Mongoose 8.19.1](https://mongoosejs.com/)
- **Authentication**: [JSON Web Tokens (JWT)](https://jwt.io/)
- **Password Hashing**: [bcryptjs 3.0.2](https://github.com/dcodeIO/bcrypt.js)
- **AI Engine**: [Google Gemini AI](https://ai.google.dev/)

### Development Tools
- **Package Manager**: npm
- **Linting**: ESLint
- **Type Checking**: TypeScript
- **Build Tool**: Turbopack (Next.js 15)

---

## 🏗️ Architecture

### System Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        Client (Browser)                          │
│  ┌──────────────┐  ┌──────────────┐  ┌─────────────────────┐   │
│  │   Landing    │  │     Auth     │  │   Dashboard         │   │
│  │     Page     │  │  (Login/Reg) │  │   (Protected)       │   │
│  └──────────────┘  └──────────────┘  └─────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                              │
                              │ HTTP/HTTPS
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                      Next.js Application                         │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │                    App Router (RSC)                       │   │
│  │  • Server Components  • Client Components  • Middleware  │   │
│  └──────────────────────────────────────────────────────────┘   │
│                              │                                   │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │                    API Routes Layer                       │   │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌─────────┐ │   │
│  │  │   Auth   │  │ Detector │  │Dashboard │  │Assistant│ │   │
│  │  │   API    │  │   API    │  │   API    │  │   API   │ │   │
│  │  └──────────┘  └──────────┘  └──────────┘  └─────────┘ │   │
│  └──────────────────────────────────────────────────────────┘   │
│                              │                                   │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │              Business Logic & Services                    │   │
│  │  • JWT Verification  • Rate Limiting  • Data Validation  │   │
│  └──────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                    │                       │
                    ▼                       ▼
          ┌───────────────────┐   ┌────────────────────┐
          │   MongoDB Atlas   │   │  Google Gemini AI  │
          │  (User Database)  │   │   (AI Analysis)    │
          │  • Users          │   │  • gemini-2.5-pro  │
          │  • DetectionHist  │   │  • Rate Limited    │
          │  • GameResults    │   │                    │
          └───────────────────┘   └────────────────────┘
```

### Data Flow

1. **User Authentication**:
   ```
   Login → POST /api/auth/login → JWT Generation → httpOnly Cookie → Protected Routes
   ```

2. **Phishing Detection**:
   ```
   Content Input → POST /api/detector/analyze → Gemini AI Analysis → 
   Detection Result → Save to MongoDB → Return Response + Refresh History
   ```

3. **History Retrieval**:
   ```
   Dashboard Load → GET /api/detector/history → JWT Verification → 
   MongoDB Query (userId filter) → Paginated Results → UI Render
   ```

---

## 🚀 Getting Started

### Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** (v18.0 or higher) - [Download](https://nodejs.org/)
- **npm** (v9.0 or higher) - Comes with Node.js
- **MongoDB** (v6.0 or higher) - [Download](https://www.mongodb.com/try/download/community) or use [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
- **Google Gemini API Key** - [Get API Key](https://makersuite.google.com/app/apikey)

### Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/mohdanas86/phishguard.git
   cd phishguard
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Set up environment variables** (see [Environment Variables](#environment-variables) section)

4. **Start MongoDB** (if running locally):
   ```bash
   # macOS/Linux
   mongod --dbpath /path/to/data/db
   
   # Windows
   mongod --dbpath C:\data\db
   
   # Or use MongoDB Atlas cloud service
   ```

### Environment Variables

Create a `.env.local` file in the root directory:

```env
# Database Configuration
MONGODB_URI=mongodb://localhost:27017/phishguard
MONGODB_DB=phishguard

# Authentication
JWT_SECRET=your-super-secret-jwt-key-change-this-in-production
COOKIE_NAME=phishguard_auth

# Google Gemini AI
GEMINI_API_KEY=your-gemini-api-key-here
GOOGLE_API_KEY=your-gemini-api-key-here

# Application
NODE_ENV=development
NEXT_PUBLIC_APP_URL=http://localhost:3000
```

**⚠️ Security Notes**:
- Never commit `.env.local` to version control
- Use strong, randomly generated JWT_SECRET in production
- Rotate API keys regularly
- Use environment-specific configurations

### Running the Application

#### Development Mode

```bash
npm run dev
```

Visit [http://localhost:3000](http://localhost:3000) to view the application.

**Features in Development Mode**:
- Hot Module Replacement (HMR) with Turbopack
- Detailed error messages
- Source maps enabled
- API logs in console

#### Production Build

```bash
# Build the application
npm run build

# Start production server
npm start
```

**Production Optimizations**:
- Minified JavaScript/CSS
- Server-side rendering optimization
- Image optimization
- Static generation where applicable

---

## 📁 Project Structure

```
phishguard/
├── app/                          # Next.js App Router
│   ├── (dashboard)/              # Dashboard route group (protected)
│   │   ├── layout.tsx            # Dashboard layout with sidebar
│   │   ├── dashboard/            # Main dashboard page
│   │   │   └── page.tsx
│   │   ├── ai-detection/         # AI phishing detection page
│   │   │   └── page.tsx
│   │   ├── detection/[id]/       # Detection detail view
│   │   │   └── page.tsx
│   │   ├── assistant/            # AI assistant chat
│   │   │   └── page.tsx
│   │   ├── learning-games/       # Interactive learning games
│   │   │   └── page.tsx
│   │   ├── analytics/            # Analytics dashboard
│   │   │   └── page.tsx
│   │   ├── profile/              # User profile management
│   │   │   └── page.tsx
│   │   └── settings/             # Application settings
│   │       └── page.tsx
│   ├── api/                      # API Routes
│   │   ├── auth/                 # Authentication endpoints
│   │   │   ├── login/route.ts    # POST /api/auth/login
│   │   │   └── register/route.ts # POST /api/auth/register
│   │   ├── detector/             # Detection endpoints
│   │   │   ├── analyze/route.ts  # POST /api/detector/analyze
│   │   │   ├── history/route.ts  # GET/DELETE /api/detector/history
│   │   │   └── stats/route.ts    # GET /api/detector/stats
│   │   ├── assistant/            # AI assistant endpoints
│   │   │   └── chat/route.ts     # POST /api/assistant/chat
│   │   ├── game/                 # Learning game endpoints
│   │   │   ├── emails/route.ts   # GET /api/game/emails
│   │   │   ├── submit/route.ts   # POST /api/game/submit
│   │   │   ├── leaderboard/      # GET /api/game/leaderboard
│   │   │   └── progress/route.ts # GET /api/game/progress
│   │   └── dashboard/            # Dashboard endpoints
│   │       ├── stats/route.ts    # GET /api/dashboard/stats
│   │       ├── history/route.ts  # GET /api/dashboard/history
│   │       └── achievements/     # GET /api/dashboard/achievements
│   ├── login/                    # Login page
│   │   └── page.tsx
│   ├── register/                 # Registration page
│   │   └── page.tsx
│   ├── layout.tsx                # Root layout
│   ├── page.tsx                  # Landing page
│   ├── globals.css               # Global styles
│   └── providers.tsx             # Context providers
│
├── components/                   # React components
│   ├── home/                     # Landing page components
│   │   ├── header.tsx            # Navigation header
│   │   ├── hero-section.tsx      # Hero section
│   │   ├── features-section.tsx  # Features showcase
│   │   ├── how-it-works.tsx      # Explanation section
│   │   ├── cta-section.tsx       # Call-to-action
│   │   └── footer.tsx            # Footer
│   ├── ui/                       # Reusable UI components (Radix)
│   │   ├── button.tsx
│   │   ├── card.tsx
│   │   ├── input.tsx
│   │   ├── badge.tsx
│   │   ├── alert.tsx
│   │   ├── tabs.tsx
│   │   ├── sidebar.tsx
│   │   └── ...
│   ├── app-sidebar.tsx           # Application sidebar
│   ├── login-form.tsx            # Login form component
│   ├── theme-provider.tsx        # Theme context provider
│   └── theme-switcher.tsx        # Dark/light mode toggle
│
├── models/                       # Mongoose models
│   ├── User.js                   # User schema
│   └── DetectionHistory.js       # Detection history schema
│
├── lib/                          # Utility libraries
│   ├── mongodb.ts                # MongoDB connection handler
│   └── utils.ts                  # Helper functions
│
├── store/                        # Redux store
│   ├── store.ts                  # Store configuration
│   └── slices/
│       └── authSlice.ts          # Authentication slice
│
├── hooks/                        # Custom React hooks
│   └── use-mobile.ts             # Mobile detection hook
│
├── middlewares/                  # Custom middleware
│
├── public/                       # Static assets
│   └── ...
│
├── .env.local                    # Environment variables (not in git)
├── .gitignore                    # Git ignore rules
├── components.json               # Shadcn UI configuration
├── middleware.ts                 # Next.js middleware
├── next.config.ts                # Next.js configuration
├── package.json                  # Dependencies
├── postcss.config.mjs            # PostCSS configuration
├── tsconfig.json                 # TypeScript configuration
├── tailwind.config.ts            # Tailwind configuration
└── README.md                     # This file
```

---

## 📡 API Documentation

### Authentication Endpoints

#### Register User
```http
POST /api/auth/register
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "SecurePass123!"
}

Response (201):
{
  "user": {
    "id": "507f1f77bcf86cd799439011",
    "name": "John Doe",
    "email": "john@example.com"
  },
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

#### Login User
```http
POST /api/auth/login
Content-Type: application/json

{
  "email": "john@example.com",
  "password": "SecurePass123!"
}

Response (200):
{
  "user": {
    "id": "507f1f77bcf86cd799439011",
    "name": "John Doe",
    "email": "john@example.com"
  },
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

### Detection Endpoints

#### Analyze Content
```http
POST /api/detector/analyze
Content-Type: application/json
Cookie: token=<jwt_token>

{
  "content": "Urgent: Your account has been suspended...",
  "contentType": "email",
  "subject": "Account Verification Required",
  "sender": "security@paypal-verify.com"
}

Response (200):
{
  "riskScore": 85,
  "isPhishing": true,
  "riskLevel": "High",
  "techniques": [
    "Urgency tactics",
    "Suspicious domain",
    "Impersonation"
  ],
  "explanation": "This email exhibits multiple phishing indicators...",
  "recommendations": [
    "Do not click any links in this email",
    "Verify sender authenticity through official channels",
    "Report to your IT security team"
  ],
  "savedToHistory": true
}
```

#### Get Detection History
```http
GET /api/detector/history?page=1&limit=10&type=email&risk=High
Cookie: token=<jwt_token>

Response (200):
{
  "success": true,
  "history": [
    {
      "_id": "507f1f77bcf86cd799439011",
      "detectionType": "email",
      "isPhishing": true,
      "confidence": 85,
      "riskLevel": "High",
      "subject": "Account Verification Required",
      "sender": "security@paypal-verify.com",
      "techniques": ["Urgency tactics", "Suspicious domain"],
      "explanation": "...",
      "recommendations": ["..."],
      "createdAt": "2025-10-20T10:30:00.000Z"
    }
  ],
  "pagination": {
    "currentPage": 1,
    "totalPages": 5,
    "totalItems": 47,
    "itemsPerPage": 10,
    "hasNextPage": true,
    "hasPrevPage": false
  }
}
```

#### Delete Detection History
```http
DELETE /api/detector/history?id=507f1f77bcf86cd799439011
Cookie: token=<jwt_token>

Response (200):
{
  "success": true,
  "message": "History item deleted successfully"
}
```

#### Get Detection Statistics
```http
GET /api/detector/stats
Cookie: token=<jwt_token>

Response (200):
{
  "overall": {
    "totalDetections": 127,
    "phishingDetected": 45,
    "safeDetections": 82,
    "averageConfidence": 73,
    "detectionRate": 0.35
  },
  "riskBreakdown": {
    "critical": 8,
    "high": 15,
    "medium": 22,
    "low": 82
  },
  "byType": [
    { "type": "email", "total": 87, "phishing": 32, "safe": 55 },
    { "type": "url", "total": 28, "phishing": 10, "safe": 18 },
    { "type": "text", "total": 12, "phishing": 3, "safe": 9 }
  ],
  "commonTechniques": [
    { "technique": "Urgency tactics", "occurrences": 28 },
    { "technique": "Suspicious links", "occurrences": 23 }
  ],
  "recentActivity": [
    { "date": "2025-10-20", "total": 5, "phishing": 2, "safe": 3 }
  ]
}
```

### Dashboard Endpoints

#### Get Dashboard Stats
```http
GET /api/dashboard/stats
Cookie: token=<jwt_token>

Response (200):
{
  "plays": 15,
  "totalAnswers": 45,
  "totalCorrect": 38,
  "accuracy": 84,
  "roundScore": 380,
  "leaderboard": {
    "totalScore": 380,
    "plays": 15
  },
  "analyses": 127,
  "avgRisk": 45,
  "phishingDetected": 45
}
```

### Assistant Endpoints

#### Chat with AI Assistant
```http
POST /api/assistant/chat
Content-Type: application/json

{
  "message": "What are common signs of phishing emails?",
  "history": []
}

Response (200):
{
  "response": "Common signs of phishing emails include:\n1. Urgency or threats...",
  "timestamp": "2025-10-20T10:30:00.000Z"
}
```

---

## 🗄️ Database Schema

### User Collection
```javascript
{
  _id: ObjectId,
  name: String,
  email: String (unique, indexed),
  password: String (bcrypt hashed),
  createdAt: Date,
  updatedAt: Date
}
```

**Indexes**:
- `email`: Unique index for fast lookup

**Methods**:
- `comparePassword(candidatePassword)`: Verifies password

### DetectionHistory Collection
```javascript
{
  _id: ObjectId,
  userId: ObjectId (ref: User, indexed),
  userEmail: String,
  detectionType: String (enum: ['email', 'url', 'text']),
  content: String,
  subject: String (optional),
  sender: String (optional),
  isPhishing: Boolean,
  confidence: Number (0-100),
  riskLevel: String (enum: ['Low', 'Medium', 'High', 'Critical']),
  techniques: [String],
  explanation: String,
  recommendations: [String],
  ipAddress: String,
  userAgent: String,
  createdAt: Date,
  updatedAt: Date
}
```

**Indexes**:
- `userId + createdAt`: Compound index for efficient user queries
- `userEmail + createdAt`: Compound index for email-based queries

**Static Methods**:
- `getUserHistory(userId, options)`: Paginated history retrieval
- `getUserStats(userId)`: Aggregated statistics

**Instance Methods**:
- `getFormattedResult()`: Returns formatted detection result

### GameResult Collection
```javascript
{
  _id: ObjectId,
  sessionId: String,
  answers: [{
    emailId: String,
    guessedPhishing: Boolean,
    correct: Boolean
  }],
  score: Number,
  createdAt: Date,
  updatedAt: Date
}
```

### GameLeaderboard Collection
```javascript
{
  _id: ObjectId,
  sessionId: String,
  totalScore: Number,
  plays: Number,
  createdAt: Date,
  updatedAt: Date
}
```

---

## 🔐 Authentication Flow

### Registration Flow
```
1. User submits registration form
   ↓
2. POST /api/auth/register
   ↓
3. Validate input (email format, password strength)
   ↓
4. Check if email already exists
   ↓
5. Hash password with bcrypt (10 rounds)
   ↓
6. Create user document in MongoDB
   ↓
7. Generate JWT token with payload: { userId, email, id }
   ↓
8. Set httpOnly cookie: "token" (7-day expiry)
   ↓
9. Return user object + token
   ↓
10. Redirect to dashboard
```

### Login Flow
```
1. User submits login credentials
   ↓
2. POST /api/auth/login
   ↓
3. Find user by email
   ↓
4. Compare password using bcrypt
   ↓
5. Generate JWT token
   ↓
6. Set httpOnly cookie: "token"
   ↓
7. Return user object + token
   ↓
8. Redirect to dashboard
```

### Protected Route Access
```
1. User requests protected page/API
   ↓
2. Extract JWT from cookie (token or phishguard_auth)
   ↓
3. Verify JWT signature using JWT_SECRET
   ↓
4. Extract userId from decoded token
   ↓
5. If valid: Allow access
   If invalid: Return 401 Unauthorized
```

### Security Features
- ✅ **httpOnly Cookies**: Prevents XSS attacks
- ✅ **Secure Flag**: HTTPS only in production
- ✅ **sameSite**: CSRF protection
- ✅ **bcrypt Hashing**: Password security (10 salt rounds)
- ✅ **JWT Expiration**: 7-day token lifetime
- ✅ **Rate Limiting**: 10 requests per 15 minutes for analysis
- ✅ **Input Validation**: Sanitized user inputs
- ✅ **User Isolation**: Data queries filtered by userId

---

## 🎯 Key Features Deep Dive

### AI Phishing Detection

**Technology**: Google Gemini 2.5 Pro AI model

**Detection Process**:
1. User submits content (email/URL/text)
2. Content is preprocessed and validated (max 10,000 characters)
3. Structured prompt sent to Gemini AI with phishing indicators checklist
4. AI analyzes content for 12+ phishing indicators
5. Returns JSON response with risk score, techniques, and recommendations
6. Result saved to user's detection history (if authenticated)
7. Frontend displays comprehensive analysis

**Phishing Indicators Analyzed**:
- Urgent or threatening language
- Suspicious URLs or domains
- Requests for personal information
- Poor grammar or spelling
- Unusual sender information
- Suspicious attachments or links
- Social engineering tactics
- Impersonation attempts
- Financial pressure tactics
- Unusual formatting
- Spoofed email addresses
- Too-good-to-be-true offers

**Risk Score Calculation**:
- **0-29**: Low Risk (likely safe)
- **30-59**: Medium Risk (suspicious)
- **60-79**: High Risk (likely phishing)
- **80-100**: Critical Risk (confirmed phishing)

### Detection History System

**Features**:
- Per-user data isolation (userId-based filtering)
- Pagination support (default: 10 items/page, max: 50)
- Advanced filtering (by type, risk level, date range)
- Sorting options (by date, confidence, risk level)
- Full-text search on content
- Export functionality (PDF/CSV) - coming soon
- Bulk actions (delete multiple) - coming soon

**Performance Optimizations**:
- MongoDB compound indexes for fast queries
- Lazy loading with pagination
- Efficient aggregation pipelines for statistics
- Client-side caching with React state

### Learning Games

**Game Types**:
1. **Email Classification**: Identify phishing vs legitimate emails
2. **URL Analysis**: Spot suspicious links
3. **Social Engineering Scenarios**: Real-world attack simulations

**Gamification Elements**:
- Points system (10 points per correct answer)
- Accuracy tracking
- Achievement badges
- Global leaderboard
- Progress tracking
- Streak bonuses

---

## 💻 Development

### Code Style & Standards

**TypeScript Best Practices**:
- Strict mode enabled
- Explicit type annotations
- Interface over type for objects
- Avoid `any` type

**React Best Practices**:
- Functional components with hooks
- Custom hooks for reusable logic
- Component composition over inheritance
- Props destructuring
- Proper key usage in lists

**Naming Conventions**:
- Components: PascalCase (`UserProfile.tsx`)
- Hooks: camelCase with "use" prefix (`useAuth.ts`)
- Constants: UPPER_SNAKE_CASE
- Variables/Functions: camelCase
- API Routes: kebab-case

### Development Workflow

```bash
# Create a new feature branch
git checkout -b feature/your-feature-name

# Make changes and test locally
npm run dev

# Check TypeScript errors
npx tsc --noEmit

# Build to verify production bundle
npm run build

# Commit changes
git add .
git commit -m "feat: add your feature description"

# Push and create pull request
git push origin feature/your-feature-name
```

### Environment Setup

**VS Code Extensions (Recommended)**:
- ESLint
- Prettier
- Tailwind CSS IntelliSense
- TypeScript Error Translator
- MongoDB for VS Code

**Debug Configuration** (`.vscode/launch.json`):
```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Next.js: debug server-side",
      "type": "node-terminal",
      "request": "launch",
      "command": "npm run dev"
    }
  ]
}
```

---

## 🧪 Testing

### Manual Testing Checklist

**Authentication**:
- [ ] User can register with valid credentials
- [ ] User cannot register with existing email
- [ ] User can login with correct credentials
- [ ] User cannot login with incorrect password
- [ ] JWT token is set in cookies
- [ ] Token expires after 7 days

**Detection**:
- [ ] User can analyze email content
- [ ] User can analyze URL
- [ ] User can analyze plain text
- [ ] Results show correct risk score
- [ ] Techniques are identified
- [ ] Recommendations are provided
- [ ] History is saved for authenticated users
- [ ] History is not saved for guest users

**Dashboard**:
- [ ] Stats display correctly
- [ ] Recent analyses appear
- [ ] Can click to view detection details
- [ ] Can delete history items
- [ ] Filtering works (type, risk level)
- [ ] Pagination works correctly

### API Testing with cURL

```bash
# Register user
curl -X POST http://localhost:3000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{"name":"Test User","email":"test@example.com","password":"Password123!"}'

# Login
curl -X POST http://localhost:3000/api/auth/login \
  -H "Content-Type: application/json" \
  -c cookies.txt \
  -d '{"email":"test@example.com","password":"Password123!"}'

# Analyze content
curl -X POST http://localhost:3000/api/detector/analyze \
  -H "Content-Type: application/json" \
  -b cookies.txt \
  -d '{"content":"Urgent: Verify your account","contentType":"email"}'

# Get history
curl -X GET http://localhost:3000/api/detector/history?page=1&limit=10 \
  -b cookies.txt
```

---

## 🚢 Deployment

### Vercel Deployment (Recommended)

1. **Push code to GitHub**
2. **Connect to Vercel**:
   - Visit [vercel.com](https://vercel.com)
   - Import your GitHub repository
3. **Configure environment variables** in Vercel dashboard
4. **Deploy** - Automatic deployments on push

### Environment Variables for Production

```env
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/phishguard
JWT_SECRET=super-secret-production-key-min-32-chars
GEMINI_API_KEY=your-production-gemini-key
NODE_ENV=production
NEXT_PUBLIC_APP_URL=https://your-domain.com
```

### Docker Deployment

```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci --only=production

COPY . .
RUN npm run build

EXPOSE 3000

CMD ["npm", "start"]
```

```bash
# Build image
docker build -t phishguard .

# Run container
docker run -p 3000:3000 \
  -e MONGODB_URI="..." \
  -e JWT_SECRET="..." \
  -e GEMINI_API_KEY="..." \
  phishguard
```

---

## 🤝 Contributing

We welcome contributions! Please follow these guidelines:

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feature/amazing-feature`
3. **Commit your changes**: `git commit -m 'feat: add amazing feature'`
4. **Push to the branch**: `git push origin feature/amazing-feature`
5. **Open a Pull Request**

### Commit Message Convention

Follow [Conventional Commits](https://www.conventionalcommits.org/):

- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation changes
- `style:` Code style changes (formatting)
- `refactor:` Code refactoring
- `test:` Adding tests
- `chore:` Maintenance tasks

---

## 🔧 Troubleshooting

### Common Issues

#### Issue: "Unauthorized. Please login to view history"

**Cause**: JWT token not found or expired

**Solution**:
1. Logout and login again
2. Clear browser cookies
3. Check JWT_SECRET in `.env.local`
4. Verify token cookie exists in DevTools

#### Issue: "No detection history" after analyzing

**Cause**: Not properly authenticated or history save failed

**Solution**:
1. Open browser console (F12)
2. Check for `savedToHistory: true` in logs
3. Verify you're logged in (check cookies)
4. Check server logs for database errors

#### Issue: MongoDB connection errors

**Cause**: MongoDB not running or incorrect URI

**Solution**:
1. Verify MongoDB is running: `mongosh`
2. Check MONGODB_URI in `.env.local`
3. Test connection: `mongosh "mongodb://localhost:27017/phishguard"`
4. Check firewall settings

#### Issue: Gemini API errors

**Cause**: Invalid API key or rate limit exceeded

**Solution**:
1. Verify GEMINI_API_KEY in `.env.local`
2. Check API key at [Google AI Studio](https://makersuite.google.com/)
3. Review rate limits (60 requests/minute)
4. Wait before retrying

### Debug Mode

Enable detailed logging:

```bash
# Set in .env.local
DEBUG=true
NODE_ENV=development
```

Check browser console and server logs for detailed error messages.

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👥 Authors

- **Mohd Anas** - [@mohdanas86](https://github.com/mohdanas86)

---

## 🙏 Acknowledgments

- [Next.js](https://nextjs.org/) - React framework
- [Google Gemini AI](https://ai.google.dev/) - AI-powered analysis
- [Radix UI](https://www.radix-ui.com/) - Accessible components
- [Tailwind CSS](https://tailwindcss.com/) - Utility-first CSS
- [MongoDB](https://www.mongodb.com/) - Database
- [Vercel](https://vercel.com/) - Hosting platform

---

## 📞 Support

For support, please:
- Contact: [coadanas@gmail.com]

---

## 🗺️ Roadmap

### Version 2.0 (Q1 2026)
- [ ] Multi-language support
- [ ] Email integration (Gmail, Outlook)
- [ ] Browser extension
- [ ] Mobile app (React Native)
- [ ] Advanced analytics dashboard
- [ ] Team collaboration features
- [ ] API for third-party integrations
- [ ] Machine learning model training
- [ ] Real-time threat intelligence

### Version 1.1 (Q4 2025)
- [x] Detection history system
- [x] User authentication
- [x] AI-powered analysis
- [x] Interactive learning games
- [ ] Export functionality (PDF/CSV)
- [ ] Bulk operations
- [ ] Email forwarding for analysis

---

<div align="center">

**⭐ Star this repository if you find it helpful!**

Made with ❤️ by the PhishGuard Team

[Report Bug](https://github.com/mohdanas86/phishguard/issues) · [Request Feature](https://github.com/mohdanas86/phishguard/issues) · [Documentation](https://github.com/mohdanas86/phishguard/wiki)

</div>
