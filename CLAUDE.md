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
The core data model (lines 290-510) defines destinations with this schema:
```javascript
{
  title: string,
  icon: emoji,
  desc: string,
  transport: string (HTML),
  hotels: { romantic: [], budget: [] },
  romantic: { date: string, extras: [] },
  activities: [],
  hikes: [],
  surf: { show: boolean, title?: string, text?: string },
  nature: string,
  music: string (HTML),
  food: { break: [], lunch: [], dinner: [] }
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
- **Tab System**: Four tabs per destination (Hotels, Activities, Romantic, Food & Music)
- **Content Rendering**: Dynamic HTML generation from data structure

### External Dependencies (CDN)
- Tailwind CSS for styling
- Phosphor Icons for iconography
- Google Fonts: Playfair Display (serif headings) + Lato (body text)

### Key Functions
- `setRoute(routeId)`: Switches between routes and rebuilds sidebar (lines 532-548)
- `loadDest(id, el)`: Loads destination data and renders all tabs (lines 550-633)
- `switchTab(tabId)`: Manages tab visibility (lines 635-640)
- `gMap(query)` / `booking(query)`: Helper functions for external links (lines 287-288)

## Content Updates

When adding or modifying destinations:
1. Add/update entries in the `data` object
2. Update `routes` object if adding new destinations to itineraries
3. Ensure all data fields follow the schema (hotels, romantic, activities, hikes, surf, nature, music, food)
4. Use Danish language for all user-facing content
5. Include Google Maps links via `gMap()` helper and Booking.com links via `booking()` helper
