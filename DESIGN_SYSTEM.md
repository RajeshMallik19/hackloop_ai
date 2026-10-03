# HackLoop --- Design System

Version: 1.0\
Status: Product Design Direction\
Scope: HackLoop V1

------------------------------------------------------------------------

## 1. Purpose

This document defines the visual and interaction foundation for HackLoop
V1.

It is intended to guide:

-   Figma design
-   UI implementation
-   Component creation
-   Responsive behavior
-   AI interaction patterns
-   Accessibility
-   Visual consistency

This is a design direction, not a final pixel-perfect UI specification.

The final visual system should be refined in Figma after the first core
screens are explored.

------------------------------------------------------------------------

# 2. Design Philosophy

HackLoop should feel:

-   Technical
-   Energetic
-   Modern
-   Intelligent
-   Creative
-   Focused
-   Trustworthy

It should **not** feel like:

-   A generic AI chatbot
-   A corporate enterprise dashboard
-   A social media feed
-   A gaming platform
-   An overly futuristic "AI" cliché

The interface should communicate:

> **"You are building something real, and HackLoop is helping you
> move."**

------------------------------------------------------------------------

# 3. Core Design Principle

The visual system should prioritize:

**Progress over decoration.**

Every major screen should make it obvious:

1.  Where am I?
2.  What have I completed?
3.  What should I do next?

------------------------------------------------------------------------

# 4. Visual Personality

Recommended direction:

``` text
Modern startup
+
Developer tool
+
Creative workspace
```

Think:

-   Clean layouts
-   Strong typography
-   Clear cards
-   Subtle depth
-   Focused accent color
-   Generous spacing
-   Small moments of motion

Avoid excessive glassmorphism, gradients, glowing borders, or floating
3D objects simply for visual novelty.

------------------------------------------------------------------------

# 5. Color Strategy

The exact palette should be finalized in Figma.

Recommended structure:

### Primary

A distinctive energetic accent for:

-   Primary CTA
-   Active states
-   AI actions
-   Progress highlights

### Neutral

A strong neutral system for:

-   Background
-   Surface
-   Elevated surface
-   Border
-   Primary text
-   Secondary text
-   Muted text

### Semantic

Use dedicated semantic colors for:

-   Success
-   Warning
-   Error
-   Information

Semantic colors must not be confused with the HackLoop brand accent.

------------------------------------------------------------------------

# 6. Suggested Initial Palette Direction

Use this as a starting point, not a locked final palette.

``` text
Background
#F8FAFC

Surface
#FFFFFF

Primary Text
#0F172A

Secondary Text
#475569

Muted Text
#64748B

Border
#E2E8F0

Brand Accent
#6366F1

Success
#16A34A

Warning
#D97706

Error
#DC2626

Info
#2563EB
```

A dark theme can be explored later.

------------------------------------------------------------------------

# 7. Typography

Recommended primary typeface:

**Inter**

Alternative:

**Geist**

Typography should be highly readable and functional.

------------------------------------------------------------------------

## Type Scale

Suggested:

``` text
Display
48–64px

H1
36–48px

H2
28–36px

H3
22–28px

H4
18–20px

Body Large
18px

Body
16px

Body Small
14px

Caption
12px
```

Exact values should be normalized into Figma variables.

------------------------------------------------------------------------

# 8. Typography Rules

Use typography to establish hierarchy.

Avoid:

-   Too many font weights
-   Long all-caps headings
-   Tiny body text
-   Excessive text density

Recommended weight usage:

``` text
Regular
Medium
Semibold
Bold
```

------------------------------------------------------------------------

# 9. Spacing System

Use a consistent spacing scale.

Recommended base:

``` text
4
8
12
16
20
24
32
40
48
64
80
96
```

Most UI spacing should use these values rather than arbitrary numbers.

------------------------------------------------------------------------

# 10. Border Radius

Recommended:

``` text
Small
6px

Medium
10px

Large
14px

XL
20px

Pill
999px
```

Use radius intentionally.

Do not make every element extremely rounded.

------------------------------------------------------------------------

# 11. Shadows

Shadows should be subtle.

Recommended levels:

``` text
None
Small
Medium
Large
```

Most cards should rely on:

-   Border
-   Surface contrast
-   Spacing

rather than heavy shadows.

------------------------------------------------------------------------

# 12. Layout System

Use a responsive layout grid.

Desktop:

``` text
Max content width
~1200–1440px

Page padding
24–40px
```

Tablet:

``` text
Page padding
20–32px
```

Mobile:

``` text
Page padding
16–20px
```

Exact grid values should be finalized during Figma implementation.

------------------------------------------------------------------------

# 13. Responsive Breakpoints

Suggested:

``` text
Mobile
< 640px

Tablet
640–1023px

Desktop
1024–1439px

Large Desktop
≥ 1440px
```

These are starting points.

Components should adapt based on content, not only breakpoints.

------------------------------------------------------------------------

# 14. Navigation

## Desktop

Recommended:

``` text
Logo

Dashboard
Explore
Projects

----------------

Profile
Settings
```

Project-specific navigation can appear within the project workspace.

------------------------------------------------------------------------

## Mobile

Use:

``` text
Top Bar
+
Contextual navigation
+
Bottom navigation where appropriate
```

Avoid squeezing desktop navigation into mobile.

------------------------------------------------------------------------

# 15. Dashboard Design

The dashboard should prioritize action.

Recommended hierarchy:

``` text
Greeting
+
Next Best Action
+
Continue Project
+
Recommended Hackathons
+
Teams / Notifications
```

Avoid turning the dashboard into a metrics-heavy analytics page.

------------------------------------------------------------------------

# 16. Next Best Action Component

This should become a signature HackLoop component.

Example:

``` text
┌─────────────────────────────────────┐
│ Your next move                      │
│                                     │
│ Run a submission review             │
│                                     │
│ Your project has 3 unresolved       │
│ requirements.                       │
│                                     │
│ [ Review Project → ]                │
└─────────────────────────────────────┘
```

The component should feel useful, not promotional.

------------------------------------------------------------------------

# 17. Hackathon Cards

Hackathon cards should quickly communicate:

``` text
Organizer
Hackathon Name
Theme
Deadline
Prize
Format
Technology
```

Primary action:

**View Hackathon**

Secondary action:

**Save**

Avoid displaying too much metadata on the card.

------------------------------------------------------------------------

# 18. Hackathon Details Page

Recommended structure:

``` text
Hero
 ↓
Key Information
 ↓
Overview
 ↓
Tracks
 ↓
Rules
 ↓
Timeline
 ↓
Prizes
 ↓
Submission Requirements
```

Desktop can use a sticky action panel:

``` text
┌─────────────────────┐
│ Deadline            │
│ Prize               │
│ Eligibility         │
│                     │
│ [ Start Project ]   │
└─────────────────────┘
```

------------------------------------------------------------------------

# 19. Project Workspace

This is one of the most important screens.

Recommended structure:

``` text
Project Header
    ↓
Project Status
    ↓
Main Content
    │
    ├── Overview
    ├── Tasks
    ├── Team
    ├── Research
    └── Submission
```

Persistent AI access should be available without overwhelming the
workspace.

------------------------------------------------------------------------

# 20. Project Header

Should show:

``` text
Project Name
Hackathon
Project State
Progress
```

Example:

``` text
EcoVision
AI for Agriculture Hackathon

Building · 64%

[ AI Assistant ] [ Review Submission ]
```

------------------------------------------------------------------------

# 21. Project Navigation

Suggested:

``` text
Overview
Problem
Solution
Features
Tasks
Team
Research
Files
Links
Submission
```

On mobile, this should become a compact contextual navigation pattern.

------------------------------------------------------------------------

# 22. Project Progress

Progress should not dominate the UI.

Recommended:

``` text
64%
████████████░░░░
```

Accompanied by meaningful context:

> 8 of 12 MVP tasks completed.

Avoid meaningless "87% project complete" values.

------------------------------------------------------------------------

# 23. AI Interaction Design

AI should feel like a product capability rather than a separate chatbot
website.

Preferred patterns:

### Inline AI

Useful for individual fields.

Example:

> Improve this problem statement

### Side Panel

Useful for contextual assistance.

Example:

> Ask Project Assistant

### Structured Generation

Useful when creating project content.

Example:

``` text
AI Suggested

Problem
[ generated content ]

[ Accept ] [ Edit ] [ Regenerate ]
```

------------------------------------------------------------------------

# 24. AI Panel

The AI panel should show context.

Example:

``` text
PROJECT ASSISTANT

EcoVision
AI Agriculture Hackathon

Ask about your project...

--------------------------------

Suggested:
• Create MVP tasks
• Review project scope
• Identify blockers
```

This is better than a blank chatbot interface.

------------------------------------------------------------------------

# 25. AI Response States

AI interactions need clear states.

``` text
Idle
↓
Thinking
↓
Generating
↓
Generated
↓
User Review
↓
Accepted / Edited / Rejected
```

Do not show a generic infinite spinner.

------------------------------------------------------------------------

# 26. AI Generated Content

AI-generated content should be visually distinguishable.

Possible pattern:

``` text
✨ AI Suggested

Content...

[ Accept ]
[ Edit ]
[ Regenerate ]
```

Once accepted and edited, the content should visually behave like normal
project content.

------------------------------------------------------------------------

# 27. AI Confidence / Evidence

Avoid fake confidence percentages.

Instead use contextual indicators:

``` text
Based on hackathon requirements
```

or:

``` text
AI recommendation
```

or:

``` text
Verified hackathon requirement
```

------------------------------------------------------------------------

# 28. Team Matching UI

The team matcher should emphasize **why** someone is recommended.

Example:

``` text
┌──────────────────────────────────────┐
│ Arun Kumar                           │
│ Backend + Python                     │
│                                      │
│ ✓ Python                             │
│ ✓ FastAPI                            │
│ ✓ PostgreSQL                         │
│                                      │
│ Matches 3 project skill gaps         │
│ Available weekends                   │
│                                      │
│ [ View Profile ] [ Invite ]          │
└──────────────────────────────────────┘
```

Avoid reducing people to a single score.

------------------------------------------------------------------------

# 29. Team Skill Gap Visualization

Example:

``` text
Project Skills

Python            ██████████ Covered
Computer Vision   ████░░░░░░ Missing
Backend           ██████░░░░ Partial
UI/UX             ██████████ Covered
```

The exact visualization can be simplified for mobile.

------------------------------------------------------------------------

# 30. Task Board

Recommended V1 task structure:

``` text
TODO
────────────────
Build login
Design dashboard

IN PROGRESS
────────────────
Prediction API

BLOCKED
────────────────
Model deployment

DONE
────────────────
Project setup
```

Mobile should use a list or segmented view instead of forcing a wide
Kanban board.

------------------------------------------------------------------------

# 31. Submission Review UI

The review should be highly actionable.

Example:

``` text
Submission Review

2 requirements need attention.

────────────────────────

AI Requirement

PARTIALLY ADDRESSED

Evidence:
AI model is used for disease detection.

Gap:
The submission doesn't explain why AI is necessary.

Recommendation:
Add a short explanation...

[ Fix in Project ]
```

The user should be able to jump directly from a review finding to the
relevant project field.

------------------------------------------------------------------------

# 32. Submission Readiness

Use a checklist rather than a giant score.

Example:

``` text
Submission Readiness

✓ Problem
✓ Solution
✓ Demo
✓ Repository
⚠ AI requirement
⚠ Documentation
✓ Team information
```

Primary CTA:

**Resolve 2 issues**

------------------------------------------------------------------------

# 33. Forms

Forms should:

-   Use clear labels
-   Show validation near the field
-   Preserve user input on errors
-   Avoid unnecessary steps
-   Use progressive disclosure

AI-assisted fields can provide optional suggestions.

------------------------------------------------------------------------

# 34. Buttons

Primary button:

Used for the main action.

Examples:

-   Start Project
-   Create Project
-   Review Submission

Secondary:

-   Save
-   Edit
-   View Profile

Tertiary:

-   Cancel
-   Learn More
-   Back

Destructive:

-   Delete
-   Remove Member

Do not style every button as a primary CTA.

------------------------------------------------------------------------

# 35. Inputs

Inputs should include:

``` text
Label
Input
Helper text where needed
Validation
Error state
```

Avoid placeholder text as the only label.

------------------------------------------------------------------------

# 36. Cards

Cards should represent meaningful objects:

-   Hackathon
-   Project
-   Team member
-   Task
-   AI recommendation
-   Review finding

Avoid putting every section inside a card.

Use open layouts when content is naturally connected.

------------------------------------------------------------------------

# 37. Status System

Standardize status badges.

Examples:

``` text
Draft
Building
Reviewing
Ready
Submitted
Blocked
```

Status should communicate state, not decoration.

------------------------------------------------------------------------

# 38. Toasts

Use toasts for lightweight confirmations:

``` text
Project saved
Invitation sent
Task created
Review completed
```

Do not use toasts for critical information that users may miss.

------------------------------------------------------------------------

# 39. Modals

Use modals sparingly.

Good uses:

-   Confirm destructive action
-   Invite teammate
-   Quick create
-   Important confirmation

Avoid putting large workflows inside modals.

------------------------------------------------------------------------

# 40. Empty States

Every major feature should have a useful empty state.

Example:

``` text
No teammates yet.

Your project is missing:
Backend
AI/ML

[ Find Teammates ]
```

The empty state should lead directly to the next action.

------------------------------------------------------------------------

# 41. Loading States

Use skeletons for content-heavy loading.

Examples:

-   Hackathon cards
-   Project overview
-   Team lists

Use progress/streaming states for AI.

------------------------------------------------------------------------

# 42. Error States

Errors should answer:

1.  What happened?
2.  Is my data safe?
3.  What can I do next?

Example:

> We couldn't load your project. Your saved data is safe.

**Try again**

------------------------------------------------------------------------

# 43. Accessibility

Target:

**WCAG 2.1 AA**

Core requirements:

-   Keyboard navigation
-   Visible focus states
-   Semantic HTML
-   Accessible labels
-   Sufficient color contrast
-   Screen-reader support
-   Reduced motion support
-   Error messages that are understandable without color alone

------------------------------------------------------------------------

# 44. Motion

Motion should communicate:

-   State changes
-   Navigation
-   Progress
-   AI generation
-   Success

Avoid decorative motion everywhere.

Recommended:

``` text
Fast
100–200ms

Standard
200–300ms

Complex
300–500ms
```

Respect:

``` text
prefers-reduced-motion
```

------------------------------------------------------------------------

# 45. Microinteractions

Potential signature interactions:

### Project creation

Subtle transition from:

``` text
Idea
→
Project
```

### AI generation

Progressive reveal of structured sections.

### Task completion

Small completion transition.

### Submission review

Findings appear progressively.

These should remain subtle.

------------------------------------------------------------------------

# 46. Responsive Philosophy

Do not design desktop first and simply shrink it.

Each major screen should have intentional layouts for:

``` text
Desktop
Tablet
Mobile
```

------------------------------------------------------------------------

# 47. Mobile Dashboard

Recommended order:

``` text
Header
↓
Next Best Action
↓
Continue Project
↓
Hackathons
↓
Teams
```

Avoid large desktop-style analytics grids.

------------------------------------------------------------------------

# 48. Mobile Project Workspace

Use:

``` text
Project Header
↓
Status
↓
Next Action
↓
Content
↓
Sticky AI Action
```

The full desktop sidebar becomes a compact navigation control.

------------------------------------------------------------------------

# 49. Tablet Design

Tablet should not be treated as oversized mobile.

Use:

-   Two-column layouts where useful
-   Collapsible navigation
-   Wider cards
-   Adaptive project workspace

------------------------------------------------------------------------

# 50. Design Tokens

Figma should eventually define variables for:

``` text
Colors
Typography
Spacing
Radius
Shadows
Motion
Breakpoints
```

The implementation should consume equivalent tokens.

------------------------------------------------------------------------

# 51. Component Library

Core components:

``` text
Button
Input
Textarea
Select
Checkbox
Badge
Avatar
Card
Modal
Drawer
Tabs
Dropdown
Tooltip
Toast
Skeleton
Progress
Breadcrumb
Command Menu
```

HackLoop-specific:

``` text
HackathonCard
ProjectCard
NextActionCard
ProjectHeader
ProjectProgress
SkillChip
SkillGap
TeamMemberCard
TaskCard
TaskBoard
AIInput
AIPanel
AIGenerationCard
ReviewFinding
SubmissionChecklist
```

------------------------------------------------------------------------

# 52. Design System Hierarchy

Figma should organize components approximately as:

``` text
Foundations
    ↓
Primitives
    ↓
Components
    ↓
Patterns
    ↓
Screens
```

Avoid creating every screen as a collection of disconnected components.

------------------------------------------------------------------------

# 53. Design-to-Code Principle

Every reusable visual pattern should have a corresponding reusable
implementation component where practical.

Example:

``` text
Figma:
NextActionCard

Code:
<NextActionCard />
```

This keeps the design and implementation systems aligned.

------------------------------------------------------------------------

# 54. Figma File Structure

Recommended:

``` text
HackLoop
│
├── Cover
├── Foundations
├── Components
├── Patterns
├── User Flows
├── Desktop
├── Tablet
├── Mobile
└── Prototype
```

------------------------------------------------------------------------

# 55. Initial Screens to Design

Do not design every possible screen immediately.

Start with the critical path:

``` text
1. Landing
2. Sign Up
3. Profile Setup
4. Dashboard
5. Explore Hackathons
6. Hackathon Details
7. Create Project
8. AI Copilot
9. Project Workspace
10. Team Matching
11. Task Workspace
12. Submission Review
13. Submission Readiness
```

------------------------------------------------------------------------

# 56. Figma Prototype Flow

The first interactive prototype should demonstrate:

``` text
Landing
 ↓
Dashboard
 ↓
Explore
 ↓
Hackathon
 ↓
Start Project
 ↓
Copilot
 ↓
Project
 ↓
Team
 ↓
Workspace
 ↓
Review
 ↓
Submission Ready
```

This is more valuable than designing dozens of isolated screens.

------------------------------------------------------------------------

# 57. Visual QA Checklist

Every screen should be checked for:

-   Alignment
-   Typography
-   Spacing
-   Contrast
-   Component consistency
-   Responsive behavior
-   Empty states
-   Loading states
-   Error states
-   Keyboard focus
-   AI interaction clarity

------------------------------------------------------------------------

# 58. Design Anti-Patterns

Avoid:

-   Excessive gradients
-   Neon AI aesthetics
-   Huge dashboard metric walls
-   Too many floating cards
-   Excessive rounded containers
-   Decorative 3D elements with no purpose
-   Generic chatbot layouts
-   Tiny text
-   Overloaded sidebars
-   Hidden primary actions
-   AI-generated content that looks indistinguishable from verified
    facts

------------------------------------------------------------------------

# 59. Signature HackLoop Elements

HackLoop should develop a recognizable visual language around:

### 1. Next Best Action

The product tells users what to do next.

### 2. Project Progress

Progress is connected to real work.

### 3. Contextual AI

AI appears where it is useful.

### 4. Evidence-based Review

Submission review shows concrete gaps rather than arbitrary scores.

### 5. Skill Gap Visualization

Teams understand what is missing.

These can become the visual identity of the product.

------------------------------------------------------------------------

# 60. Design Validation

Before implementation, test the prototype with a small group of
potential hackathon participants.

Ask:

-   Can they find a hackathon?
-   Do they understand the project flow?
-   Do they understand what the AI is doing?
-   Can they find teammates?
-   Can they understand project progress?
-   Can they identify what to do next?
-   Can they understand submission readiness?

Do not optimize solely for visual aesthetics.

------------------------------------------------------------------------

# 61. Design-to-Engineering Handoff

Figma handoff should provide:

-   Component names
-   Variables
-   Spacing
-   Typography
-   Responsive behavior
-   Interaction states
-   Empty states
-   Loading states
-   Error states
-   Accessibility notes

The goal is to make implementation predictable.

------------------------------------------------------------------------

# 62. Final Design Principle

HackLoop should look like a product built for people who are **actively
making things**.

The interface should continuously communicate:

``` text
Here is your project.
Here is where you are.
Here is what is missing.
Here is what you can do next.
Here is how AI can help.
```

The visual system should support that loop without becoming the product
itself.
