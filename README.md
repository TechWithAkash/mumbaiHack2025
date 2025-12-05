# 📋 WealthWise - Complete Project Context & Documentation

> **Document Version:** 1.0  
> **Last Updated:** December 5, 2025  
> **Project:** WealthWise - AI-Powered Financial Intelligence Platform  
> **Event:** MumbaiHacks 2025 Hackathon Submission  
> **Repository:** [TechWithAkash/mumbaiHack2025](https://github.com/TechWithAkash/mumbaiHack2025)  
> **Live Demo:** [wealthwise-mumbaihack.vercel.app](https://wealthwise-mumbaihack.vercel.app/)

---

## 📖 Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Project Vision & Problem Statement](#2-project-vision--problem-statement)
3. [Core Innovation - Autonomous AI Agents](#3-core-innovation---autonomous-ai-agents)
4. [Technology Stack](#4-technology-stack)
5. [System Architecture](#5-system-architecture)
6. [Project Structure](#6-project-structure)
7. [Feature Implementation Details](#7-feature-implementation-details)
8. [Database Models & Schema](#8-database-models--schema)
9. [API Endpoints](#9-api-endpoints)
10. [Authentication System](#10-authentication-system)
11. [Internationalization (i18n)](#11-internationalization-i18n)
12. [Progressive Web App (PWA)](#12-progressive-web-app-pwa)
13. [Event-Driven Architecture](#13-event-driven-architecture)
14. [Development Timeline & Updates](#14-development-timeline--updates)
15. [Deployment & Infrastructure](#15-deployment--infrastructure)
16. [Future Roadmap](#16-future-roadmap)

---

## 1. Executive Summary

**WealthWise** is an AI-powered financial intelligence platform designed specifically for young Indian professionals (22-35 years). Unlike traditional budgeting apps that are reactive (showing what happened after it's too late), WealthWise is **proactive** - it uses autonomous AI agents that continuously monitor, learn, and take actions to improve users' financial well-being.

### Key Differentiators

- 🤖 **Three Autonomous AI Agents** working 24/7 in the background
- 🔮 **Predictive Intervention** - Alerts before problems occur, not after
- 🎯 **Flex Budgets** - Adaptive budgeting for gig workers with variable income
- 🗣️ **Multi-Language Voice Input** - Hindi, English, and Marathi support
- 📱 **Full PWA Support** - Offline functionality with native app experience
- 🇮🇳 **Indian Context** - Understands lakh/crore, festivals, and local financial patterns

### Target Metrics

- 85% reduction in budget overruns (proactive alerts)
- 60% increase in savings rate (automated recommendations)
- 3 seconds average agent response time
- 95% user satisfaction with AI recommendations

---

## 2. Project Vision & Problem Statement

### The Problem

Traditional finance apps are fundamentally **reactive**:

- ❌ "You overspent $500 this month" (after the damage is done)
- ❌ No understanding of gig economy income variability
- ❌ One-size-fits-all budgets that don't adapt
- ❌ English-only, no cultural context for Indian users

### Our Solution

WealthWise is **proactive**:

- ✅ "You're trending toward overspending. I've adjusted your budget and sent you an alert before you reach the limit."
- ✅ Flex budgets that automatically adapt to income fluctuations
- ✅ Pattern detection that learns from every transaction
- ✅ Multi-language support with Indian financial context

### Target Audience

- Young Indian professionals (22-35 years)
- Gig workers and freelancers with variable income
- First-generation wealth builders
- Users who prefer voice/vernacular interfaces

---

## 3. Core Innovation - Autonomous AI Agents

The heart of WealthWise is its **three specialized AI agents** that operate autonomously using real-time data, machine learning, and event-driven architecture.

### 3.1 Income Variability Agent (`lib/agents/IncomeAgent.js`)

**Purpose:** Designed for gig workers, freelancers, and anyone with irregular income.

**Autonomous Capabilities:**

- 📊 **Pattern Detection** - Analyzes 90-day income history to detect variability patterns
- 🎯 **Adaptive Budgeting** - Automatically creates "flex budgets" that adjust based on income fluctuations
- 🔮 **Income Prediction** - Predicts low-income periods using coefficient of variation analysis
- 🛡️ **Proactive Protection** - Auto-adjusts spending limits during predicted low-income months
- 💡 **Smart Recommendations** - Suggests emergency fund targets and income smoothing strategies

**Technical Implementation:**

```javascript
// Coefficient of variation for income variability
const variabilityScore = stdDev / mean;
if (variabilityScore > 0.3) {
  // High income variability detected
  await createFlexBudget(userId, {
    minIncome: Math.min(...amounts),
    maxIncome: Math.max(...amounts),
    avgIncome: mean,
  });
}
```

**Flex Budget Tiers:**

- **Lean Mode** - Activated during low-income periods
- **Normal Mode** - Standard spending patterns
- **Flush Mode** - Activated during high-income periods (increased savings)

### 3.2 Spending Pattern Agent (`lib/agents/SpendingPatternAgent.js`)

**Purpose:** Behavioral finance expert that learns from every transaction.

**Autonomous Capabilities:**

- 📈 **Behavioral Learning** - Builds spending profiles by category, day, time, and location
- 🚨 **Proactive Intervention** - Sends alerts BEFORE overspending (at 80% threshold)
- 🎯 **Trigger Detection** - Identifies spending triggers (e.g., "Always overspend on weekends")
- 🔍 **Anomaly Detection** - Uses z-score analysis to detect unusual spending patterns
- 📊 **Trend Analysis** - Identifies escalating spending behaviors early

**Technical Implementation:**

```javascript
// Pattern learning structure
userPatterns = {
  byCategory: {},      // Category-wise spending averages
  byDayOfWeek: {},     // Day-specific patterns
  byTimeOfDay: {},     // Time slot patterns (morning/afternoon/evening)
  byLocation: {},      // Location-based spending
  triggers: []         // Identified spending triggers
}

// Proactive intervention at 80% threshold
if (shouldIntervene.percentage >= 0.80) {
  sendAlert({
    type: 'warning',
    message: 'You've used 80% of your Food budget with 10 days left'
  });
}
```

### 3.3 Financial Coach Agent

**Purpose:** Personal AI financial advisor with multi-language support.

**Autonomous Capabilities:**

- 💬 **Natural Language Understanding** - Processes queries in English, Hindi, and Marathi
- 🎯 **Contextual Advice** - Personalized recommendations based on complete financial profile
- 📊 **Holistic Analysis** - Analyzes budget, expenses, goals, and investments simultaneously
- 🗣️ **Voice Integration** - Works with Vapi.ai for voice-based assistance
- 🌍 **Cultural Context** - Understands Indian financial patterns (festivals, lakh/crore)

### Agent Collaboration

All three agents work together through an event-driven architecture:

```
┌─────────────────────────────────────────────────────────────┐
│                     Event Bus (Central Hub)                  │
├─────────────────────────────────────────────────────────────┤
│  EXPENSE_ADDED → BUDGET_UPDATED → AGENT_ACTION → ...       │
└─────────────────────────────────────────────────────────────┘
         ↓                    ↓                    ↓
┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐
│  Income Agent    │  │ Spending Agent   │  │  Coach Agent     │
│  - Listen        │  │ - Listen         │  │ - Listen         │
│  - Analyze       │  │ - Learn          │  │ - Advise         │
│  - Act           │  │ - Intervene      │  │ - Recommend      │
└──────────────────┘  └──────────────────┘  └──────────────────┘
```

---

## 4. Technology Stack

### Frontend

| Technology    | Version | Purpose                                    |
| ------------- | ------- | ------------------------------------------ |
| Next.js       | 15.4    | React framework with App Router            |
| React         | 19.1    | Modern UI library with concurrent features |
| Tailwind CSS  | 4.x     | Utility-first CSS framework                |
| Framer Motion | 12.x    | Smooth animations and transitions          |
| Radix UI      | Latest  | Accessible component primitives            |
| Lucide Icons  | Latest  | Modern icon library                        |
| Recharts      | 3.x     | Data visualization                         |

### Backend

| Technology         | Version  | Purpose                              |
| ------------------ | -------- | ------------------------------------ |
| Next.js API Routes | 15.4     | Serverless API functions             |
| MongoDB            | 6.x      | Primary database                     |
| Mongoose           | 8.17     | MongoDB ODM                          |
| NextAuth.js        | 5.0-beta | Authentication (OAuth + Credentials) |
| bcryptjs           | 3.x      | Password hashing                     |

### AI & Intelligence

| Technology           | Purpose                                         |
| -------------------- | ----------------------------------------------- |
| Google Gemini AI     | Natural language processing & budget generation |
| Vapi.ai              | Voice assistant integration                     |
| Custom AI Agents     | Autonomous financial intelligence               |
| Statistical Analysis | Pattern recognition & prediction                |

### DevOps & Infrastructure

| Technology     | Purpose              |
| -------------- | -------------------- |
| Vercel         | Deployment & hosting |
| MongoDB Atlas  | Cloud database       |
| GitHub Actions | CI/CD pipeline       |

### Key Dependencies

```json
{
  "@auth/mongodb-adapter": "^3.10.0",
  "@google/generative-ai": "^0.24.1",
  "@vapi-ai/web": "^2.5.0",
  "bcryptjs": "^3.0.2",
  "framer-motion": "^12.23.24",
  "i18next": "^25.5.2",
  "mongodb": "^6.18.0",
  "mongoose": "^8.17.0",
  "next": "15.4.4",
  "next-auth": "^5.0.0-beta.29",
  "react": "19.1.0",
  "react-i18next": "^15.7.3",
  "recharts": "^3.1.1",
  "zod": "^4.0.10"
}
```

---

## 5. System Architecture

### High-Level Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                           Client Layer                               │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐ │
│  │   PWA App   │  │   Voice UI  │  │  Dashboard  │  │   Mobile    │ │
│  └─────────────┘  └─────────────┘  └─────────────┘  └─────────────┘ │
└─────────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────────┐
│                       Next.js Application                            │
│  ┌─────────────────────────────────────────────────────────────────┐│
│  │                    API Routes (/app/api/)                        ││
│  │  ┌───────┐ ┌────────┐ ┌───────┐ ┌───────┐ ┌──────┐ ┌─────────┐ ││
│  │  │ Auth  │ │ Budget │ │Expense│ │ Goals │ │ Debt │ │ Profile │ ││
│  │  └───────┘ └────────┘ └───────┘ └───────┘ └──────┘ └─────────┘ ││
│  └─────────────────────────────────────────────────────────────────┘│
│                              │                                       │
│  ┌─────────────────────────────────────────────────────────────────┐│
│  │                    AI Agent Layer                                ││
│  │  ┌────────────┐  ┌─────────────────┐  ┌──────────────────────┐ ││
│  │  │IncomeAgent │  │SpendingPatternAgt│  │FinancialCoachAgent  │ ││
│  │  └────────────┘  └─────────────────┘  └──────────────────────┘ ││
│  └─────────────────────────────────────────────────────────────────┘│
│                              │                                       │
│  ┌─────────────────────────────────────────────────────────────────┐│
│  │                     Event Bus System                             ││
│  │  EXPENSE_ADDED | INCOME_ADDED | AGENT_ACTION | AGENT_ALERT      ││
│  └─────────────────────────────────────────────────────────────────┘│
└─────────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────────┐
│                       External Services                              │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐ │
│  │MongoDB Atlas│  │ Google OAuth│  │  Gemini AI  │  │   Vapi.ai   │ │
│  └─────────────┘  └─────────────┘  └─────────────┘  └─────────────┘ │
└─────────────────────────────────────────────────────────────────────┘
```

### Request Flow

1. **User Interaction** → User performs action (add expense, voice command)
2. **API Layer** → Request processed by Next.js API routes
3. **Service Layer** → Business logic execution
4. **Agent Layer** → AI agents analyze and potentially intervene
5. **Event Bus** → Events propagated to all listening agents
6. **Database** → Data persisted to MongoDB
7. **Response** → Real-time feedback to user with agent insights

---

## 6. Project Structure

```
wealthwise-main/
├── app/                          # Next.js App Router
│   ├── api/                      # API Routes (Serverless Functions)
│   │   ├── auth/                 # Authentication endpoints
│   │   │   ├── [...nextauth]/    # NextAuth.js configuration
│   │   │   ├── register/         # User registration
│   │   │   ├── verify-email/     # Email verification
│   │   │   ├── forgot-password/  # Password reset request
│   │   │   └── reset-password/   # Password reset
│   │   ├── budget/               # Budget CRUD & AI generation
│   │   ├── debt/                 # Debt tracking & management
│   │   ├── expenses/             # Expense CRUD operations
│   │   ├── goals/                # Financial goals tracking
│   │   ├── health/               # System health checks
│   │   ├── investment/           # Investment tracking
│   │   ├── loan-advisor/         # AI loan recommendations
│   │   ├── notifications/        # Push notification management
│   │   ├── onboarding/           # User onboarding flow
│   │   ├── profile/              # User profile management
│   │   ├── transactions/         # Transaction history
│   │   ├── user/                 # User management
│   │   └── voice/                # Voice processing
│   ├── auth/                     # Authentication pages
│   │   ├── signin/               # Login page
│   │   ├── signup/               # Registration page
│   │   ├── verify-email/         # Email verification
│   │   ├── forgot-password/      # Password reset
│   │   └── error/                # Auth error handling
│   ├── dashboard/                # Main dashboard
│   ├── onboarding/               # Onboarding wizard
│   ├── offline/                  # Offline fallback page
│   ├── privacy-policy/           # Legal pages
│   ├── layout.js                 # Root layout
│   ├── page.js                   # Landing page
│   ├── globals.css               # Global styles
│   └── error.js                  # Error boundary
│
├── components/                   # React Components
│   ├── agents/                   # AI Agent UI components
│   │   └── AgentDashboard.js     # Real-time agent monitoring
│   ├── auth/                     # Authentication components
│   ├── budget/                   # Budget management
│   │   ├── BudgetCustomizer.js   # Budget customization
│   │   ├── BudgetCustomizationGuide.js
│   │   ├── DetailedBudgetReport.js
│   │   └── AIBudgetTip.js        # AI-powered tips
│   ├── dashboard/                # Dashboard components
│   │   ├── BudgetDisplay.js      # Budget visualization
│   │   └── ExpenseTrackingDashboard.js
│   ├── expenses/                 # Expense tracking
│   │   ├── ExpenseEntryModal.js  # Quick expense entry
│   │   └── ManualExpenseEntry.js
│   ├── goals/                    # Goal management
│   │   └── GoalTracker.js        # Goal progress tracking
│   ├── investment/               # Investment components
│   ├── layout/                   # Layout components
│   ├── mobile/                   # Mobile-specific components
│   ├── notifications/            # Notification components
│   ├── onboarding/               # Onboarding wizard
│   ├── providers/                # Context providers
│   ├── ui/                       # Reusable UI components
│   │   └── LanguageSelector.js   # i18n language switcher
│   ├── voice/                    # Voice interface
│   │   └── VoiceExpenseEntry.js  # Voice expense entry
│   ├── AgentInitializer.jsx      # Agent initialization
│   ├── ErrorBoundary.js          # Error handling
│   ├── OnboardingGuard.js        # Onboarding protection
│   ├── PWAInstallPrompt.js       # PWA install prompt
│   └── PWARegister.js            # Service worker registration
│
├── contexts/                     # React Contexts
│   ├── NotificationContext.js    # Notification state
│   └── ProfileContext.js         # User profile state
│
├── lib/                          # Core Libraries
│   ├── agents/                   # AI Agent Classes
│   │   ├── BaseAgent.js          # Base agent class
│   │   ├── IncomeAgent.js        # Income variability handler
│   │   ├── SpendingPatternAgent.js # Spending analyzer
│   │   └── index.js              # Agent exports
│   ├── events/                   # Event system
│   │   └── EventBus.js           # Event bus implementation
│   ├── config/                   # Configuration
│   ├── advancedBudgetEngine.js   # AI budget generation
│   ├── auth.js                   # Authentication logic
│   ├── budgetConfig.js           # Budget configuration
│   ├── budgetGenerator.js        # Budget generation
│   ├── database.js               # Database connection
│   ├── dbConnect.js              # Mongoose connection
│   ├── emailService.js           # Email sending
│   ├── encryption.js             # Data encryption
│   ├── errorHandler.js           # Error handling
│   ├── eventBus.js               # Event bus (legacy)
│   ├── i18n.js                   # Internationalization
│   ├── investmentAlerts.js       # Investment notifications
│   ├── languageDetection.js      # Auto language detection
│   ├── mongodb.js                # MongoDB client
│   ├── notificationService.js    # Push notifications
│   ├── otpService.js             # OTP generation
│   ├── serverEncryption.js       # Server-side encryption
│   ├── statementParser.js        # Bank statement parsing
│   ├── utils.js                  # Utility functions
│   ├── validations.js            # Input validation
│   ├── validationSchemas.js      # Zod schemas
│   └── voiceProcessor.js         # Voice processing
│
├── models/                       # MongoDB Schemas
│   ├── User.js                   # User model
│   ├── UserProfile.js            # User profile model
│   ├── Debt.js                   # Debt tracking model
│   └── Transaction.js            # Transaction model
│
├── public/                       # Static Assets
│   ├── icons/                    # PWA icons (72-512px)
│   ├── assets/                   # Images and media
│   ├── manifest.json             # PWA manifest
│   ├── sw.js                     # Service worker
│   ├── robots.txt                # SEO
│   └── sitemap.xml               # SEO
│
├── scripts/                      # Utility Scripts
│   ├── cleanup-duplicate-profiles.js
│   ├── setup-database-indexes.js
│   ├── test-mongodb-connection.js
│   └── verify-auth-config.js
│
├── utils/                        # Testing Utilities
│   ├── testBudgetSave.js
│   └── testVoiceProcessor.js
│
├── package.json                  # Dependencies
├── next.config.mjs               # Next.js configuration
├── tailwind.config.js            # Tailwind configuration
├── middleware.js                 # Next.js middleware
├── components.json               # Shadcn/UI configuration
└── README.md                     # Project documentation
```

---

## 7. Feature Implementation Details

### 7.1 Smart Expense Tracking

**Location:** `components/expenses/`, `app/api/expenses/`

**Features:**

- Real-time expense logging with instant categorization
- Voice expense entry via Web Speech API
- Multi-language support (Hindi, English, Marathi)
- Category-wise analytics and trends
- Receipt OCR processing (planned)

**Voice Processing Flow:**

```
User speaks → Speech Recognition → NLP Processing →
Expense Extraction → Category Detection → Database Save →
Agent Analysis → User Feedback
```

### 7.2 Intelligent Budgeting

**Location:** `lib/budgetGenerator.js`, `lib/advancedBudgetEngine.js`

**AI Budget Generation:**

- Analyzes user profile (income, city, family size, age)
- Uses Google Gemini AI for personalized recommendations
- City-specific cost adjustments (Mumbai, Delhi, Bangalore, etc.)
- Life stage considerations (student, working, retired)

**Budget Health Score:**

- 0-100 score based on allocation balance
- Savings rate analysis
- Housing burden assessment
- Lifestyle balance metrics

**Budget Categories:**

- Housing (rent/mortgage)
- Groceries & Essentials
- Transportation
- Utilities
- Healthcare
- Entertainment
- Personal Care
- Savings & Investments
- Debt Repayment
- Emergency Fund

### 7.3 Goal Management

**Location:** `components/goals/GoalTracker.js`, `app/api/goals/`

**Features:**

- Set savings goals with target amounts and dates
- Track debt payoff progress
- Investment goal planning
- Milestone-based progress tracking
- Celebration animations on achievements
- Goal recommendations from AI agents

### 7.4 Debt Management

**Location:** `models/Debt.js`, `app/api/debt/`

**Debt Types:**

- **Taken (Liability):** Loans taken from others
- **Given (Asset):** Loans given to others

**Features:**

- Track principal amount and interest rate
- Payment history tracking
- Due date reminders
- Status management (active, paid, overdue, defaulted)
- AI-powered payoff strategies

### 7.5 Investment Tracking

**Location:** `app/api/investment/`, `lib/investmentAlerts.js`

**Features:**

- Portfolio monitoring
- Asset allocation analysis
- Performance tracking
- Risk assessment
- Investment alerts and notifications

### 7.6 Voice Interface

**Location:** `components/voice/VoiceExpenseEntry.js`, `lib/voiceProcessor.js`

**Technical Implementation:**

- Web Speech API for speech recognition
- Multi-language support (Hindi primary with English fallback)
- Confidence scoring for transcriptions
- Alternative transcript handling for accuracy
- Audio quality assessment

**Voice Commands Supported:**

- "Add expense of ₹500 for food"
- "मैंने 200 रुपये खाने पर खर्च किए" (Hindi)
- "Spent 1000 on transport"

---

## 8. Database Models & Schema

### 8.1 User Model (`models/User.js`)

```javascript
{
  email: String,           // Unique, lowercase, indexed
  name: String,
  image: String,
  emailVerified: Date,
  preferences: {
    language: ['en', 'hi', 'hinglish'],
    currency: ['INR', 'USD', 'EUR', 'GBP', 'JPY', 'AUD', 'CAD'],
    timezone: String,
    dateFormat: ['DD/MM/YYYY', 'MM/DD/YYYY', 'YYYY-MM-DD'],
    numberFormat: ['indian', 'international'],
    notifications: {
      email: Boolean,
      push: Boolean,
      budgetAlerts: Boolean,
      goalReminders: Boolean,
      weeklyReports: Boolean,
      monthlyReports: Boolean
    },
    privacy: {
      shareData: Boolean,
      analytics: Boolean
    }
  }
}
```

### 8.2 UserProfile Model (`models/UserProfile.js`)

```javascript
{
  userId: ObjectId,        // Reference to User
  monthlyIncome: Number,   // Min: 1000
  incomeSource: ['salary', 'business', 'freelance', 'other'],
  city: String,
  familySize: Number,      // 1-20
  age: Number,             // 18-100
  occupation: String,
  generatedBudget: Mixed,  // AI-generated budget object
  budgetHealthScore: Number, // 0-100
  lastBudgetGenerated: Date,
  budgetPreferences: {
    language: String,
    spendingStyle: String
  }
}
```

### 8.3 Debt Model (`models/Debt.js`)

```javascript
{
  userId: ObjectId,
  type: ['taken', 'given'],
  name: String,            // Lender/Borrower name
  amount: Number,          // Original amount
  interestRate: Number,    // 0-100%
  duration: Number,        // Months (1-600)
  remainingBalance: Number,
  dueDate: Date,
  description: String,
  status: ['active', 'paid', 'overdue', 'defaulted'],
  payments: [{
    amount: Number,
    date: Date,
    note: String
  }]
}
```

### Database Indexes

- `users.email` - Unique index for fast lookups
- `userProfiles.userId` - Unique index for user-profile relationship
- `debts.userId` + `debts.status` - Compound index for filtering
- `debts.dueDate` - Index for reminder queries

---

## 9. API Endpoints

### Authentication APIs

| Endpoint                    | Method   | Description            |
| --------------------------- | -------- | ---------------------- |
| `/api/auth/[...nextauth]`   | GET/POST | NextAuth.js handler    |
| `/api/auth/register`        | POST     | User registration      |
| `/api/auth/verify-email`    | POST     | Email verification     |
| `/api/auth/forgot-password` | POST     | Password reset request |
| `/api/auth/reset-password`  | POST     | Password reset         |

### Budget APIs

| Endpoint               | Method | Description            |
| ---------------------- | ------ | ---------------------- |
| `/api/budget`          | GET    | Get user's budget      |
| `/api/budget`          | POST   | Create new budget      |
| `/api/budget/save`     | POST   | Save customized budget |
| `/api/budget/generate` | POST   | AI-generate budget     |

### Expense APIs

| Endpoint             | Method | Description    |
| -------------------- | ------ | -------------- |
| `/api/expenses`      | GET    | List expenses  |
| `/api/expenses`      | POST   | Add expense    |
| `/api/expenses/[id]` | PUT    | Update expense |
| `/api/expenses/[id]` | DELETE | Delete expense |

### Goal APIs

| Endpoint          | Method | Description |
| ----------------- | ------ | ----------- |
| `/api/goals`      | GET    | List goals  |
| `/api/goals`      | POST   | Create goal |
| `/api/goals/[id]` | PUT    | Update goal |
| `/api/goals/[id]` | DELETE | Delete goal |

### Debt APIs

| Endpoint            | Method | Description    |
| ------------------- | ------ | -------------- |
| `/api/debt`         | GET    | List debts     |
| `/api/debt`         | POST   | Create debt    |
| `/api/debt/[id]`    | PUT    | Update debt    |
| `/api/debt/[id]`    | DELETE | Delete debt    |
| `/api/debt/payment` | POST   | Record payment |

### Profile APIs

| Endpoint          | Method | Description           |
| ----------------- | ------ | --------------------- |
| `/api/profile`    | GET    | Get profile           |
| `/api/profile`    | POST   | Create/Update profile |
| `/api/onboarding` | POST   | Complete onboarding   |

### Voice APIs

| Endpoint             | Method | Description         |
| -------------------- | ------ | ------------------- |
| `/api/voice`         | POST   | Process voice input |
| `/api/voice/expense` | POST   | Voice expense entry |

### Utility APIs

| Endpoint             | Method   | Description             |
| -------------------- | -------- | ----------------------- |
| `/api/health`        | GET      | Health check            |
| `/api/health-check`  | GET      | Detailed health check   |
| `/api/notifications` | GET/POST | Notification management |

---

## 10. Authentication System

### Providers

1. **Google OAuth**

   - One-click sign-in
   - Automatic email verification
   - Profile picture sync

2. **Credentials (Email/Password)**
   - Email verification required
   - Password hashing with bcryptjs
   - Secure session management

### Security Features

- **JWT Sessions** - 30-day expiry with 24-hour refresh
- **Password Hashing** - bcryptjs with salt rounds
- **CSRF Protection** - Built-in NextAuth protection
- **Secure Cookies** - HTTP-only, secure flags
- **Rate Limiting** - API route protection

### Authentication Flow

```
User Sign Up → Email Verification → Profile Creation →
Onboarding Quiz → Dashboard Access
```

### Session Management

```javascript
session: {
  strategy: "jwt",
  maxAge: 30 * 24 * 60 * 60,  // 30 days
  updateAge: 24 * 60 * 60,    // Refresh every 24 hours
}
```

---

## 11. Internationalization (i18n)

### Supported Languages

| Language | Code       | Coverage |
| -------- | ---------- | -------- |
| English  | `en`       | 100%     |
| Hindi    | `hi`       | 100%     |
| Hinglish | `hinglish` | 100%     |
| Marathi  | `mr`       | Planned  |

### Implementation

**Library:** i18next + react-i18next

**Translation Structure:**

```javascript
{
  en: {
    translation: {
      "nav.features": "Features",
      "nav.dashboard": "Dashboard",
      "dashboard.welcome": "Welcome",
      "features.ai.title": "AI-Powered Insights",
      // ... 200+ translation keys
    }
  },
  hi: {
    translation: {
      "nav.features": "विशेषताएं",
      "nav.dashboard": "डैशबोर्ड",
      // ...
    }
  }
}
```

### Indian Context Features

- **Number Formatting:** Indian system (lakh, crore) vs international
- **Date Format:** DD/MM/YYYY default for India
- **Currency:** INR with ₹ symbol
- **Festival Budgeting:** Diwali, Holi, etc. considerations
- **Voice:** Hindi speech recognition with English fallback

---

## 12. Progressive Web App (PWA)

### Manifest Configuration

```json
{
  "name": "WealthWise - Smart Financial Planner",
  "short_name": "WealthWise",
  "start_url": "/dashboard",
  "display": "standalone",
  "theme_color": "#10b981",
  "background_color": "#ffffff",
  "orientation": "portrait-primary"
}
```

### PWA Features

- ✅ **Installable** - Add to home screen on mobile/desktop
- ✅ **Offline Support** - Service worker caching
- ✅ **Push Notifications** - Real-time alerts
- ✅ **App Shortcuts** - Quick actions from home screen
- ✅ **Responsive** - Works on all screen sizes

### App Shortcuts

1. **Add Expense** - Quick expense entry
2. **View Budget** - Budget overview
3. **Track Goals** - Goal progress
4. **AI Assistant** - Voice assistant

### Icon Sizes

- 72x72, 96x96, 128x128, 144x144, 152x152, 192x192, 384x384, 512x512

---

## 13. Event-Driven Architecture

### Event Bus Implementation

**Location:** `lib/eventBus.js`, `lib/events/EventBus.js`

```javascript
class EventBus {
  constructor() {
    this.listeners = new Map();
  }

  on(event, callback) {
    /* Subscribe */
  }
  emit(event, data) {
    /* Publish */
  }
  off(event) {
    /* Unsubscribe */
  }
}
```

### Event Types

| Event                         | Trigger                | Listeners           |
| ----------------------------- | ---------------------- | ------------------- |
| `EXPENSE_ADDED`               | New expense created    | All agents          |
| `INCOME_ADDED`                | Income recorded        | Income Agent        |
| `BUDGET_CREATED`              | Budget generated       | All agents          |
| `AGENT_ACTION`                | Agent takes action     | Dashboard UI        |
| `AGENT_ALERT`                 | Agent sends alert      | Notification system |
| `AGENT_RECOMMENDATION`        | Agent suggests action  | Dashboard UI        |
| `INCOME_VARIABILITY_DETECTED` | High variability found | Coach Agent         |
| `ANOMALY_DETECTED`            | Unusual spending       | Alert system        |
| `VOICE_EXPENSE_DETECTED`      | Voice input processed  | Spending Agent      |

### Event Flow Example

```
User adds expense →
  EXPENSE_ADDED event emitted →
    Income Agent: Checks income patterns →
    Spending Agent: Learns pattern, checks budget →
    Coach Agent: Prepares contextual advice →
      AGENT_ACTION events emitted →
        Dashboard UI updates in real-time
```

---

## 14. Development Timeline & Updates

### Phase 1: Foundation (Initial Setup)

- ✅ Next.js 15 project setup with App Router
- ✅ MongoDB integration with Mongoose
- ✅ Basic authentication with NextAuth.js
- ✅ Core UI components with Tailwind CSS
- ✅ Project structure established

### Phase 2: Core Features

- ✅ User registration and login
- ✅ Profile management and onboarding
- ✅ Expense tracking CRUD operations
- ✅ Budget creation and display
- ✅ Goal tracking system

### Phase 3: AI Integration

- ✅ Google Gemini AI integration
- ✅ AI-powered budget generation
- ✅ Budget health scoring system
- ✅ Personalized recommendations
- ✅ Multi-language AI responses

### Phase 4: Autonomous Agents

- ✅ Base Agent class implementation
- ✅ Income Variability Agent
- ✅ Spending Pattern Agent
- ✅ Event Bus architecture
- ✅ Real-time agent dashboard
- ✅ Proactive intervention system

### Phase 5: Voice & i18n

- ✅ Voice expense entry with Web Speech API
- ✅ Hindi language support
- ✅ Hinglish translations
- ✅ Indian number formatting
- ✅ Language auto-detection

### Phase 6: PWA & Polish

- ✅ PWA manifest and service worker
- ✅ Offline functionality
- ✅ Push notifications setup
- ✅ App shortcuts
- ✅ Performance optimization

### Phase 7: MumbaiHacks 2025 Preparation

- ✅ Live demo deployment on Vercel
- ✅ Documentation completion
- ✅ Demo scenarios preparation
- ✅ Presentation materials
- ✅ Final testing and bug fixes

---

## 15. Deployment & Infrastructure

### Production Environment

- **Platform:** Vercel
- **URL:** https://wealthwise-mumbaihack.vercel.app/
- **Database:** MongoDB Atlas
- **CDN:** Vercel Edge Network

### Environment Variables

```env
# Database
MONGODB_URI=mongodb+srv://...

# Authentication
NEXTAUTH_SECRET=...
NEXTAUTH_URL=https://wealthwise-mumbaihack.vercel.app

# Google OAuth
GOOGLE_CLIENT_ID=...
GOOGLE_CLIENT_SECRET=...

# AI
GEMINI_API_KEY=...

# Voice (Optional)
NEXT_PUBLIC_VAPI_PUBLIC_KEY=...
```

### Build Configuration

```json
{
  "scripts": {
    "dev": "next dev --turbopack",
    "build": "next build",
    "start": "next start",
    "lint": "next lint"
  }
}
```

### Performance Optimizations

- **Turbopack** - Fast development builds
- **Server Components** - Reduced client JavaScript
- **Image Optimization** - Next.js Image component
- **Code Splitting** - Automatic route-based splitting
- **Edge Caching** - Vercel CDN caching

---

## 16. Future Roadmap

### Short-term (Next 3 months)

- [ ] Receipt OCR with AI categorization
- [ ] Bank statement import (PDF/CSV)
- [ ] Investment portfolio integration
- [ ] Enhanced voice commands
- [ ] Marathi language support

### Medium-term (3-6 months)

- [ ] UPI transaction sync
- [ ] Credit score integration
- [ ] Tax planning features
- [ ] Family budget sharing
- [ ] Bill payment reminders

### Long-term (6-12 months)

- [ ] Native mobile apps (iOS/Android)
- [ ] Open banking API integration
- [ ] AI financial advisor chat
- [ ] Automated savings transfers
- [ ] Investment recommendations

### Technical Improvements

- [ ] Redis caching layer
- [ ] WebSocket real-time updates
- [ ] GraphQL API option
- [ ] Advanced analytics dashboard
- [ ] A/B testing framework

---

## 📞 Support & Contact

- **Live Demo:** [wealthwise-mumbaihack.vercel.app](https://wealthwise-mumbaihack.vercel.app/)
- **GitHub:** [TechWithAkash/mumbaiHack2025](https://github.com/TechWithAkash/mumbaiHack2025)
- **Issues:** [GitHub Issues](https://github.com/TechWithAkash/mumbaiHack2025/issues)

---

## 🏆 MumbaiHacks 2025

**Team:** TechWithAkash  
**Track:** Fintech  
**Status:** Submitted

---

_This document provides a complete end-to-end context of the WealthWise project. For specific implementation details, refer to the source code and inline documentation._

**Document Version:** 1.0  
**Last Updated:** December 5, 2025
