# Overview

This is a full-stack investment wallet application built with a React frontend and Express.js backend. The application allows users to register with subscription amounts, provides an admin panel for user activation, and includes a user dashboard for viewing account information. The interface is primarily in Arabic, targeting Arabic-speaking users.

# System Architecture

## Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter for client-side navigation
- **State Management**: TanStack React Query for server state management
- **UI Framework**: Shadcn/UI components with Radix UI primitives
- **Styling**: Tailwind CSS with custom theme (green primary colors)
- **Build Tool**: Vite with custom configuration for client/server separation

## Backend Architecture
- **Framework**: Express.js with TypeScript
- **Runtime**: Node.js 20
- **Session Management**: Express sessions with memory store
- **Data Persistence**: Currently using in-memory storage (MemStorage class)
- **Build Strategy**: ESBuild for production bundling

## Key Components

### Authentication System
- User registration with username, password, and subscription amount
- Admin authentication with secret password
- Session-based authentication using express-session
- Role-based access control (regular users vs admin)

### User Management
- User registration with pending status by default
- Admin approval workflow for user activation
- User dashboard displaying account information and motivational content

### Database Schema (Drizzle ORM Ready)
- **Users table**: id, username, password, subscription_amount, is_active, start_date, created_at
- Schema defined in `shared/schema.ts` with Zod validation
- Currently uses PostgreSQL dialect with Neon serverless driver
- Drizzle configuration points to PostgreSQL but currently using memory storage

### UI/UX Design
- RTL (Right-to-left) support for Arabic text
- Responsive design with mobile-first approach
- Green theme with professional styling
- Toast notifications for user feedback
- Form validation with React Hook Form and Zod

## Data Flow

1. **User Registration**: Users submit registration form → Backend validates data → Stores in pending users list → Shows confirmation message
2. **Admin Activation**: Admin logs in with secret password → Views pending users → Activates selected users → Users become active
3. **User Login**: Users login with credentials → Backend validates against active users → Creates session → Redirects to dashboard
4. **Dashboard**: Authenticated users view their account info, subscription details, and motivational content

## External Dependencies

### Frontend Dependencies
- **UI Components**: Extensive Radix UI component library for accessible UI primitives
- **Form Handling**: React Hook Form with Zod resolvers for type-safe form validation
- **HTTP Client**: TanStack React Query for data fetching and caching
- **Date Utilities**: date-fns for date formatting and manipulation
- **Icons**: Lucide React for consistent iconography

### Backend Dependencies
- **Database**: @neondatabase/serverless for PostgreSQL connectivity (configured but not actively used)
- **ORM**: Drizzle ORM for type-safe database operations
- **Session Store**: connect-pg-simple for PostgreSQL session storage (when database is connected)
- **Development**: tsx for TypeScript execution in development

## Deployment Strategy

### Development Environment
- **Runtime**: Replit with Node.js 20, Web, and PostgreSQL 16 modules
- **Development Server**: Concurrent client and server with hot reload
- **Port Configuration**: Server runs on port 5000, externally accessible on port 80
- **File Watching**: Vite handles client-side hot reload, tsx handles server-side restart

### Production Build
- **Client Build**: Vite builds React app to `dist/public`
- **Server Build**: ESBuild bundles server code to `dist/index.js`
- **Static Assets**: Express serves built client files in production
- **Deployment Target**: Autoscale deployment on Replit infrastructure

### Database Migration Strategy
- Drizzle Kit configured for PostgreSQL migrations
- Migration files output to `./migrations` directory
- Schema changes managed through `drizzle-kit push` command
- Environment variable `DATABASE_URL` required for database operations

## Changelog

```
Changelog:
- June 17, 2025. Initial setup
```

## User Preferences

```
Preferred communication style: Simple, everyday language.
```