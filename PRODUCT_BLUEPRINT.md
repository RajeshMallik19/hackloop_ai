# HackLoop --- Product Blueprint v1

**Status:** Draft for product validation\
**Version:** 1.0\
**Product:** HackLoop\
**Category:** AI-native hackathon platform\
**Primary audience:** College students and early-career developers who
participate in hackathons

------------------------------------------------------------------------

## 1. Product Vision

HackLoop helps people move from **finding a hackathon** to **building
and submitting a strong project**.

The core loop is:

**Discover → Ideate → Form Team → Build → Validate → Submit**

AI is not a separate chatbot feature. AI is embedded throughout the
workflow and uses the user's profile, selected hackathon, project
context, team information, tasks, and submission requirements.

### Product promise

> **HackLoop helps hackathon participants turn opportunities and ideas
> into viable projects, teams, and submission-ready work --- with AI
> assistance throughout the process.**

------------------------------------------------------------------------

## 2. The Problem

Hackathon participants commonly face several disconnected problems:

1.  They discover hackathons through fragmented sources.
2.  They struggle to decide which hackathon is actually relevant to
    their skills and interests.
3.  They have ideas but struggle to turn them into a focused, buildable
    MVP.
4.  They need teammates with complementary skills.
5.  They lose time organizing tasks and project information.
6.  They are unsure whether their final submission addresses the judging
    criteria.
7.  They often start building before understanding scope, feasibility,
    and differentiation.

Existing tools tend to solve only one part of this journey.

HackLoop aims to connect these stages into one workflow.

------------------------------------------------------------------------

## 3. Target Users

### Primary user

College students who regularly participate in hackathons.

Typical characteristics:

-   Technical or design background
-   Limited hackathon time
-   Frequently works in small teams
-   Uses GitHub, Figma, AI coding tools, or similar tools
-   Wants to build something impressive quickly
-   May have limited experience with product planning

### Secondary users

-   Student hackathon organizers
-   Mentors
-   Judges
-   Early-career developers
-   Designers looking for technical teammates

These secondary audiences are NOT first-class V1 users. They may be
introduced in later versions.

------------------------------------------------------------------------

## 4. Core User Persona

### The Hackathon Builder

A student wants to participate in a hackathon but has problems with:

-   finding suitable events
-   choosing an idea
-   validating the idea
-   finding the right teammates
-   organizing the project
-   preparing the final submission

Their desired outcome is not "use an AI chatbot."

Their desired outcome is:

> **Finish a credible hackathon project and submit it confidently before
> the deadline.**

------------------------------------------------------------------------

## 5. Core User Journey

``` text
Sign Up
   ↓
Create Profile
   ↓
Discover Hackathons
   ↓
Select Hackathon
   ↓
Create Project
   ↓
AI Copilot
   ↓
Define Problem + Solution
   ↓
Identify Required Skills
   ↓
Find Teammates
   ↓
Create Project Workspace
   ↓
Build + Track Tasks
   ↓
AI Submission Review
   ↓
Improve
   ↓
Submit
```

Every stage should create or enrich reusable project data.

------------------------------------------------------------------------

## 6. V1 Product Scope

### Feature 1 --- Authentication & Profile

Users can:

-   Sign up
-   Log in
-   Create a profile
-   Add skills
-   Add interests
-   Add experience level
-   Add preferred technologies
-   Indicate availability
-   Add portfolio/GitHub links

The profile becomes the foundation for recommendations and team
matching.

------------------------------------------------------------------------

### Feature 2 --- Hackathon Discovery

Users can:

-   Browse hackathons
-   Search hackathons
-   Filter by category
-   Filter by technology
-   Filter by online/offline
-   Filter by deadline
-   View prize information
-   View eligibility
-   View themes/tracks
-   Save hackathons
-   Open a detailed hackathon page

The system should store structured hackathon data.

Do not make AI responsible for basic filtering.

AI should enhance discovery after the underlying data is reliable.

------------------------------------------------------------------------

### Feature 3 --- AI Hackathon Copilot

This is the flagship V1 AI feature.

A user can provide a rough idea such as:

> "I want to build something for elderly people living alone."

The Copilot should transform the idea into structured project
information:

-   Problem statement
-   Target users
-   Proposed solution
-   Core features
-   Differentiator
-   Technical approach
-   Suggested tech stack
-   MVP scope
-   Future scope
-   Hackathon pitch

The user can iterate using natural language.

Examples:

-   "Make this buildable in 24 hours."
-   "Reduce the scope."
-   "Make it more technically innovative."
-   "Focus on accessibility."
-   "Rewrite this as a 60-second pitch."

### Critical requirement

The result must become an editable **Project**, not disappear as a chat
response.

------------------------------------------------------------------------

### Feature 4 --- AI Team Matching

The system should identify the skills required by a project.

Example:

``` text
Project requirements

Backend       High
AI/ML         High
Frontend      Medium
UI/UX         Low
Pitch         Medium
```

It then compares those requirements with user profiles.

Matching should consider:

-   Skills
-   Skill gaps
-   Interests
-   Availability
-   Experience
-   Project requirements

V1 can use structured skill matching.

Semantic/vector matching can be introduced after the basic workflow
works.

------------------------------------------------------------------------

### Feature 5 --- Project Workspace

Each project gets a workspace containing:

``` text
Project
├── Overview
├── Problem
├── Solution
├── Features
├── Team
├── Tasks
├── Research
├── Files
├── Links
├── GitHub
└── Submission
```

The workspace is the central source of project context for HackLoop AI.

------------------------------------------------------------------------

### Feature 6 --- AI Submission Reviewer

Before submission, the user provides or selects:

-   Problem statement
-   Solution
-   Features
-   README
-   Architecture information
-   Pitch
-   Demo information
-   Hackathon judging criteria

The AI identifies:

-   Missing information
-   Weak explanations
-   Unclear differentiation
-   Technical gaps
-   Unsupported claims
-   Missing judging criteria
-   Areas that need stronger evidence

It should provide:

``` text
Criterion
Evidence
Potential gap
Recommendation
Suggested improvement
```

Avoid fake numerical precision such as "Innovation = 82" until a
defensible scoring framework exists.

------------------------------------------------------------------------

## 7. V1 User Roles

### Participant

Can:

-   Create profile
-   Discover hackathons
-   Create projects
-   Use AI Copilot
-   Find teammates
-   Join projects
-   Manage tasks
-   Review submissions

### Team Member

A participant attached to a project with project-specific permissions.

### Admin

Internal HackLoop role.

Can:

-   Manage hackathon records
-   Manage reported content
-   Manage users
-   Monitor system health

Admin tooling can remain basic in V1.

------------------------------------------------------------------------

## 8. V1 Screens

### Public

``` text
/
├── Landing
├── Explore Hackathons
├── Hackathon Details
├── About
└── Login / Sign Up
```

### Authenticated

``` text
/dashboard

/explore
/hackathons/:id

/projects
/projects/:id
/projects/:id/copilot
/projects/:id/team
/projects/:id/workspace
/projects/:id/review
/projects/:id/submission

/profile
/settings
```

------------------------------------------------------------------------

## 9. Core AI Agents

V1 should start with three primary AI systems.

### Agent 1 --- Hackathon Copilot

Purpose:

Turn rough ideas into structured, buildable projects.

Input:

-   User idea
-   Selected hackathon
-   Hackathon rules
-   User skills
-   Time constraints

Output:

-   Problem
-   Users
-   Solution
-   Features
-   Architecture
-   MVP
-   Differentiator
-   Pitch

------------------------------------------------------------------------

### Agent 2 --- Team Matcher

Purpose:

Find people who fill project skill gaps.

Input:

-   Project requirements
-   User profiles
-   Skills
-   Availability
-   Interests

Output:

-   Candidate recommendations
-   Match explanation
-   Skill gap explanation

------------------------------------------------------------------------

### Agent 3 --- Submission Reviewer

Purpose:

Improve submission quality against the actual hackathon requirements.

Input:

-   Hackathon criteria
-   Project information
-   README
-   Pitch
-   Demo information

Output:

-   Gaps
-   Evidence
-   Recommendations
-   Suggested rewrites

------------------------------------------------------------------------

## 10. Future AI Agents

Do NOT build these in V1.

Potential V2/V3 agents:

-   AI Project Manager
-   AI Technical Mentor
-   AI Judge Simulator
-   AI Demo Coach
-   AI Research Agent
-   AI Architecture Reviewer
-   AI Pitch Coach

These should only be developed after users demonstrate a real need.

------------------------------------------------------------------------

## 11. Product Architecture

### Frontend

-   Next.js
-   TypeScript
-   Tailwind CSS
-   shadcn/ui
-   Framer Motion

### Backend

-   Supabase
-   PostgreSQL
-   Supabase Auth
-   Supabase Storage
-   Row Level Security
-   pgvector when semantic matching is needed

### AI application layer

Use a provider-neutral AI abstraction so HackLoop is not permanently
tied to one model provider.

The application should support model routing based on task complexity
and cost.

### Deployment

-   Vercel
-   Supabase

### Source control

-   GitHub

------------------------------------------------------------------------

## 12. AI Development Team

HackLoop development should use different AI tools for different
responsibilities.

### ChatGPT

Role:

-   Product strategy
-   Product planning
-   Research
-   Requirements
-   Brainstorming
-   Debugging discussions
-   Decision support

### Claude

Role:

-   Product architecture
-   Specification review
-   Architecture critique
-   UX reasoning
-   Code review
-   Edge-case analysis

### Codex

Role:

-   Repository implementation
-   Feature development
-   Refactoring
-   Tests
-   Debugging
-   Database migrations
-   Engineering tasks

### Antigravity

Role:

-   Autonomous implementation tasks
-   Browser testing
-   End-to-end flows
-   Visual QA
-   Repetitive engineering tasks
-   Multi-agent execution

### Figma

Role:

-   Product design
-   Design system
-   Prototypes
-   Responsive layouts
-   Developer handoff

------------------------------------------------------------------------

## 13. AI Development Workflow

Never ask an AI agent:

> "Build HackLoop."

Instead:

``` text
Product decision
      ↓
Specification
      ↓
Architecture
      ↓
Design
      ↓
Implementation
      ↓
Automated tests
      ↓
Browser QA
      ↓
Code review
      ↓
Fix
      ↓
Deploy
```

Each feature should move through this loop independently.

------------------------------------------------------------------------

## 14. Repository Structure

Recommended structure:

``` text
hackloop/
│
├── app/
├── components/
├── features/
│   ├── auth/
│   ├── hackathons/
│   ├── projects/
│   ├── teams/
│   ├── submissions/
│   └── ai/
│
├── agents/
│   ├── copilot/
│   ├── matcher/
│   └── reviewer/
│
├── lib/
│   ├── supabase/
│   ├── ai/
│   └── integrations/
│
├── prompts/
├── tests/
├── supabase/
│   ├── migrations/
│   └── seed/
│
├── docs/
│
├── AGENTS.md
└── README.md
```

------------------------------------------------------------------------

## 15. Initial Database Entities

Start with:

``` text
users
profiles
skills
profile_skills

hackathons
hackathon_tracks
hackathon_rules

projects
project_members
project_skills
project_tasks
project_documents
project_links

ai_sessions
ai_generations

submissions
submission_reviews

notifications
```

Do not create dozens of tables before the first workflow is implemented.

------------------------------------------------------------------------

## 16. V1 Non-Goals

These are explicitly outside V1:

-   Native mobile app
-   Social feed
-   Full Discord replacement
-   Full project management replacement
-   Custom AI model
-   Marketplace
-   Judge marketplace
-   Organizer analytics suite
-   Complex gamification
-   Multiple external hackathon integrations
-   Full GitHub automation
-   AI Judge Simulator
-   AI Demo Coach
-   AI Mentor
-   Autonomous coding agent inside the user's project

The goal is to prove the core participant workflow first.

------------------------------------------------------------------------

## 17. Success Criteria

V1 is successful if real participants can complete this workflow without
manual intervention:

``` text
Create account
   ↓
Create profile
   ↓
Find a relevant hackathon
   ↓
Create project
   ↓
Generate/refine project using AI
   ↓
Find teammates
   ↓
Create project tasks
   ↓
Prepare submission
   ↓
Run AI review
   ↓
Improve submission
```

### Initial validation target

Recruit:

**20--50 real hackathon participants.**

Measure:

-   Profile completion
-   Hackathon discovery usage
-   Projects created
-   AI Copilot usage
-   Teams formed
-   Projects reaching workspace stage
-   Submission reviews completed
-   Repeat usage
-   User-reported usefulness

Do not optimize for registered users alone.

------------------------------------------------------------------------

## 18. Product North Star

The primary question HackLoop should answer is:

> **How many users successfully move from hackathon discovery to a
> submission-ready project?**

This is more meaningful than:

-   Number of AI messages
-   Number of signups
-   Number of page views
-   Number of generated ideas

AI usage is not the goal.

**Successful hackathon progress is the goal.**

------------------------------------------------------------------------

## 19. V1 Build Order

### Stage 0 --- Product

1.  Product Blueprint
2.  User journeys
3.  Feature specifications
4.  Database model
5.  AI agent specifications

### Stage 1 --- Design

1.  Design tokens
2.  Components
3.  Authentication
4.  Dashboard
5.  Explore
6.  Hackathon details
7.  Copilot
8.  Project workspace
9.  Team matching
10. Submission review

### Stage 2 --- Foundation

1.  Next.js
2.  Supabase
3.  Authentication
4.  Database
5.  RLS
6.  Routing
7.  Core components

### Stage 3 --- Core workflow

1.  Hackathon discovery
2.  Project creation
3.  AI Copilot
4.  Team matching
5.  Project workspace
6.  Submission reviewer

### Stage 4 --- Validation

1.  Automated tests
2.  Browser testing
3.  Mobile testing
4.  Accessibility
5.  Performance
6.  Security
7.  Analytics

### Stage 5 --- Real users

Recruit 20--50 participants.

Observe where they struggle.

Only then decide what belongs in V2.

------------------------------------------------------------------------

## 20. V2 Direction

After V1 validation, potential expansion:

``` text
HackLoop
│
├── AI Project Manager
├── AI Technical Mentor
├── AI Judge Simulator
├── AI Demo Coach
├── GitHub intelligence
├── Figma intelligence
├── Organizer tools
├── Mentor marketplace
└── Hackathon analytics
```

These are possibilities, not commitments.

------------------------------------------------------------------------

## 21. Guiding Principle

HackLoop should not become:

> "A website containing several AI tools."

It should become:

> **"The AI-native workspace for building hackathon projects."**

AI should understand the context of the hackathon, project, team,
deadline, requirements, and submission --- and help the user move
forward.

The product should always optimize for **progress**, not AI novelty.
