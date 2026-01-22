# Product Requirements Document: Meditation Mobile App

## Product Overview

**Product Name:** Meditation Mobile App (TBD)

**Product Vision:** A local-first, gesture-driven mobile meditation application that provides quick access to customizable meditation sessions with intelligent timing and minimal distractions.

**Problem Statement:** Experienced meditation practitioners need a simple, distraction-free tool to practice meditation on their own terms, with full control over their content, without dependency on external services, subscriptions, or predefined programs.

**Solution:** A mobile application that enables users to create and manage custom meditation sessions locally on their device, with an intuitive gesture-based interface for instant access and duration control, supporting self-directed practice with personalized content.

---

## Target Audience

**Primary Users:** Self-directed meditation practitioners who:
- Already know meditation fundamentals and techniques
- Want full control over their meditation content and structure
- Prefer privacy and local data storage over cloud-based services
- Value simplicity and quick access over guided programs
- Are comfortable defining their own meditation framework

**User Pain Points:**
- Existing apps require subscriptions or constant internet connectivity
- Guided meditation apps impose specific techniques or teaching styles
- Too many features create friction between intention and practice
- Data privacy concerns with cloud-based meditation tracking
- Lack of customization for personal meditation frameworks

**Usage Context:**
- Daily meditation practice at home, office, or during travel
- Quick meditation breaks between activities
- Structured personal practice without external guidance
- Offline environments where connectivity isn't available

---

## Success Metrics

The following quantifiable outcomes will indicate product success:

1. **Daily Active Users (DAU):** Track how many users open and use the app daily
2. **Meditation Completion Rate:** Percentage of started meditations that run to full timer completion
3. **Session Frequency:** Average number of completed meditation sessions per user per week
4. **Custom Content Creation:** Average number of custom-defined sessions per user
5. **Custom Content Utilization:** Frequency of use for user-created sessions vs. starter templates

---

## Main User Flow

### Primary Flow: Quick Start Meditation

1. **Open Application**
   - User launches the app to home screen
   - Displays central "Go" button with current duration setting
   - Shows preset duration buttons for quick selection

2. **Adjust Duration (Optional)**
   - User rotates around the Go button to adjust meditation duration
   - OR taps preset duration buttons (5m, 10m, 15m, 20m, etc.)
   - Duration value updates in real-time

3. **Select Session (Optional)**
   - User long-presses the Go button
   - Session selector appears showing available templates
   - User selects specific session or keeps random selection

4. **Start Meditation**
   - User taps Go button
   - App randomly selects a session from user's template library
   - Session begins with entry quote display

5. **Active Meditation Session**
   - Entry quote displays
   - Wisdom text appears
   - Focus points display at pre-timed intervals (scaled proportionally to selected duration)
   - Timer counts down
   - Screen stays on throughout session
   - Minimal UI with pause/resume/stop controls available

6. **Complete or Stop Session**
   - Session ends when timer reaches zero (completion)
   - OR user manually stops the session early
   - Return to home screen

### Interruption Handling

- **Phone Call / Notification / App Backgrounding:**
  - Session automatically pauses
  - Timer stops
  - User can resume when ready, continuing from where they left off

---

## Must-Have Capabilities (v1.0)

### 1. Session Template Management

**Description:** Create, edit, delete, and organize custom meditation session templates stored locally on device.

**Inputs:**
- Session template name
- Entry quote (text)
- Wisdom text
- List of focus points with individual display durations
- Total intended session duration (sum of focus point durations)

**Outputs:**
- Stored session templates in local database
- Available templates for meditation playback
- Exportable session data files

**Behavior:**
- Full CRUD operations on session templates
- All data stored locally on device without external services
- No limit on number of templates
- Templates include metadata (creation date, last modified, usage count)
- Validation: prevent empty focus point lists, require at least entry quote or wisdom

**Dependencies:** None

---

### 2. Gesture-Based Quick Start Interface

**Description:** Intuitive gesture controls and preset buttons for instant meditation access and duration control.

**Inputs:**
- Tap gesture on Go button (start meditation)
- Rotation gesture around Go button (duration adjustment)
- Long-press gesture on Go button (session template selector)
- Tap on preset duration buttons (quick duration selection)

**Outputs:**
- Meditation session launch
- Duration value (in minutes/seconds)
- Selected session template

**Behavior:**
- Central Go button is primary interaction point
- Rotation gesture continuously adjusts duration (e.g., 1-60 minutes)
- Preset duration buttons (5m, 10m, 15m, 20m, 30m) provide accessible alternative to rotation
- Long-press reveals session template picker modal
- Default behavior: tap Go button starts random session at current duration
- Visual feedback for all gestures (rotation shows duration, long-press shows haptic feedback)

**Dependencies:** Session Template Management (requires templates to select from)

---

### 3. Session Playback Engine

**Description:** Execute meditation sessions with proportionally-scaled timing, minimal UI, and intelligent interruption handling.

**Inputs:**
- Selected duration (from gesture interface)
- Chosen session template with pre-timed focus points
- User controls (pause, resume, stop)

**Outputs:**
- Visual display of entry quote, wisdom, and focus points
- Countdown timer display
- Session completion event

**Behavior:**
- **Timing Calculation:** Scale all focus point durations proportionally to match user-selected duration
  - Formula: `scaled_duration = (focus_point_duration / total_template_duration) × selected_duration`
  - Example: Template with 3 focus points (30s, 60s, 30s = 120s total), user selects 10 minutes → points display for 2.5m, 5m, 2.5m
- **Display Sequence:**
  1. Entry quote (10% of session duration or 30s, whichever is less)
  2. Wisdom text (10% of session duration or 30s, whichever is less)
  3. Focus points in sequence with scaled durations
- **UI During Session:**
  - Minimal, distraction-free interface
  - Current focus point text centered
  - Countdown timer (discrete, non-intrusive)
  - Pause/Resume/Stop buttons (accessible but unobtrusive)
- **Screen Behavior:** Screen stays on throughout meditation session (prevent device sleep)
- **Interruption Handling:** Auto-pause on phone calls, notifications, or app backgrounding; user can resume
- **Completion Criteria:** Session is "completed" only when timer reaches zero; manual stops are not completions

**Dependencies:** Session Template Management, Random Session Selector

---

### 4. Random Session Selector

**Description:** Randomly select one session template from user's library for playback.

**Inputs:**
- User's collection of session templates
- Exclusion rules (optional: don't repeat last N sessions)

**Outputs:**
- Single randomly selected session template

**Behavior:**
- Uniform random selection from all available templates
- If library is empty, fallback to starter templates
- Selection happens on Go button tap (before playback begins)
- No bias toward newer or more frequently used sessions

**Dependencies:** Session Template Management

---

### 5. Starter Templates

**Description:** Pre-built example meditation sessions to demonstrate app functionality and provide immediate usability for new users.

**Inputs:** None (built into app)

**Outputs:**
- 2-3 pre-configured session templates available on first launch
- Templates restored if user deletes all custom sessions

**Behavior:**
- Included starter templates cover common meditation styles:
  1. **Breath Awareness** (10 minutes): Focus on breath sensations
  2. **Body Scan** (15 minutes): Progressive body awareness
  3. **Loving-Kindness** (12 minutes): Compassion practice
- Starter templates can be edited or deleted by users
- If user deletes all templates (including starters), app automatically restores starter templates
- Starter templates are visually distinguishable from user-created templates

**Dependencies:** None

---

### 6. Session Import/Export

**Description:** Allow users to backup and restore their session template library via file export/import.

**Inputs:**
- User action to export templates
- Import file selection (JSON format)

**Outputs:**
- JSON file containing all session templates
- Imported session templates added to library

**Behavior:**
- **Export:** Generate JSON file with all user templates, save to device storage or share
- **Import:** Parse JSON file, validate structure, add templates to library (merge, don't overwrite)
- File format: Structured JSON with version metadata for future compatibility
- Export includes all template metadata (name, quotes, wisdom, focus points, durations, creation date)
- Import validates data integrity before adding to library

**Dependencies:** Session Template Management

---

## Good-to-Have Capabilities (Future Versions)

### 7. Session History Tracking

**Description:** Record completed meditation sessions and generate practice statistics.

**Inputs:**
- Completed session data (which template, actual duration, completion timestamp)

**Outputs:**
- Historical log of completed sessions
- Statistics: total sessions, total time meditated, current streak, weekly frequency

**Behavior:**
- Log only sessions that reach timer completion (manual stops don't count)
- Calculate engagement metrics: consecutive days practiced, average session length
- Provide weekly/monthly views of meditation activity
- All data stored locally

**Dependencies:** Session Playback Engine

---

### 8. Background Audio

**Description:** Play ambient sounds or music during meditation sessions.

**Inputs:**
- User-selected audio files (imported to app)
- Volume settings
- Audio-to-session association (which sounds for which sessions)

**Outputs:**
- Audio playback synchronized with meditation session

**Behavior:**
- Play selected audio in background throughout session
- Audio continues through focus point transitions
- Fade in at session start, fade out at completion
- Support for looping short audio clips

**Dependencies:** Session Playback Engine

---

### 9. Meditation Reminders

**Description:** Schedule local notifications to encourage regular meditation practice.

**Inputs:**
- Reminder schedule preferences (daily, specific times, days of week)
- Notification text customization

**Outputs:**
- Push notifications at configured times

**Behavior:**
- Trigger local notifications based on user-defined schedule
- Smart scheduling: don't remind if user already meditated today
- Respectful notification text (encouraging, not guilt-inducing)

**Dependencies:** None (independent feature)

---

## Technical Considerations

### Platform
- **Target Platform:** iOS and/or Android mobile
- **Minimum OS Version:** TBD based on development framework

### Data Storage
- **Local Database:** SQLite, Core Data (iOS), or Room (Android)
- **Session Templates:** Structured storage with relational data
- **File Format:** JSON for import/export
- **Privacy:** All data stored locally, no telemetry or external servers

### Screen Management
- **Wake Lock:** Prevent device sleep during active meditation
- **Battery Consideration:** Warn users about battery drain for long sessions with screen-on

### Interruptions
- **Background Mode:** Handle app backgrounding gracefully with auto-pause
- **Phone Calls:** Detect incoming calls and auto-pause session
- **Notifications:** Suppress all notifications during active meditation (Do Not Disturb mode)

### Accessibility
- **Gesture Alternatives:** Preset duration buttons for users who can't use rotation gesture
- **Text Size:** Respect system text size settings for focus point display
- **VoiceOver/TalkBack:** Future consideration for screen reader support

---

## Why This Product?

### Why We Need This Product

1. **Privacy-First Approach:** Existing meditation apps collect user data, require accounts, and sync to cloud servers. Users concerned about privacy and data ownership need a local-first alternative.

2. **Self-Directed Practice:** Popular meditation apps (Headspace, Calm, Insight Timer) are built for guided meditation or structured programs. Experienced practitioners need a tool that supports their own meditation framework without imposing external structure.

3. **No Subscription Fatigue:** The meditation app market is dominated by subscription models. Users want a one-time purchase tool they own outright.

4. **Offline Capability:** Travelers, remote practitioners, and users in low-connectivity environments need reliable offline access.

5. **Customization Freedom:** Existing apps limit customization to preset themes, durations, or sounds. This app empowers users to define their entire meditation structure.

### Why Can't We Use Existing Products?

- **Headspace/Calm:** Focused on guided meditation and courses, not customizable content
- **Insight Timer:** Community-focused with thousands of guided sessions, but limited support for self-created structured sessions
- **Simple Meditation Timers:** Lack content management, only provide timer functionality
- **Generic Timers:** Don't support meditation-specific features like focus point sequences
- **Note-Taking Apps:** Could store meditation content but lack playback, timing, and session management

No existing product combines:
- Local-only storage with full privacy
- Gesture-based quick start interface
- Customizable meditation session templates with timed focus points
- Proportional timing scaling
- Random session selection for variety

---

## Out of Scope (v1.0)

The following are explicitly NOT included in the first version:

- Cloud sync or backup
- Social features (sharing sessions, community, friends)
- Audio recording or playback of voice guidance
- Video content
- Integration with health tracking platforms (Apple Health, Google Fit)
- Wearable device support (Apple Watch, Wear OS)
- Multi-language support (English only for v1.0)
- Guided meditation voice recordings
- Background sounds or music (moved to good-to-have)
- Session history and statistics (moved to good-to-have)
- Meditation streaks or gamification

---

## Open Questions & Considerations

1. **Monetization Strategy:** Free with optional one-time purchase? Freemium with limited templates? Fully paid upfront?

2. **Template Sharing:** While cloud sync is out of scope, should users be able to share session templates via file export with other users?

3. **Focus Point Complexity:** Should focus points support rich text formatting, or plain text only?

4. **Maximum Duration:** Should there be a maximum meditation duration (e.g., 120 minutes) to prevent battery drain issues?

5. **Session Naming:** How should random sessions be identified to users after completion? Show template name during or after session?

6. **Haptic Feedback:** Should focus point transitions include subtle haptic feedback on supported devices?

7. **Dark Mode:** Should the app support system dark mode, or force a specific color scheme for meditation?

8. **Timer Display Toggle:** Should users be able to hide the timer during meditation for deeper immersion?

---

## Dependencies & Development Order

### Phase 1: Foundation
1. Session Template Management (no dependencies)
2. Starter Templates (no dependencies)

### Phase 2: Core Experience
3. Gesture-Based Quick Start Interface (depends on #1)
4. Random Session Selector (depends on #1)
5. Session Playback Engine (depends on #1, #3, #4)

### Phase 3: Data Portability
6. Session Import/Export (depends on #1)

### Future Phases
7. Session History Tracking (depends on #5)
8. Background Audio (depends on #5)
9. Meditation Reminders (independent)

---

## Revision History

- **v1.0 (2026-01-20):** Initial PRD creation
