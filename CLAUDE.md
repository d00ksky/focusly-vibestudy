# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**VibeStudy** is a React Native (Expo) mobile app that combines pomodoro timer functionality with a virtual pet otter that collects stones. Users earn stones by completing study sessions and enjoy curated memes during breaks.

**Tagline:** "Study hard, vibe harder"

## Current Status

This is a **greenfield project** in early development phase. The repository currently contains only documentation files with no code implementation yet.

## Tech Stack (Decided)

- **Frontend**: React Native + Expo SDK 50
- **State Management**: Zustand
- **Navigation**: Expo Router (file-based)
- **Animations**: React Native Reanimated + Rive
- **Local Storage**: AsyncStorage + Expo SecureStore
- **Platform**: iOS first, Android later
- **Backend** (Future): Firebase (Firestore, Cloud Storage, Auth)

## Development Commands

```bash
# Once project is initialized:
npx create-expo-app vibestudy --template blank-typescript
cd vibestudy
npm install zustand react-native-reanimated expo-router @react-native-async-storage/async-storage
npm start
```

## Project Structure

```
vibestudy/
├── app/                    # Expo Router screens
│   ├── (tabs)/            
│   │   ├── timer.tsx      # Main timer screen with otter
│   │   ├── collection.tsx # Stone collection display
│   │   └── stats.tsx      # Study statistics
│   ├── _layout.tsx        # Root layout with providers
│   └── onboarding.tsx     # First-time user flow
├── components/
│   ├── Otter/
│   │   ├── OtterSprite.tsx    # Main otter component
│   │   ├── OtterAnimations.ts # Animation definitions
│   │   └── OtterEmotions.ts   # Emotion state machine
│   ├── Timer/
│   │   ├── TimerDisplay.tsx   # Circular progress timer
│   │   ├── TimerControls.tsx  # Start/pause/skip buttons
│   │   └── SessionConfig.tsx  # 25/5 or 50/10 selector
│   ├── Stones/
│   │   ├── StoneItem.tsx      # Individual stone component
│   │   ├── StoneCollection.tsx # Grid display of stones
│   │   └── StoneAnimation.tsx  # Collection animation
│   └── Memes/
│       ├── MemeDisplay.tsx     # Break-time meme viewer
│       └── MemeLoader.tsx      # Caching and loading logic
├── lib/
│   ├── store/
│   │   ├── useTimerStore.ts   # Timer state (Zustand)
│   │   ├── useOtterStore.ts   # Otter state & stones
│   │   └── useUserStore.ts    # User prefs & stats
│   ├── utils/
│   │   ├── storage.ts         # AsyncStorage helpers
│   │   ├── sounds.ts          # Sound effect player
│   │   └── notifications.ts   # Study reminders
│   └── constants/
│       ├── colors.ts          # River Morning palette
│       ├── stones.ts          # Stone types & rarities
│       └── animations.ts      # Animation configs
└── assets/
    ├── rive/              # Otter animation files
    ├── sounds/            # Click, success, stone collect
    ├── images/
    │   ├── stones/        # Stone PNG assets
    │   └── backgrounds/   # Study environment art
    └── memes/            # Local meme cache
```

## Core Features

### Virtual Pet: Otto the Otter
- Collects stones for each completed study session
- Different animations: idle, studying, celebrating, sleeping
- Holds comfort stone during study sessions
- Shows excitement when presenting new stones

### Stone Collection System
**Regular Stones** (from normal sessions):
- River stones (gray, brown shades)
- Smooth pebbles (various earth tones)
- Sea glass (soft blues, greens)

**Special Stones** (from achievements/streaks):
- 🧊 **Freeze Stone**: Protects your streak if you miss a day
- ⏰ **Time Stone**: Grants extra break time (+2 min)
- 🔥 **Fire Stone**: Study streak milestone rewards
- 🌟 **Star Stone**: Perfect day completion
- 🍀 **Lucky Stone**: Random rare drop

### Timer Modes
- 25/5 (25 min focus, 5 min break)
- 50/10 (50 min focus, 10 min break)
- Long break every 4 sessions (15 min)

### Streak System
- Daily study goal (customizable: 1-5 sessions)
- Visual streak counter with fire animation
- Streak freeze stones for emergencies
- Milestone rewards at 7, 30, 50, 100 days

## Visual Design System

### Colors (River Morning Palette)
```typescript
export const colors = {
  primary: '#5DADE2',    // Soft teal
  secondary: '#F4E5D3',  // Warm sand  
  accent: '#7F8C8D',     // River stone gray
  highlight: '#F39C12',  // Golden hour
  background: '#FAFAFA', // Morning mist
  text: '#2C3E50',      // Dark blue-gray
  success: '#27AE60',   // Forest green
  danger: '#E74C3C'     // Soft red
}
```

### Design Principles
- **Cute but not childish** - Think Studio Ghibli, not Fisher-Price
- **Minimal distractions** - Clean UI during focus time
- **Delightful interactions** - Smooth animations, satisfying feedback
- **One-handed operation** - Everything reachable with thumb

## MVP Checklist (3 Month Target)

- [ ] Basic timer (25/5, 50/10)
- [ ] Otto with 5 core animations
- [ ] 10 stone types (5 common, 5 special)
- [ ] Streak counter with freeze stones
- [ ] 50 local memes
- [ ] Sound effects
- [ ] Onboarding flow
- [ ] Local data persistence

## Development Guidelines

### State Management
- Use Zustand stores for global state
- React state for component-specific UI
- Persist critical data to AsyncStorage

### Performance
- Lazy load heavy components
- Cache meme images aggressively  
- Optimize otter animations for 60fps
- Use React.memo for stone grid items

### Error Handling
- Graceful offline mode
- Fallback for failed meme loads
- Recovery for corrupted local data
- Never lose user's stone collection!

### Testing Priorities
1. Timer accuracy across backgrounds
2. Stone collection persistence
3. Streak calculation edge cases
4. Meme caching and cleanup
5. Otter animation performance

## Pre-Launch Development

### Landing Page Project
Before the main app launch, create a marketing landing page with mini-game:
- **URL**: vibestudy.app
- **Tech**: Next.js/Astro + Phaser.js
- **Database**: Supabase for email/code storage
- **Purpose**: Build hype, collect emails, distribute reward codes

### Reward Code Integration
The main app needs to support:
- Deep linking: `vibestudy://redeem/{CODE}`
- Code validation against Supabase
- Special rewards for pre-launch players:
  - Founder's Stone
  - Golden Otto skin
  - Freeze stone starter pack
  - Day One achievement badge

## Next Steps

### Phase 1: Landing Page (Month 1)
1. Set up landing page with Next.js/Astro
2. Implement mini-game (Stone Memory or Otto's River Rush)
3. Email collection system with Supabase
4. Reward code generation

### Phase 2: Mobile App MVP (Months 2-3)
1. Initialize Expo project with TypeScript
2. Set up project structure and navigation
3. Implement basic timer functionality
4. Create Otto sprite and basic animations
5. Design stone assets (10 basic types)
6. Build stone collection mechanic
7. Add local storage persistence
8. Implement reward code redemption

### Phase 3: Polish & Launch (Month 4)
1. Beta testing with pre-launch community
2. Bug fixes and performance optimization
3. App store submission
4. Launch day coordination with email list

Remember: The otter is the heart of the app. Every interaction should feel alive and delightful! 🦦