# replit.md

## Overview

This is a full-stack web application for digital gift card management built with React frontend and Express backend. The application allows users to scan QR codes, activate gift cards with personal messages and videos, and redeem them through various payment methods. It features a mobile-first design with a comprehensive UI component library and real-time media handling capabilities.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter for client-side routing
- **UI Library**: shadcn/ui components built on Radix UI primitives
- **Styling**: Tailwind CSS with CSS custom properties for theming
- **State Management**: TanStack Query for server state, React hooks for local state
- **Build Tool**: Vite with hot module replacement and development plugins

### Backend Architecture
- **Runtime**: Node.js with Express framework
- **Language**: TypeScript with ES modules
- **API Design**: RESTful endpoints with Express middleware
- **File Handling**: Multer for video upload processing
- **Development**: TSX for TypeScript execution in development

### Data Storage Solutions
- **Database**: PostgreSQL with Drizzle ORM
- **Provider**: Neon Database (@neondatabase/serverless)
- **Schema Management**: Drizzle Kit for migrations and schema management
- **Development Storage**: In-memory storage class for testing and development

## Key Components

### Gift Card Management
- **Schema**: Comprehensive gift card model with status tracking (pending, activated, redeemed)
- **Validation**: Zod schemas for type-safe API requests and responses
- **File Storage**: Video attachment support for personalized messages
- **ID Generation**: Nanoid for unique gift card identifiers

### QR Code Scanning
- **Implementation**: HTML5 QR Code library integration
- **Camera Access**: MediaDevices API for camera functionality
- **Validation**: Custom gift card format validation (GC + 10 alphanumeric characters)
- **Error Handling**: Graceful fallbacks for camera access issues

### Video Recording
- **MediaRecorder API**: Native browser video recording capabilities
- **Format Support**: WebM with VP8/Opus codecs as primary, fallback to MP4
- **Constraints**: 30-second duration limit, 50MB file size limit
- **Quality Settings**: 1Mbps video bitrate, 128kbps audio bitrate

### UI Component System
- **Design System**: shadcn/ui with "new-york" style variant
- **Theme**: Custom color palette with primary (coral), secondary (teal), accent (yellow)
- **Responsive Design**: Mobile-first approach with max-width containers
- **Accessibility**: ARIA-compliant components with keyboard navigation

## Data Flow

### Gift Card Activation Flow
1. User scans QR code → Scanner component validates format
2. Frontend queries gift card status → Backend retrieves from database
3. If pending → Navigate to activation page
4. User fills form (sender, recipient, message, amount) → Form validation with Zod
5. Optional video recording → MediaRecorder API captures video
6. Submit activation → API call with form data and video blob
7. Backend updates gift card status and stores video file

### Gift Card Redemption Flow
1. Activated gift card scanned → Navigate to redemption page
2. Display gift card details and video message
3. User selects payment method (UPI, Bank Transfer, Digital Wallet)
4. Submit redemption → Backend processes payment and updates status
5. Success confirmation with payment details

### API Request Flow
- **Query Client**: TanStack Query manages server state with automatic caching
- **Error Handling**: Centralized error handling with toast notifications
- **Request Interceptor**: Automatic JSON headers and credential inclusion
- **Response Processing**: Type-safe response parsing with error boundaries

## External Dependencies

### Frontend Dependencies
- **React Ecosystem**: React 18, React DOM, React Hook Form with Zod resolvers
- **UI Libraries**: Radix UI primitives, Lucide React icons, Class Variance Authority
- **Utilities**: clsx for conditional classes, date-fns for date handling
- **Media**: Embla Carousel for component carousels

### Backend Dependencies
- **Database**: Drizzle ORM with PostgreSQL dialect, Neon serverless adapter
- **File Upload**: Multer for multipart form handling
- **Validation**: Drizzle Zod integration for schema validation
- **Session Management**: Connect-pg-simple for PostgreSQL session store

### Development Dependencies
- **Build Tools**: Vite, ESBuild for production builds
- **TypeScript**: Strict type checking with path mapping
- **Linting**: PostCSS with Tailwind CSS and Autoprefixer
- **Replit Integration**: Runtime error overlay and cartographer plugins

## Deployment Strategy

### Build Configuration
- **Development**: Vite dev server with HMR and TypeScript compilation
- **Production**: Vite build for client, ESBuild for server bundling
- **Assets**: Static file serving with Vite middleware in development

### Environment Setup
- **Node Version**: Node.js 20 with ES modules support
- **Database**: PostgreSQL 16 with connection via DATABASE_URL environment variable
- **File Storage**: Local uploads directory with configurable path

### Deployment Target
- **Platform**: Replit with autoscale deployment target
- **Port Configuration**: Internal port 5000, external port 80
- **Build Process**: npm run build followed by npm run start
- **Process Management**: Single process with graceful error handling

### Security Considerations
- **File Upload**: MIME type validation for video files only
- **CORS**: Credential inclusion for authenticated requests
- **Input Validation**: Comprehensive Zod schema validation on all endpoints
- **Error Sanitization**: Safe error messages without sensitive information exposure