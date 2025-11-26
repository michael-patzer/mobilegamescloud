# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a website for Mobile Card Games & Travel Apps LLC, showcasing iOS mobile applications with a focus on color identification, paint matching, and mobile utilities. The website serves as a portfolio and landing page for multiple iOS apps.

## Architecture

The website is organized as a multi-app showcase with the following structure:

- **Main site** (`index.html`): Primary landing page featuring app portfolio and company information
- **App-specific pages**: Individual landing pages for each app (`color/`, `paint/`, `identifier/`, `aso/`, etc.)
  - Each app directory contains its own `index.html` with dedicated styling and screenshots
  - Apps feature iOS-style design with App Store integration
- **Twilio service** (`twilio/`): Node.js Express service for SMS notifications
- **Static assets**: App icons, screenshots, and promotional images organized by app

## Key Components

### Main Website Architecture (index.html)
- **Dynamic App Grid**: JavaScript-powered app grid that dynamically loads app information from iTunes API using `APP_IDS` array (lines 842-854)
- **iTunes API Integration**: Fetches app metadata including name, description, icons, and screenshots with fallback for different screenshot formats
- **Campaign Tracking**: Uses `CAMPAIGN_TAG` for App Store attribution tracking
- **Modal System**: Contact forms for services (localization, app updates) with form submission handling
- **SEO Optimization**: Structured data generation for each app, comprehensive meta tags
- **Responsive Design**: iOS-inspired styling with CSS Grid and Flexbox layouts

### App Landing Pages Structure
- Individual showcase pages for each mobile app in dedicated directories
- Screenshot galleries with iOS device frames
- App Store download links with campaign tracking
- Responsive design optimized for mobile viewing
- SEO-optimized with structured data and meta tags

### Twilio SMS Service (`twilio/`)
- Express.js server with CORS enabled for cross-origin requests
- Single endpoint `/send-sms` accepting POST requests with `phone`, `appName`, `appLink` fields
- Environment variable configuration for credentials
- Designed for deployment on Google Cloud Run (port handling via `process.env.PORT`)

## Development Commands

### Twilio Service
```bash
cd twilio
npm install
npm start  # Starts on port 8080 or process.env.PORT
```

### Static Website
No build process required - static HTML/CSS/JS files served directly from any static hosting.

## Key Configuration

### App Integration System
- **APP_IDS Array**: Core app IDs for iTunes API fetching (index.html:842-854)
- **CAMPAIGN_TAG**: Attribution tracking for App Store links (index.html:856)
- **Dynamic Content Loading**: Apps load asynchronously on page load via `loadApps()` function
- **Screenshot Handling**: Supports both legacy and iOS 17+ screenshot format structures

### API Integration Patterns
- iTunes Store API integration for real-time app metadata
- Fallback handling for different screenshot formats and missing data
- Campaign attribution tracking on all App Store links
- Structured data generation for SEO optimization

### Modal and Form System
- Service inquiry modals with form validation
- FormSubmit.co integration for form handling without backend
- Success message display and modal state management
- Keyboard accessibility (ESC key support)

## Environment Variables (Twilio Service)

Required for Twilio SMS functionality:
- `TWILIO_ACCOUNT_SID`: Twilio account identifier
- `TWILIO_AUTH_TOKEN`: Twilio authentication token  
- `TWILIO_PHONE_NUMBER`: Twilio phone number for sending SMS
- `PORT`: Server port (defaults to 8080 for Cloud Run compatibility)

## Deployment Architecture

- **Main Website**: Static hosting (GitHub Pages, Netlify, Vercel, etc.)
- **Twilio Service**: Google Cloud Run or similar Node.js hosting platform
- **Assets**: Static files served directly from hosting provider
- **Domain Configuration**: CNAME files in app subdirectories for custom domains