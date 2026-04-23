<div align="center">
  <img 
    src="assets/Next.js 3D Parallax Web Experience Engine.png" 
    alt="Next.js 3D Parallax Web Experience Engine Logo Animation"
    width="100%"
  />

  <h1 style="font-size: 3em; font-weight: 800; margin: 0.4em 0 0;">
    Next.js 3D Parallax Web Experience Engine 
  </h1>

  <h3 style="margin-top: 0.6em;">
    Scroll-Driven Immersion. Cinematic UI. High-Performance Web Intelligence. 
  </h3>

  <p>
    <em>A production-grade, cinematic 3D web experience engine engineered to transform scrolling into immersive storytelling. Built with Next.js App Router, React 19, and TypeScript, it delivers ultra-smooth, frame-perfect parallax interactions powered by a 200-frame optimized WebP pipeline.  </em>
  </p>
</div>

## 🧾 Executive Summary
This project documents the successful modernization of the Olipop brand website into a Next.js 16 application. The project achieved all core objectives, including the implementation of a complex 200-frame scroll-driven parallax animation system, seamless variant switching logic with state management, and a highly responsive component-based architecture. The new system leverages React 19, TypeScript for reliability, and Tailwind CSS v4 for modern styling, delivering a premium, interactive user experience that maintains the original design's aesthetic fidelity while significantly improving maintainability and scalability.

## 📑 Table of Contents
- [🧩 Project Overview](#-project-overview)
- [🎯 Objectives & Goals](#-objectives--goals)
- [✅ Acceptance Criteria](#-acceptance-criteria)
- [💻 Prerequisites](#-prerequisites)
- [⚙️ Installation & Setup](#️-installation--setup)
- [🔗 API Documentation](#-api-documentation)
- [🖥️ UI / Frontend](#️-ui--frontend)
- [🔢 Status Codes](#-status-codes)
- [🚀 Features](#-features)
- [🧱 Tech Stack & Architecture](#-tech-stack--architecture)
- [🛠️ Workflow & Implementation](#️-workflow--implementation)
- [🧪 Testing & Validation](#-testing--validation)
- [🧰 Verification Testing Tools](#-verification-testing-tools)
- [🧯 Troubleshooting & Debugging](#-troubleshooting--debugging)
- [🔒 Security & Secrets](#-security--secrets)
- [☁️ Deployment (Vercel)](#️-deployment-vercel)
- [⚡ Quick-Start Cheat Sheet](#-quick-start-cheat-sheet)
- [🧾 Usage Notes](#-usage-notes)
- [🧠 Performance & Optimization](#-performance--optimization)
- [🌟 Enhancements & Features](#-enhancements--features)
- [🧩 Maintenance & Future Work](#-maintenance--future-work)
- [🏆 Key Achievements](#-key-achievements)
- [🧮 High-Level Architecture](#-high-level-architecture)
- [🗂️ Folder Structure (Tree)](#️-folder-structure-tree)
- [🧭 How to Demonstrate Live](#-how-to-demonstrate-live)
- [💡 Summary, Closure & Compliance](#-summary-closure--compliance)

## 🧩 Project Overview
The Olipop Next.js project is a rebuild of the customer-facing landing page. It features a sophisticated hero section with a scroll-controlled 3D product rotation (parallax), interactive flavor variant switching, and modular content sections (Reviews, Ingredients, Nutrition). The architecture is designed to be "production-ready," utilizing Server Components where possible and Client Components for interactivity.

## 🎯 Objectives & Goals
- **Modernization:** Migrate legacy HTML/JS to Next.js 16 App Router architecture.
- **Performance:** Optimize asset loading (specifically heavy image sequences) and improve Core Web Vitals.
- **Type Safety:** Implement strict TypeScript across all components and hooks.
- **Maintainability:** Componentize the UI using React enabling easier updates and AB testing.
- **UX Excellence:** Replicate and smooth out the detailed parallax interactions and animations.

## ✅ Acceptance Criteria
- Hero animation uses exactly 200 frames for optimal load/quality balance.
- Hero section stays fixed (z-0) while content sections scroll over it (z-10).
- Variant switching (Cherry, Grape, Lemon) updates all relevant UI elements (Hero image, Colors, Product section image) instantly.
- Buttons and layout are fully responsive down to mobile devices (375px width).
- No hydration errors or console warnings in the final build.

## 💻 Prerequisites
- **Node.js:** Version 20.x or higher
- **Package Manager:** npm (v10+) or pnpm
- **Git:** For version control
- **OS:** Windows, macOS, or Linux

## ⚙️ Installation & Setup
1. **Clone the repository:**
   ```bash
   git clone [repository-url]
   cd nextjs-parallax-web-experience
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Run development server:**
   ```bash
   npm run dev
   ```

4. **Build for production:**
   ```bash
   npm run build
   npm start
   ```

## 🔗 API Documentation
*Note: This project is primarily a frontend application. However, it interfaces with external storage for assets.*

- **Asset Source:** Supabase Object Storage
- **Endpoint Pattern:** `[BaseUrl]/[FrameNumber].webp`
- **Hook Interface (`useImagePreloader`):**
  - Input: `variant: Variant`
  - Output: `{ frames: HTMLImageElement[], isLoading: boolean, progress: number }`

## 🖥️ UI / Frontend

### Structure & State Flow
- **Global State:** `VariantContext` wraps the application layout, managing the `currentVariant` state globally.
- **Hero Component:** `ParallaxHero` consumes context to display the correct image sequence. It controls the window scroll interaction.
- **Content Sections:** `ProductSection`, `IngredientsSection`, etc., consume context to update content dynamically based on the selected flavor.

### Key Components
| Component | Path | Description |
|-----------|------|-------------|
| ParallaxHero | src/components/hero/ParallaxHero.tsx | Manages the scroll-driven frame animation (400vh height). |
| VariantSwitcher | src/components/hero/VariantSwitcher.tsx | Handles user input for changing flavors. |
| ProductSection | src/components/sections/ProductSection.tsx | Displays "Our Story" with dynamic product imagery. |

## 🔢 Status Codes
Application logic handles the following internal states:
- **Loading (0-99%):** `isLoading: true` in `useImagePreloader`. Blocks interaction.
- **Ready (100%):** `isLoading: false`. Unlocks scroll and reveals interface.
- **Error:** Failed asset loads trigger console errors but attempt to degrade gracefully.

## 🚀 Features
- **3D Parallax Scroll:** Smooth scrubbing through 200 high-res frames as the user scrolls.
- **Dynamic Theme Engine:** Background colors and asset paths switch instantly based on variant selection.
- **Asset Preloading:** Custom hook ensures smooth playback by pre-fetching image sequences.
- **Responsive Design:** Mobile-first approach using Tailwind CSS v4 breakpoints.
- **Component Encapsulation:** ShadCN UI primitives used for standard elements like Accordion and Separators.

## 🧱 Tech Stack & Architecture
- **Framework:** Next.js 16 (App Router)
- **Language:** TypeScript 5.x
- **UI Library:** React 19.2
- **Styling:** Tailwind CSS v4 + PostCSS
- **Animation:** Framer Motion + Native Scroll Events
- **Validation:** Zod
- **Assets:** WebP sequences hosted on Supabase

### Component Architecture Diagram
```
RootLayout (VariantProvider)
│
├── Navigation (Fixed)
│
├── Page (Home)
│   │
│   ├── LoadingScreen (Overlay)
│   │
│   ├── ParallaxHero (h-400vh, z-0)
│   │   ├── ParallaxBackground (Frames)
│   │   └── HeroContent (z-1)
│   │       ├── Header/Buttons
│   │       └── VariantSwitcher
│   │
│   ├── ProductSection (z-10)
│   ├── IngredientsSection (z-10)
│   ├── NutritionSection (z-10)
│   ├── ReviewsSection (z-10)
│   ├── FAQSection (z-10)
│   └── CTASection (z-10)
│
└── Footer
```

## 🛠️ Workflow & Implementation
1. **Setup:** Initialized Next.js project with TypeScript and Tailwind CSS.
2. **Data Modeling:** Defined `Variant` types and configured asset sources in `variants.ts`.
3. **Core Logic:** Implemented `useImagePreloader` to handle heavy asset fetching and `useParallax` for scroll calculations.
4. **Component Construction:** Built modular sections (Hero, Product, FAQ) using ShadCN UI primitives.
5. **State Integration:** Created `VariantContext` to link the Hero switcher with downstream sections.
6. **Refinement:** Adjusted Parallax timing (Extended height to 400vh) to fix overlap issues.
7. **Optimization:** Reduced frame count from 240 to 200 for better performance.

## 🧪 Testing & Validation
| ID | Area | Command / Action | Expected Output | Status |
|----|------|------------------|-----------------|--------|
| T-01 | Core | `npm run dev` | Server starts on port 3000 without error. | 🟢 PASS |
| T-02 | Parallax | Scroll down 3000px | Animation plays smoothly through frame 200 before content covers it. | 🟢 PASS |
| T-03 | Responsiveness | Resize width to 375px | Buttons stack vertically, layout adjusts to single column. | 🟢 PASS |
| T-04 | State Management | Click "Next" variant | Hero color, hero image, and "Our Story" product image update simultaneously. | 🟢 PASS |
| T-05 | Production Build | `npm run build` | Build completes with valid static generation and no lint errors. | 🟢 PASS |

## 🧰 Verification Testing Tools
The following tools were used to verify the integrity of the implementation:
- **ESLint:** Static code analysis for finding problems.
- **TypeScript Compiler (tsc)::** Type checking verification.
- **Browser DevTools:** Network throttling and z-index visualizer.
- **Browser Subagents:** Automated navigation and DOM inspection agents used during development.

## 🧯 Troubleshooting & Debugging
- **Issue: Hydration Mismatch.** *Fix:* Ensured no browser-extension specific attributes were interfering, and synchronized server/client rendering logic.
- **Issue: Next Section Overlap.** *Fix:* Increased Hero section height from 300vh to 400vh to accommodate the full 200-frame animation sequence.
- **Issue: Missing Images.** *Fix:* Verified Supabase URLs and configured `next.config.ts` (if needed for external domains, though basic `img` tags were used for raw frames).

## 🔒 Security & Secrets
- No sensitive API keys are exposed in the client bundle.
- Asset URLs are public and read-only.
- `next.config.ts` is configured to be secure by default.

## ☁️ Deployment (Vercel)
The project is optimized for Vercel deployment:
1. Push code to GitHub.
2. Import project in Vercel Dashboard.
3. Framework Preset: **Next.js**.
4. Build Command: `next build`.
5. Install Command: `npm install`.
6. Click **Deploy**.

## ⚡ Quick-Start Cheat Sheet
```bash
# Start Dev Server
npm run dev

# Build for Prod
npm run build

# Lint Code
npm run lint
```

## 🧾 Usage Notes
- Ensure a stable internet connection for asset loading (images are fetched from remote storage).
- The parallax effect relies on scroll events; extensive throttling is applied for performance, but very fast scrolling may skip frames visually.

## 🧠 Performance & Optimization
- **Lazy Loading:** Content sections below the fold are standard React components.
- **Image Optimization:** WebP format used for all animation frames.
- **Memory Management:** `useImagePreloader` manages the buffer to prevent memory leaks, though caching is leveraged for smoothness.
- **Code Splitting:** Next.js App Router automatically splits routes and components.

## 🌟 Enhancements & Features
- **Context API:** Introduced `VariantContext` to decouple component communication.
- **Z-Index Layering:** Architectural change to allow content to "slide over" the fixed hero background.

## 🧩 Maintenance & Future Work
- **Future:** Add more flavors by simply updating `variants.ts`.
- **Future:** Implement a backend CMS for dynamic text updates.
- **Maintenance:** Regularly update `npm` dependencies to patch security vulnerabilities.

## 🏆 Key Achievements
Successfully transformed a static concept into a scalable, interactive application. Maintained high visual fidelity while introducing strict engineering practices (Type safety, CI/CD readiness).

## 🧮 High-Level Architecture
The application follows a standard Next.js App Router topology. `page.tsx` serves as the composition root for the homepage, injecting the `ParallaxHero` and subsequent `sections`. Data flows unidirectionally from the `variants` configuration file into the state context, which then distributes it to subscribers.

## 🗂️ Folder Structure (Tree)
```
nextjs-parallax-web-experience/
├── src/
│   ├── app/
│   │   ├── globals.css         # Tailwind & Global Styles
│   │   ├── layout.tsx          # Root Layout & Providers
│   │   └── page.tsx            # Composition Root
│   ├── components/
│   │   ├── hero/               # Hero & Parallax Components
│   │   ├── layout/             # Header & Footer
│   │   ├── sections/           # Modular Page Sections
│   │   └── ui/                 # Reusable UI Primitives (ShadCN)
│   ├── contexts/               # React Context Definitions
│   ├── hooks/                  # Custom Business Logic Hooks
│   ├── lib/                    # Utilities & Constants
│   └── types/                  # TypeScript Interfaces
├── public/                     # Static Assets
└── package.json                # Project Manifest
```

## 🧭 How to Demonstrate Live
To showcase the project features in a live demo:
1. Open terminal in `nextjs-parallax-web-experience` directory.
2. Run `npm run dev`.
3. Open `http://localhost:3000`.
4. **Action 1:** Reload page to show Loading Screen.
5. **Action 2:** Scroll slowly to demonstrate Parallax and Layering.
6. **Action 3:** At the top, click "Next" to switch variants - point out the color and image change.
7. **Action 4:** Scroll down to "Our Story" - point out the matching product bottle.
8. **Action 5:** Open DevTools (F12), toggle Device Toolbar, set to "iPhone 12", and show responsive layout.

## 💡 Summary, Closure & Compliance
This report confirms that the Olipop Next.js Website project meets all specified technical requirements. The system is robust, performant, and ready for deployment. All code generated adheres to modern web standards and best practices.
