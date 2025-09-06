# Overview

**Vibe** is a trendy full-stack neighborhood events discovery app with violet theming that recommends local activities based on demographics within a 10-mile radius. The platform connects to real-time event APIs (Ticketmaster) to show actual concerts, sports events, family activities, and community events happening nearby. Users can browse events by category, create profiles based on family composition, save favorite events, and view detailed event information.

# User Preferences

Preferred communication style: Simple, everyday language.

# System Architecture

## Frontend Architecture
The client is built using **React 18** with **TypeScript** and follows a component-based architecture:
- **UI Framework**: Uses shadcn/ui components built on Radix UI primitives for consistent, accessible design
- **Styling**: Tailwind CSS with custom theme variables for dark mode and glassmorphism effects
- **State Management**: TanStack Query (React Query) for server state management with custom query client
- **Routing**: Wouter for lightweight client-side routing
- **Build Tool**: Vite for fast development and optimized production builds
- **Form Handling**: React Hook Form with Zod validation for type-safe forms

The frontend follows a modular structure with reusable UI components, custom hooks for location services and mobile detection, and pages organized by feature.

## Backend Architecture  
The server uses **Express.js** with **TypeScript** in ESM mode:
- **API Design**: RESTful endpoints following resource-based patterns (/api/users, /api/events, /api/favorites)
- **Data Layer**: Abstracted storage interface (IStorage) with in-memory implementation for development, designed for easy swapping to database persistence
- **Middleware**: Request logging, JSON parsing, and error handling with structured error responses
- **Development Integration**: Vite middleware integration for seamless full-stack development experience

The server architecture separates concerns between routing, storage, and business logic, making it extensible and testable.

## Data Storage Solutions
Currently uses **in-memory storage** with sample data seeding for development. The storage interface is designed to easily transition to:
- **PostgreSQL** database with Drizzle ORM (configuration already present)
- **Connection pooling** via @neondatabase/serverless for production deployment
- **Type-safe schemas** using drizzle-zod for runtime validation

## Database Schema Design
Defines three main entities with proper relationships:
- **Users**: Profile types (family, couple, single, senior), demographics, interests, and location data
- **Events**: Categorized events with scheduling, location, pricing, and organizer information  
- **User Favorites**: Many-to-many relationship between users and events for bookmarking

## Authentication and Authorization
Currently implements a **simplified user system** with localStorage-based user identification. The architecture is prepared for more robust authentication with session management via connect-pg-simple.

## External Dependencies
- **UI Components**: Radix UI primitives for accessible, unstyled components
- **Styling**: Tailwind CSS for utility-first styling with custom design tokens
- **Database**: Drizzle ORM with PostgreSQL dialect for type-safe database operations
- **Validation**: Zod for runtime type validation and schema parsing
- **Development**: Replit-specific plugins for enhanced development experience in the Replit environment
- **Geolocation**: Browser Geolocation API with reverse geocoding via BigDataCloud API for location services
- **Date Handling**: date-fns for date manipulation and formatting
- **Build Tools**: ESBuild for server bundling, PostCSS for CSS processing