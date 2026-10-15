# ⚡ PulseHabit — Behavioral Analytics & Habit Tracking Dashboard

![React](https://img.shields.io/badge/React-18.x-61DAFB?style=flat-square&logo=react&logoColor=black)
![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.4-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)
![Accessibility](https://img.shields.io/badge/WCAG-AA_Compliant-10B981?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-F59E0B?style=flat-square)

**PulseHabit** is a high-craft, local-first habit-tracking and behavioral analytics web application. Built with a focus on tactile micro-interactions, schedule-aware streak algorithms, and zero-dependency audiovisual feedback, it transforms daily routine logging into an engaging, analytical experience.

---

## ✨ Key Features

### 1. Full Habit Lifecycle (CRUD) & Custom Scheduling
- **Granular Frequency Masks**: Configure habits for **Every Day**, **Weekdays Only (Mon–Fri)**, **Weekends (Sat–Sun)**, or **Custom Day Selection** (`[0..6]`).
- **Categorization & Theming**: Assign custom category tags (`Health`, `Deep Work`, `Mindfulness`, `Fitness`, `Learning`), icons, and 6 distinct semantic accent palettes (`Emerald`, `Indigo`, `Rose`, `Amber`, `Cyan`, `Violet`).
- **Daily Target Notes**: Attach micro-goals (e.g., `"45 mins • Zone 2"`, `"20 pages minimum"`) for clear completion criteria.

### 2. Schedule-Aware Streak Engine
Unlike naive streak counters that reset to zero when a user takes a planned rest day, PulseHabit implements a **Schedule-Aware Streak Algorithm**:
- **Rest-Day Bridging**: Unscheduled days are bypassed transparently without breaking an active streak.
- **Today Grace Period**: If today is scheduled but not yet completed, the active streak from yesterday remains preserved until the day ends.
- **4 Distinct Cell States**:
  - ✅ **Completed**: Logged for the target date.
  - ⭕ **Pending Scheduled**: Scheduled for today or a future date.
  - ❌ **Missed Scheduled**: A past scheduled day that was not logged (visualized with a subtle rose slash indicator).
  - ➖ **Rest / Unscheduled Day**: Dimmed dot indicator; can still be logged as bonus credit.

### 3. Tactile Micro-Interactions (Zero External Media Dependencies)
- **Web Audio API Synthesizer**: Real-time procedural sound effects generated directly in the browser without external MP3/WAV assets:
  - *Check Completion*: Crisp ascending major triad (`C5 → G5`).
  - *Uncheck / Undo*: Subtle low-pass downward pop.
  - *100% Daily Sweep Fanfare*: 4-note arpeggiated celebration chord (`C5 → E5 → G5 → C6`).
- **Localized 2D Canvas Particle Engine**: Clicking any habit checkbox spawns a physics-based confetti burst directly from the exact `(x, y)` viewport coordinates of the interaction.

### 4. Multi-View Analytical Workspace
- **Dashboard View (`Key: 1`)**:
  - **KPI Summary Cards**: Active Momentum (Current & Peak Streak), Today's Progress Ring, 7-Day Adherence Rate, and Total Completions.
  - **7-Day Rolling Matrix**: Interactive weekly grid with date-window pagination (`Prev Week`, `Next Week`, `Jump to Today`).
  - **Today's Action Focus**: Quick-toggle checklist sorted by scheduled priority vs. optional rest-day bonus habits.
  - **Rolling 7-Day Bar & Heat-Strip Chart**: Interactive SVG/CSS visualization showing daily completion percentages and scheduled load.
- **28-Day Analytics & Heatmap (`Key: 2`)**:
  - GitHub-style 28-day consistency matrix for every habit.
  - Category performance breakdown and individual adherence leaderboards.
- **System Specs & Architecture (`Key: 3`)**:
  - Live interactive documentation of component hierarchy, TypeScript state schema, and design tokens.

### 5. Local-First Persistence & Data Portability
- **Optimistic UI & `localStorage` Sync**: Instantaneous state updates persisted under versioned storage keys (`pulsehabit_v2_habits`).
- **JSON Backup & Restore**: Full export to timestamped `.json` files and validated schema import.
- **1-Click Demo Reset**: Quickly restore curated sample habits and 35 days of realistic historical data.

---

## 🏗️ Component Architecture

```text
App (Root Container & Global Keyboard Listener)
├── ConfettiCanvas (Fixed 2D HTML5 Canvas Particle Overlay)
├── TopNavigation
│   ├── BrandIdentity
│   ├── ViewSwitcher (Dashboard | 28-Day Heatmap | System Specs)
│   └── UtilityBar (New Habit CTA, Sound Toggle, Theme Toggle, JSON Export/Import)
├── KPISummaryGrid
│   ├── TodayProgressCard (Dynamic SVG Circular Progress Ring)
│   ├── MomentumStreakCard (Current vs. All-Time Best Streak)
│   ├── WeeklyAdherenceCard (7-Day Scheduled Completion Rate + Trend Delta)
│   └── VolumeCard (30-Day & All-Time Completion Counters)
├── DashboardWorkspace
│   ├── FilterToolbar (Search Input, Category Pills, New Habit Trigger)
│   ├── WeeklyHabitMatrix (7-Day Rolling Grid + Schedule-Aware Status Cells)
│   ├── TodayFocusPanel (Interactive Priority Action Checklist)
│   └── Rolling7DayChart (Interactive Bar Chart + Heat-Strip Matrix)
├── AnalyticsWorkspace
│   ├── ConsistencyHeatmap28D (28-Day Multi-Habit Completion Grid)
│   └── CategoryBreakdownPanel (Adherence Progress Bars by Tag)
├── SystemSpecsWorkspace (In-App Architecture & Token Explorer)
└── HabitFormModal (Accessible CRUD Dialog with Frequency Mask Picker)
