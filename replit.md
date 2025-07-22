# Stock Prediction Application

## Overview

This is a full-stack web application that provides AI-powered stock price predictions and analysis. The app features a React frontend with a Node.js/Express backend, integrating with Python-based machine learning models for stock market analysis. Uses modern technologies like Drizzle ORM for database management and shadcn/ui for the user interface components.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter for client-side routing
- **State Management**: TanStack Query (React Query) for server state management
- **UI Framework**: shadcn/ui components built on Radix UI primitives
- **Styling**: Tailwind CSS with CSS variables for theming
- **Build Tool**: Vite for development and production builds

### Backend Architecture
- **Runtime**: Node.js with Express.js
- **Language**: TypeScript with ES modules
- **API Style**: RESTful endpoints
- **File Handling**: Multer for image upload processing
- **Database ORM**: Drizzle ORM for type-safe database operations
- **Session Management**: Built-in session handling

### Database Design
- **Database**: PostgreSQL (configured via Drizzle)
- **Connection**: Neon Database serverless connection
- **Schema Management**: Drizzle Kit for migrations and schema management

#### Database Tables:
1. **users**: User authentication and management
   - id (serial, primary key)
   - username (text, unique)
   - password (text)

2. **stocks**: Stock information and metadata
   - id (serial, primary key)
   - symbol (text, unique)
   - name (text)
   - sector (text, nullable)
   - marketCap (real, nullable)
   - lastUpdated (timestamp)

3. **stockPrices**: Historical stock price data
   - id (serial, primary key)
   - stockId (foreign key to stocks)
   - date, open, high, low, close, volume
   - createdAt (timestamp)

4. **predictions**: AI-generated stock predictions
   - id (serial, primary key)
   - stockId (foreign key to stocks)
   - predictionDate, targetDate, predictedPrice
   - actualPrice (nullable), confidence, model
   - features (JSON string), processingTime
   - createdAt (timestamp)

## Key Components

### Frontend Components
- **Stock Selection Interface**: Dropdown for choosing stocks and prediction timeframes
- **Market Overview Cards**: Display of market gainers, losers, and most active stocks
- **Prediction Results Display**: Comprehensive AI prediction results with confidence scores
- **Recent Predictions Feed**: Historical predictions from the platform
- **Technical Analysis Panel**: RSI, volume, moving averages, and sentiment indicators

### Backend Services
- **Storage Layer**: Abstracted storage interface with in-memory implementation and sample stock data
- **Stock Prediction Service**: Mock LSTM-based prediction engine (ready for Python ML integration)
- **Market Analysis Engine**: Real-time market overview generation
- **API Routes**: RESTful endpoints for stock operations and prediction generation

### Shared Types
- **Stock Schema**: Complete stock information with market data
- **Prediction Schema**: AI prediction results with technical features
- **Market Analysis Types**: Structured market overview interfaces

## Data Flow

1. **Stock Selection**: User selects stock symbol and prediction timeframe
2. **API Request**: JSON payload sent to `/api/predict` endpoint
3. **AI Processing**: Mock LSTM model generates prediction with technical analysis
4. **Feature Analysis**: RSI, volume, moving averages, and sentiment calculation
5. **Storage**: Prediction results stored with full metadata
6. **Response**: Complete prediction results with confidence and features
7. **Display**: Results rendered with technical indicators and market context

## External Dependencies

### Production Dependencies
- **Database**: Neon Database (PostgreSQL serverless)
- **UI Components**: Radix UI primitives
- **File Processing**: Multer for uploads
- **Validation**: Zod for schema validation
- **HTTP Client**: TanStack Query for API calls

### Development Tools
- **Build**: Vite with React plugin
- **Database**: Drizzle Kit for schema management
- **TypeScript**: Full type safety across stack
- **Replit Integration**: Development environment optimizations

## Deployment Strategy

### Development Mode
- **Frontend**: Vite dev server with HMR
- **Backend**: tsx for TypeScript execution
- **Database**: Shared PostgreSQL instance
- **Environment**: Replit-optimized development setup

### Production Build
- **Frontend**: Vite build to `dist/public`
- **Backend**: esbuild bundle to `dist/index.js`
- **Static Serving**: Express serves built frontend
- **Database**: Production PostgreSQL connection

### Configuration Requirements
- `DATABASE_URL`: PostgreSQL connection string (required)
- File upload directory (`uploads/`) for temporary storage
- Environment-specific settings via `NODE_ENV`

### Key Architectural Decisions

1. **Monorepo Structure**: Frontend (`client/`), backend (`server/`), and shared code (`shared/`) in single repository for easier development and deployment.

2. **Type Safety**: Full TypeScript implementation with shared schemas ensures type consistency between frontend and backend.

3. **Storage Abstraction**: Interface-based storage layer allows easy switching between in-memory (development) and database (production) implementations.

4. **Stock Prediction Pipeline**: Mock LSTM neural network simulation with realistic technical analysis features.

5. **UI Component System**: shadcn/ui provides consistent, accessible components optimized for financial data display.

6. **Market Data Architecture**: Real-time market overview generation with gainers/losers analysis and volume tracking.

7. **Database Schema**: Comprehensive schema supporting stocks, historical prices, and AI predictions with full technical feature storage.

The application is designed to be easily extensible, with mock LSTM predictions ready to be replaced by actual Python ML models via subprocess calls, and a storage layer that can be enhanced with real financial data APIs.