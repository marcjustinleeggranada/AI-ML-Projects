# McDonald's App Redesign

A high-fidelity, interactive prototype of a redesigned McDonald's mobile ordering app, built as a single self-contained HTML file rendered inside a realistic phone mockup frame.

![McDonald's Logo](mcdo-logo.png)

## Overview

This project reimagines the McDonald's mobile app experience end-to-end — from an onboarding splash screen through browsing, deal redemption, checkout, and live order tracking. It's built entirely in vanilla HTML, CSS, and JavaScript with no frameworks or build tools, making it easy to open directly in a browser and interact with.

## Tech Stack

- **HTML5** — structure and markup
- **CSS3** — custom properties (CSS variables) for theming, flexbox/grid layouts, animations and transitions
- **Vanilla JavaScript** — all interactivity (tab switching, cart logic, timers, filtering)
- **Google Fonts** — [Figtree](https://fonts.google.com/specimen/Figtree) as the primary typeface
- No external JS libraries or frameworks — everything is dependency-free

## Design System

| Token | Value | Usage |
|---|---|---|
| `--mcd-red` | `#DA291C` | Primary brand red (buttons, accents) |
| `--mcd-yellow` | `#FFC72C` | Primary brand yellow (CTAs, highlights) |
| `--mcd-yellow-light` | `#FFF3C4` | Soft yellow backgrounds |
| `--mcd-dark` | `#1A1A1A` | Primary text / dark surfaces |
| `--mcd-grey` / `--mcd-grey-mid` | `#F5F5F5` / `#E8E8E8` | Neutral backgrounds and dividers |

Border radii are tokenized (`--radius-lg`, `--radius-md`, `--radius-sm`) for consistent rounding across cards, buttons, and sheets.

## App Structure

The prototype is presented inside a realistic phone frame with a notch, status bar, and a floating nav-tab switcher (for demo navigation) above the device. Four main sections are accessible via both the top demo switcher and the in-app bottom navigation bar:

### 1. Splash / Onboarding Screen
- Full-screen intro shown on load with the McDonald's logo, headline, and supporting copy
- **Log in** and **Sign up** actions dismiss the splash with a fade/scale transition

### 2. Home
- **Delivery / Pick Up toggle** to switch fulfillment mode app-wide
- Personalized greeting and estimated delivery time/address
- **Exclusive Deals carousel** linking into the Deals tab
- **Order Again** card for quick reordering of a saved usual (adds directly to cart)
- **Browse by category** pills (Burgers, McCafé, Chicken, Fries, Salads, Desserts) that jump into the Menu tab pre-filtered

### 3. Menu
- Horizontally scrollable category chips (Burgers, McCafé, Chicken, Sides, Drinks, Desserts)
- Two-column grid of menu items with image, calories, and price
- Quick **"+" add-to-cart** button on each card (without opening details)
- Tapping a card opens a **bottom sheet** with full item detail: description, allergen tags, nutritional highlights, and an "Add to Cart" action

### 4. Deals
- List of app-exclusive deals with original vs. app price, savings amount, and validity (Delivery / Pick Up)
- Filter bar: **All** vs **Available Now** (reacts to the current fulfillment mode)
- Deals not valid for the current mode are visually greyed out with an overlay message
- **Redeem Now** opens a full-screen **QR code modal** with:
  - A live 5-minute countdown timer
  - A backup alphanumeric code for manual entry
  - Automatic "Code Expired" state with a **regenerate** action once the timer hits zero

### 5. Checkout
- Delivery address (inline-editable text field) or Pick-Up store details, shown conditionally based on fulfillment mode
- **Payment method selector** (Visa on file vs. Apple Pay) with radio-style selection that updates the order button's label and styling
- **Order summary**: aggregated cart items with quantity, line totals, remove buttons, delivery fee (waived for pickup), taxes, and any applied deal discount
- Empty-cart state when no items have been added
- **Place Order** button with dynamic total, which triggers an animated **order tracker**:
  - Order Received → Preparing → Driver En Route → Delivered
  - Steps progress automatically on a timer with updated timestamps
  - Final state shows an arrival message and a "Rate Your Order" action

## Key Interactions Implemented

- Tab/state switching without page reloads (all screens live in one DOM, toggled via CSS classes)
- Cart state management (add, quick-add, remove, aggregate quantities, live subtotal/tax/total calculation)
- Conditional UI based on fulfillment mode (delivery vs. pickup) across Home, Deals, and Checkout
- Simulated real-time elements: QR countdown timer and multi-stage order tracker with `setTimeout`-driven progression
- Responsive bottom-sheet modal pattern for menu item details

## Assets

| File | Description |
|---|---|
| `mcdo-logo.png` | McDonald's logo used on the splash screen |
| `splash-icon.png` | Decorative sparkle icon accompanying the splash headline |

## How to Run

1. Clone or download this repository
2. Ensure `mcdo-logo.png` and `splash-icon.png` are in the same directory as the HTML file
3. Open the HTML file directly in any modern browser — no build step or server required

## Notes

This is a front-end prototype for design/UX exploration purposes. All menu items, prices, and deals are placeholder data for demonstration only and are not reflective of actual McDonald's pricing or offerings.
