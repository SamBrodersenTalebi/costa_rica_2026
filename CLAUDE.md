# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a single-file static HTML application for planning a Costa Rica 2026 trip. The app is written in Danish and provides two travel route options (Pacific coast and Coast-to-Coast) with detailed information about destinations, accommodations, activities, and food recommendations.

## Running the Application

Simply open [index.html](index.html) in a web browser. No build process, dependencies, or local server required.

## Architecture

### Single-File Structure
The entire application lives in [index.html](index.html) and consists of three main sections:
- `<style>` block: Custom CSS (lines 11-79) that extends Tailwind
- `<body>`: HTML structure with navigation, sidebar, and content areas (lines 81-282)
- `<script>` block: Vanilla JavaScript for interactivity (lines 285-643)

### Data Structure
The core data model defines destinations with this enhanced schema:
```javascript
{
  title: string,
  icon: emoji,
  desc: string,
  transport: string (HTML),
  images: {
    hero: string (Unsplash URL)
  },
  hotels: {
    romantic: [{ name, desc, map, book, image? }],
    budget: [{ name, desc, map, book, image? }]
  },
  romantic: { date: string, extras: [] },
  activities: [{ title, text }],
  hikes: [{ title, text, alltrails, map }],
  surf: { show: boolean, title?: string, text?: string },
  nature: string,
  music: string (HTML),
  food: { break: [], lunch: [], dinner: [] },
  practical: {
    nights: string,
    budget: string (HTML),
    notes: string[],
    timing: string
  }
}
```

Destinations: `sjo` (San José), `lafortuna` (La Fortuna), `monteverde` (Monteverde), `teresa` (Santa Teresa), `manuel` (Manuel Antonio), `puerto` (Puerto Viejo)

### Route System
Two predefined routes (lines 512-528):
- `pacific`: SJO → La Fortuna → Monteverde → Santa Teresa → SJO
- `coast`: SJO → Puerto Viejo → La Fortuna → Monteverde → Manuel Antonio → SJO

### UI Components
- **Route Switcher**: Toggle between Pacific/Coast routes
- **Sidebar Navigation**: Dynamic destination list based on selected route
- **Tab System**: Five tabs per destination (Hotels, Activities, Romantic, Food & Music, Practical Info)
- **Hero Images**: Full-width destination images from Unsplash with gradient overlay
- **Hotel Cards**: Image thumbnails (lazy loaded) with booking links
- **Hike Cards**: AllTrails integration with prominent trail information
- **Content Rendering**: Dynamic HTML generation from data structure

### Visual Features

- **Hero Images**: Each destination has a large hero image (1200x600px) sourced from Unsplash
- **Hotel Images**: Hotel cards display 400x300px thumbnail images
- **Lazy Loading**: Images use native browser lazy loading for performance
- **Image Animation**: Smooth opacity transitions when images load

### External Dependencies (CDN)
- Tailwind CSS for styling
- Phosphor Icons for iconography
- Google Fonts: Playfair Display (serif headings) + Lato (body text)

### Key Functions
- `setRoute(routeId)`: Switches between routes and rebuilds sidebar (lines 532-548)
- `loadDest(id, el)`: Loads destination data and renders all tabs (lines 550-633)
- `switchTab(tabId)`: Manages tab visibility (lines 635-640)
- `gMap(query)` / `booking(query)`: Helper functions for external links (lines 287-288)

## Mobile Responsiveness

The app is fully optimized for mobile devices with:

- **Horizontal Scrollable Tabs**: On mobile (<768px), tabs scroll horizontally to prevent wrapping
- **Single Column Layouts**: All grids convert to single column on mobile
- **Touch-Friendly**: Minimum 44px touch targets for all interactive elements
- **Responsive Images**: Hero images adjust height (12rem on mobile vs 20rem on desktop)
- **Optimized Padding**: Reduced padding on mobile for better content visibility

## AllTrails Integration

All hiking trails link to AllTrails for detailed trail information:

- **Primary Link**: AllTrails profile with trail details, reviews, and maps
- **Secondary Link**: Google Maps for directions to trailhead
- **Trail Info**: Distance and estimated time included in descriptions
- Covers 15+ hikes across all 6 destinations

## Content Updates

When adding or modifying destinations:

1. Add/update entries in the `data` object
2. Update `routes` object if adding new destinations to itineraries
3. Ensure all data fields follow the enhanced schema (including images, practical info, AllTrails links)
4. Use Danish language for all user-facing content
5. Include Google Maps links via `gMap()` helper and Booking.com links via `booking()` helper
6. Add hero image URLs from Unsplash with proper dimensions (?w=1200&h=600&fit=crop&auto=format)
7. Include AllTrails links for all hikes
8. Provide practical information (recommended nights, budget, important notes, best timing)

## Recent Enhancements (Dec 2025)

- ✅ Added hero images for all 6 destinations
- ✅ Added hotel thumbnail images (24 hotels total)
- ✅ Integrated AllTrails links for all 15+ hikes
- ✅ Improved mobile UX (scrollable tabs, responsive grids, 44px touch targets)
- ✅ Expanded food content 2.5x (San José & La Fortuna: 5 options per meal type)
- ✅ Added "Praktisk Info" tab with travel planning details
- ✅ Implemented lazy loading for images
- ✅ Added image loading animations
