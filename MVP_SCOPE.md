# HackLoop AI — MVP Scope

## 1. Purpose

This document defines exactly what HackLoop V1 will contain, what it will deliberately postpone, and what “MVP complete” means.

The goal is not to build the biggest hackathon platform.

The goal is to prove one complete product loop:

> Discover a hackathon → create an idea → turn it into a project → form a team → build/organize the work → review the submission → become submission-ready.

If a feature does not materially improve that loop, it should not block V1.

---

# 2. V1 Product Definition

### HackLoop V1

An AI-native workspace that helps hackathon participants move from a hackathon opportunity to a structured, team-based, submission-ready project.

### Primary user

A hackathon participant who:

- joins hackathons regularly or occasionally
- has ideas but struggles to structure them
- needs teammates with complementary skills
- wants help turning an idea into an MVP
- wants feedback before submitting

### Core product loop

```text
Discover
   ↓
Select Hackathon
   ↓
Create Project
   ↓
AI Copilot
   ↓
Define Project
   ↓
Find Team
   ↓
Build / Organize
   ↓
Submission Review
   ↓
Submission Ready
```

---

# 3. MVP Scope Rules

Every feature must pass three questions:

1. Does it support the core hackathon journey?
2. Does it provide meaningful user value in V1?
3. Can it be implemented without creating unnecessary platform complexity?

If the answer is no to any of these, the feature should be postponed.

---

# 4. MUST HAVE — V1

These features are required for the first usable release.

## 4.1 Authentication

### Required

- Sign up
- Login
- Logout
- Session persistence
- Password reset
- Protected routes
- Basic account settings

### Definition of done

A user can create an account and securely access their personal HackLoop workspace.

---

# 5. Profile

## Required profile fields

- Name
- Profile photo/avatar
- Short bio
- Experience level
- Skills
- Technologies
- Interests
- Availability
- GitHub URL
- Portfolio URL
- LinkedIn URL

## Why it matters

The profile becomes the foundation for:

- Team Matching
- Personalization
- AI context
- Future recommendations

### Definition of done

A user can complete a useful profile and edit it later.

---

# 6. Hackathon Discovery

## Required

Users can:

- Browse hackathons
- Search hackathons
- Filter hackathons
- Open hackathon details
- Save a hackathon
- Start a project from a hackathon

## Initial filters

- Category
- Technology
- Format
- Deadline
- Status

## Hackathon card

Each card should show:

- Name
- Organizer
- Theme
- Deadline
- Prize
- Format
- Relevant technologies
- Save action

## Hackathon detail page

Include:

- Overview
- Theme
- Eligibility
- Tracks
- Rules
- Timeline
- Prizes
- Submission requirements
- Official submission link

### Important V1 constraint

Do NOT build a universal hackathon crawler.

Start with:

- curated hackathons
- manually imported hackathons
- a small controlled data source

The product needs to prove the experience before building ingestion infrastructure.

---

# 7. Project Creation

A project is the central object in HackLoop.

## Required

A user can:

- Create a project
- Attach it to a hackathon
- Select a track
- Name the project
- Save a draft
- Edit the project later

## Project information

- Name
- Problem
- Target users
- Solution
- Differentiator
- Features
- Technical approach
- Technology stack
- MVP
- Future scope
- Pitch

### Project states

```text
Draft
Defined
Team Forming
Planning
Building
Reviewing
Submission Ready
Submitted
Archived
```

---

# 8. AI Hackathon Copilot

This is one of the three core AI capabilities.

## Input

The user can provide:

- rough idea
- problem
- target audience
- technology preference
- hackathon context
- existing project information

## AI should help generate

- Problem statement
- Target users
- Proposed solution
- Core features
- Differentiator
- Technical approach
- Suggested tech stack
- MVP scope
- Future scope
- Pitch

## Critical product behavior

AI output must NOT automatically become final project data.

The flow is:

```text
User Input
   ↓
AI Generation
   ↓
AI Suggested Content
   ↓
User Reviews
   ↓
Accept / Edit / Reject
   ↓
Project Data
```

### Definition of done

A participant can start with a rough idea and leave with a structured project draft.

---

# 9. AI Team Matching

This is the second core AI capability.

## Required

The system identifies:

- project skill requirements
- current team skills
- skill gaps

Then suggests potential teammates.

## Candidate matching context

Use:

- skills
- proficiency
- experience
- interests
- availability
- project requirements

## Recommendation UI

Do not show only:

> 94% Match

Instead explain:

> Recommended because they have React + Firebase experience and your project currently lacks frontend implementation skills.

## Required actions

- View profile
- Invite teammate
- Accept invitation
- Decline invitation
- Remove member

### Definition of done

A project owner can identify missing skills and invite suitable participants.

---

# 10. Project Workspace

The workspace is the operational center of HackLoop.

## Required sections

- Overview
- Problem
- Solution
- Features
- Team
- Tasks
- Research
- Files
- Links
- Submission

## Project header

Show:

- Project name
- Hackathon
- Current status
- Progress
- Primary next action

---

# 11. Tasks

V1 needs lightweight project management.

## Required

- Create task
- Edit task
- Assign task
- Change status
- Set priority
- Set due date
- Mark complete

## Statuses

```text
TODO
IN PROGRESS
BLOCKED
DONE
```

## Priority

```text
LOW
MEDIUM
HIGH
CRITICAL
```

### Important boundary

This is NOT a Jira/Trello/Linear replacement.

Only build enough task management to support a hackathon project.

---

# 12. Project Files & Links

## Required

Users can store:

- Documents
- Design links
- Research links
- Demo links
- GitHub repository
- External resources

V1 can use Supabase Storage for project files.

GitHub integration initially means:

- repository URL
- basic validation

Do not build full GitHub synchronization in V1.

---

# 13. AI Submission Reviewer

This is the third core AI capability.

## Input context

The reviewer receives:

- Hackathon
- Track
- Rules
- Submission requirements
- Project
- Submission content
- Relevant project documents

## Review output

Each finding should contain:

- Requirement
- Evidence
- Status
- Gap
- Recommendation
- Suggested improvement

## Statuses

```text
Addressed
Partially Addressed
Missing
Unclear
Not Applicable
```

## Example

```text
Requirement:
Project must demonstrate use of AI.

Evidence:
The project description mentions an AI recommendation engine.

Status:
Partially Addressed

Gap:
The implementation approach is not explained.

Recommendation:
Add the model/provider, input data, and role of AI in the system architecture.
```

### Definition of done

A participant can run a review and receive actionable gaps they can resolve before submission.

---

# 14. Submission Readiness

The product should not end with an AI score.

Use a checklist.

## Example

```text
✓ Problem defined
✓ Solution explained
✓ Team complete
✓ MVP defined
✓ GitHub linked
✓ Demo linked
⚠ Eligibility evidence unclear
⚠ AI implementation needs explanation
✗ Final submission description missing
```

The user should be able to click a missing item and jump directly to the relevant project field.

---

# 15. Dashboard

The dashboard should answer:

> “What should I do next?”

## Required sections

### Greeting

Simple contextual greeting.

### Next Best Action

Examples:

- Complete your profile
- Finish project definition
- Find a frontend teammate
- Run submission review
- Fix missing submission requirements

### Continue Project

Show active projects.

### Recommended Hackathons

Show relevant opportunities.

### Notifications

Show:

- team invitations
- project activity
- important deadlines

---

# 16. Notifications

V1 notifications should be simple.

## Required events

- Team invitation received
- Team invitation accepted
- Team invitation declined
- Project member joined
- Important deadline approaching
- Submission review completed

No advanced notification center is required initially.

---

# 17. Admin / Internal Tools

A minimal admin capability is required to maintain hackathon data.

## Required

Admin can:

- Add hackathon
- Edit hackathon
- Archive hackathon
- Add tracks
- Add rules
- Add submission requirements

This can initially be a very basic internal interface.

Do not build a sophisticated organizer platform.

---

# 18. AI Architecture Boundary

HackLoop V1 has exactly three primary AI agents:

## Agent 1 — Hackathon Copilot

```text
Idea → Structured Project
```

## Agent 2 — Team Matcher

```text
Project Skill Gaps → Candidate Recommendations
```

## Agent 3 — Submission Reviewer

```text
Hackathon Requirements + Project → Actionable Review
```

A lightweight project assistant can exist as supporting infrastructure, but it should not become a fourth major product surface during MVP development.

---

# 19. SHOULD HAVE — After Core V1 Works

These features can improve the product but should not delay the first usable release.

## Discovery

- Better personalization
- More sophisticated filters
- More hackathon sources
- Deadline reminders
- Similar hackathon recommendations

## Profile

- GitHub project import
- Skill inference
- Portfolio parsing
- Achievement history

## Team

- Team availability calendar
- Team roles
- Team invitation links
- Team chat integration
- Better candidate explanations

## Project

- Kanban board improvements
- Project templates
- AI-generated task suggestions
- Research summaries
- Project activity timeline

## AI

- Project Assistant
- Technical Mentor
- Pitch Coach
- Architecture Reviewer

## Submission

- Submission templates
- Version history
- Better requirement extraction
- Submission document generation

---

# 20. LATER — V2+

These are intentionally postponed.

## AI Agents

- AI Judge Simulator
- AI Demo Coach
- AI Research Agent
- Autonomous Coding Agent
- AI Pitch Coach
- AI Technical Mentor

## Integrations

- GitHub OAuth
- GitHub issues synchronization
- GitHub PR integration
- Discord
- Slack
- Google Drive
- Notion

## Platform

- Native mobile application
- Advanced realtime collaboration
- Dedicated search engine
- Semantic/vector search
- Marketplace
- Public project community
- Social feed
- Team reputation system

## Organizer Platform

- Organizer dashboard
- Participant analytics
- Submission management
- Judging workflow
- Judge assignment
- Advanced hackathon management

---

# 21. DO NOT BUILD FOR V1

These are explicitly out of scope.

### 1. Custom AI model

Use existing model providers.

### 2. AI chatbot homepage

HackLoop is not “ChatGPT for hackathons.”

### 3. Discord replacement

Do not build full messaging infrastructure.

### 4. Social network

No feed, likes, followers, comments, or creator ecosystem.

### 5. Marketplace

No paid mentors, judges, developers, designers, or services.

### 6. Complex gamification

No XP economy, badges, leaderboards, streaks, etc.

### 7. Microservices

Use a modular monolith.

### 8. Kubernetes

Not needed.

### 9. Dedicated vector database

Not needed until retrieval requirements justify it.

### 10. Universal hackathon crawler

Start controlled.

### 11. Full GitHub automation

Store repository links first.

### 12. Native mobile apps

Responsive web first.

---

# 22. MVP Screen Set

The minimum screen inventory is:

## Public

1. Landing
2. Login
3. Sign Up
4. Explore Hackathons
5. Hackathon Details

## Onboarding

6. Profile Setup

## Core App

7. Dashboard
8. Projects
9. Create Project
10. AI Copilot
11. Project Workspace
12. Team Matching
13. Team Member Profile
14. Task Workspace
15. Submission Review
16. Submission Readiness
17. Profile
18. Settings

## Internal

19. Admin Hackathon Management

---

# 23. V1 Acceptance Criteria

HackLoop V1 is not “done” because all screens exist.

It is done when a real participant can complete this journey:

### Step 1

Create an account.

### Step 2

Complete their profile.

### Step 3

Discover a hackathon.

### Step 4

Open its requirements.

### Step 5

Start a project.

### Step 6

Use Hackathon Copilot.

### Step 7

Accept/edit generated project information.

### Step 8

Identify project skill gaps.

### Step 9

Find and invite a teammate.

### Step 10

Create and complete project tasks.

### Step 11

Add required links/files.

### Step 12

Run Submission Reviewer.

### Step 13

Resolve important findings.

### Step 14

Reach Submission Ready.

### Step 15

Submit or proceed to the official submission platform.

That is the MVP.

---

# 24. Quality Gates

Before calling V1 complete, verify:

## Product

- Core journey works end-to-end.
- No dead-end screens.
- Every major screen has a clear next action.
- Project is the central context.

## UX

- Responsive on desktop/tablet/mobile.
- WCAG 2.1 AA baseline.
- AI content is visually distinguished.
- Loading, error, empty, and success states exist.
- No unnecessary modal chains.

## AI

- Structured outputs validated.
- AI never silently overwrites user data.
- Context is explicit.
- Missing information is acknowledged.
- AI does not invent hackathon requirements.
- Provider/model is tracked.

## Security

- Protected routes work.
- Server-side authorization exists.
- Supabase RLS is configured.
- Secrets are server-side only.
- Project data cannot be accessed by unauthorized users.

## Engineering

- Database migrations are version controlled.
- Unit tests cover critical logic.
- Integration tests cover key server actions.
- Playwright covers the core journey.
- Errors are monitored.
- Production deployment works.

---

# 25. MVP Success Metrics

The first release should optimize for learning, not vanity metrics.

## Activation

- Signup completed
- Profile completed
- First hackathon viewed
- First project created

## AI activation

- Copilot started
- Copilot output accepted/edited
- Team Matcher used
- Submission Review used

## Product progression

- Project defined
- Team formed
- Tasks created
- Submission review completed
- Submission-ready state reached

## Outcome

Most important:

> Number of users who successfully move from hackathon discovery to a submission-ready project.

---

# 26. Initial Validation Target

Do not wait for thousands of users.

Start with approximately:

```text
20–50 real hackathon participants
```

Observe:

- Where they stop
- What they misunderstand
- Which AI outputs they edit
- Which recommendations they trust
- Whether team matching is useful
- Whether review findings actually improve submissions
- Which features they never touch

Use those findings to determine V1.1.

---

# 27. Build Priority

The implementation order should be:

```text
P0 — Foundation
Auth
Database
Profile
Design system
Application shell

P1 — Hackathon Journey
Hackathon data
Explore
Hackathon details
Project creation

P2 — AI Core
Hackathon Copilot
Structured project generation

P3 — Team
Project skills
Skill gaps
Team matching
Invitations

P4 — Workspace
Tasks
Files
Links
Project progress

P5 — Submission
Submission data
Submission Reviewer
Submission readiness

P6 — Validation
Analytics
Error monitoring
E2E tests
Real-user testing
```

---

# 28. Definition of a Good V1

A good V1 is NOT:

> “HackLoop has lots of features.”

A good V1 is:

> “A hackathon participant can enter HackLoop with an opportunity or idea and leave with a structured, team-supported, reviewed project that is ready to submit.”

Everything else is secondary.

---

# 29. Founder Rule

During development, whenever a new feature idea appears, place it into one of four buckets:

```text
MUST HAVE
SHOULD HAVE
LATER
NO
```

If it does not strengthen the core journey, do not let it enter V1.

The biggest risk for HackLoop is not lack of features.

The biggest risk is building too much before proving the core loop.

---

# 30. Final MVP Statement

> HackLoop V1 is an AI-native hackathon project workspace that connects hackathon discovery, project ideation, team formation, lightweight execution, and submission review into one continuous workflow.

The MVP succeeds when the product can reliably take a participant from:

**“I want to join this hackathon.”**

to:

**“My project is structured, my team is ready, my gaps are identified, and I know what I need to fix before submitting.”**
