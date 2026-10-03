# HackLoop AI — Build Plan

## 1. Purpose

This is the execution roadmap for building HackLoop V1.

The planning documents define **what HackLoop should be**.

This document defines:

> **What to build, in what order, with which AI/tool, and what must be true before moving forward.**

The goal is to avoid trying to build the entire startup at once.

Build one validated layer at a time.

---

# 2. The Build Philosophy

HackLoop should be built as:

```text
Product Decision
      ↓
Specification
      ↓
Design
      ↓
Implementation
      ↓
Testing
      ↓
Review
      ↓
Real User Feedback
      ↓
Next Product Decision
```

Never:

```text
"AI, build my entire startup."
```

Instead:

```text
"Here is the approved feature specification.
Implement only this feature.
Do not change unrelated parts."
```

---

# 3. AI Tool Responsibilities

## ChatGPT

Use for:

- Product strategy
- Requirements
- User flows
- UX reasoning
- Feature prioritization
- AI architecture
- Data model decisions
- Product analytics
- Research
- Acceptance criteria
- Prompt/system design
- Reviewing product decisions

ChatGPT should remain the product brain.

---

## Claude

Use for:

- Architecture critique
- Technical design review
- Complex reasoning
- Edge cases
- Code review
- Security review
- Refactoring recommendations
- AI prompt/schema review

Claude should challenge implementation decisions.

---

## Figma

Use for:

- UI design
- Design system
- Responsive layouts
- Components
- Prototypes
- Interaction design
- Visual QA references
- Developer handoff

Figma should become the visual source of truth.

---

## Codex

Use for:

- Repository implementation
- Feature coding
- Refactoring
- Tests
- Database migrations
- Bug fixes
- API/server implementation
- Integration work

Codex should implement approved specifications rather than invent product behavior.

---

## Antigravity

Use for:

- Autonomous implementation tasks
- Browser testing
- End-to-end flows
- Visual QA
- Repetitive fixes
- Cross-screen validation

Antigravity is especially useful after a feature is implemented.

---

# 4. Recommended Development Loop

For every meaningful feature:

```text
1. Define
      ↓
2. Specify
      ↓
3. Design
      ↓
4. Review
      ↓
5. Implement
      ↓
6. Test
      ↓
7. Visual QA
      ↓
8. Code Review
      ↓
9. Fix
      ↓
10. Commit
```

Only then move to the next feature.

---

# 5. Phase 0 — Product Lock

### Goal

Freeze the V1 scope before coding.

### Complete

- Product Blueprint
- User Flows
- Product Requirements
- AI Architecture
- Data Model
- Technical Architecture
- Design System
- MVP Scope
- Build Plan

### Decision

The following are V1:

- Authentication
- Profile
- Hackathon discovery
- Hackathon details
- Project creation
- AI Hackathon Copilot
- Team Matching
- Project Workspace
- Tasks
- Files/Links
- Submission Review
- Submission Readiness
- Basic notifications
- Minimal admin hackathon management

### Exit condition

No new major feature enters V1 without an explicit product decision.

---

# 6. Phase 1 — Repository & Infrastructure

### Goal

Create a clean technical foundation.

## Stack

```text
Next.js
TypeScript
Tailwind CSS
shadcn/ui
Framer Motion
Supabase
Vercel
GitHub
AI Gateway / provider abstraction
Zod
Playwright
PostHog
Sentry
```

## Tasks

### 1. Create GitHub repository

Recommended:

```text
hackloop
```

### 2. Create Next.js application

Use TypeScript.

### 3. Configure

- ESLint
- Prettier
- TypeScript strict mode
- Environment variables
- Tailwind
- shadcn/ui

### 4. Create Supabase project

Configure:

- PostgreSQL
- Auth
- Storage
- RLS

### 5. Connect Vercel

Create:

```text
Production
Preview
Local
```

### 6. Create environment strategy

Never commit:

- API keys
- Supabase service role keys
- AI provider secrets
- OAuth secrets

### Exit condition

A clean Next.js application deploys successfully to Vercel and connects to Supabase.

---

# 7. Phase 2 — Database Foundation

### Goal

Implement the core data model.

Create migrations for:

```text
users
profiles
skills
profile_skills

hackathons
hackathon_tracks
hackathon_rules
saved_hackathons

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

## Important

Do not create random tables during feature development.

Update the data model deliberately through migrations.

## RLS

Every project-owned entity must enforce authorization.

Example:

```text
User A
  ↓
Project A
  ↓
Tasks A

User B
  X
Tasks A
```

### Exit condition

Database schema exists, migrations are version controlled, and authorization policies are tested.

---

# 8. Phase 3 — Authentication

### Build

- Sign up
- Login
- Logout
- Password reset
- Session persistence
- Protected routes

### Routes

```text
/login
/signup
/forgot-password
```

### Test

- Unauthenticated user cannot access dashboard
- Authenticated user can access dashboard
- User cannot access another user's private data

### Exit condition

Authentication and authorization work reliably.

---

# 9. Phase 4 — Profile & Onboarding

### Build

Profile setup flow:

```text
Account
 ↓
Name
 ↓
Bio
 ↓
Experience
 ↓
Skills
 ↓
Technologies
 ↓
Availability
 ↓
Links
 ↓
Complete
```

### UX principle

Do not create a giant form.

Use progressive steps.

### AI opportunity

AI can eventually infer skills from GitHub/portfolio, but this is not required for V1.

### Exit condition

A participant can create a meaningful profile.

---

# 10. Phase 5 — Application Shell

Build the shared product structure.

## Desktop navigation

```text
HackLoop
────────────
Dashboard
Explore
Projects
Profile
Settings
```

## Mobile

Use a simplified contextual navigation/bottom navigation where appropriate.

## Shared components

Implement:

- Button
- Input
- Textarea
- Select
- Checkbox
- Badge
- Avatar
- Card
- Modal
- Drawer
- Tabs
- Toast
- Skeleton
- Progress
- Breadcrumb

### Exit condition

Every future page can use a consistent shell and component system.

---

# 11. Phase 6 — Hackathon Discovery

### First create controlled data

Start with a small set of real/curated hackathons.

Each hackathon needs:

- Name
- Organizer
- Description
- Theme
- Format
- Location
- Registration deadline
- Submission deadline
- Prize
- Eligibility
- Tracks
- Rules
- Submission requirements
- Official URL
- Source

### Build

```text
/explore
/hackathons/:id
```

### Features

- Search
- Filter
- Save
- View details
- Start project

### Exit condition

A participant can discover an opportunity and begin a project from it.

---

# 12. Phase 7 — Project Creation

### Build

```text
/projects
/projects/new
/projects/:id
```

### Creation flow

```text
Choose Hackathon
      ↓
Choose Track
      ↓
Name Project
      ↓
Start with blank project
      OR
Use AI Copilot
```

### Project state

Initially:

```text
Draft
```

### Exit condition

A project is created and persisted correctly.

---

# 13. Phase 8 — AI Gateway

Before building the individual AI agents, create the AI infrastructure.

## Responsibilities

```text
Agent Registry
      ↓
Context Builder
      ↓
Prompt Builder
      ↓
Model Provider
      ↓
Structured Output
      ↓
Zod Validation
      ↓
Usage Tracking
```

## Agent registry

```text
hackathon_copilot
team_matcher
submission_reviewer
```

## AI request flow

```text
User
 ↓
Server
 ↓
Auth Check
 ↓
Load Context
 ↓
Build Prompt
 ↓
AI Provider
 ↓
Validate Output
 ↓
Return Structured Result
 ↓
User Review
 ↓
Persist Accepted Data
```

### Critical rule

AI secrets never reach the browser.

### Exit condition

A provider-independent AI request can safely return validated structured data.

---

# 14. Phase 9 — AI Hackathon Copilot

### Build UI

```text
Project
  ↓
AI Copilot
  ↓
Idea Input
  ↓
Generate
  ↓
Structured Suggestions
```

### Output schema

```text
problem
target_users
solution
differentiator
features[]
technical_approach
technology_stack[]
mvp
future_scope
pitch
```

### UX

Each generated section should support:

```text
Accept
Edit
Reject
Regenerate
```

### Important

Do not dump AI output into a chat transcript and call the feature complete.

The output must directly help construct the project.

### Exit condition

A rough idea can become a structured project draft.

---

# 15. Phase 10 — Project Workspace

Build the central project page.

## Structure

```text
Project Header
    ↓
Progress
    ↓
Overview
    ↓
Problem
Solution
Features
Team
Tasks
Research
Files
Links
Submission
```

### Signature component

## Next Best Action

Examples:

```text
Your project is missing a backend contributor.
→ Find teammates
```

or:

```text
Your submission has 3 unresolved requirements.
→ Review project
```

### Exit condition

A user can understand project state and continue work without leaving the workspace.

---

# 16. Phase 11 — Skill Model

Implement:

```text
Skills
Profile Skills
Project Skills
Team Skills
```

## Skill gap calculation

Conceptually:

```text
Required Project Skills
-
Current Team Skills
=
Skill Gaps
```

Example:

```text
Required:
React
Firebase
UI/UX
Python

Team:
React
UI/UX
Python

Gap:
Firebase
```

### Exit condition

Project skill requirements and team coverage are visible.

---

# 17. Phase 12 — AI Team Matcher

### Build

```text
Team
 ↓
Skill Gaps
 ↓
Find Members
 ↓
AI Recommendations
```

### Recommendation context

Use:

- skills
- proficiency
- interests
- experience
- availability
- project requirements

### Recommendation explanation

Every recommendation should answer:

> Why this person?

Example:

```text
Strong fit because:
• Firebase experience
• Backend projects
• Available during hackathon
• Interested in AI applications
```

### Actions

```text
View Profile
Invite
```

### Exit condition

A project owner can identify a gap and invite a relevant teammate.

---

# 18. Phase 13 — Team Invitations

### Build

Statuses:

```text
invited
active
declined
removed
```

### Flow

```text
Owner
 ↓
Invite
 ↓
Candidate
 ↓
Notification
 ↓
Accept / Decline
 ↓
Project Membership Updated
```

### Exit condition

Team formation works end-to-end.

---

# 19. Phase 14 — Tasks

### Build lightweight task management.

```text
Create
Assign
Prioritize
Due Date
Status
Complete
```

### Avoid

- complex dependencies
- advanced project management
- custom workflow builders

### Exit condition

A small team can coordinate hackathon work inside the project.

---

# 20. Phase 15 — Files & Links

### Build

- Upload document
- View document
- Delete document
- Add external link
- Add GitHub URL
- Add demo URL

### Storage

Use Supabase Storage.

### Security

Project files must respect project membership permissions.

### Exit condition

A project can store the resources needed for submission.

---

# 21. Phase 16 — Submission Model

Build:

```text
Submission
```

Fields:

- Description
- Demo URL
- Repository URL
- Documentation URL
- Status

### Status

```text
Draft
Reviewing
Ready
Submitted
```

### Exit condition

Project submission information exists independently from general project notes.

---

# 22. Phase 17 — AI Submission Reviewer

### Context

```text
Hackathon
+
Track
+
Rules
+
Submission Requirements
+
Project
+
Documents
```

### Output

```text
Requirement
Evidence
Status
Gap
Recommendation
Suggested Improvement
```

### UI

Use a review checklist.

Example:

```text
✓ Problem clearly defined
✓ Solution explained
⚠ Technical implementation unclear
✗ Required demo link missing
```

### Interaction

Clicking a finding should navigate to the relevant project/submission field.

### Exit condition

A user can run a review and act on its findings.

---

# 23. Phase 18 — Submission Readiness

Create a final checklist.

## Example

```text
PROJECT
✓ Problem
✓ Solution
✓ Features

TEAM
✓ Required skills covered
✓ Team members confirmed

TECHNICAL
✓ Repository
✓ Architecture
✓ Demo

SUBMISSION
✓ Description
⚠ Eligibility evidence
✗ Final demo
```

### Final state

```text
SUBMISSION READY
```

should only become available when required checks are satisfied.

### Exit condition

A participant can clearly understand whether their project is ready.

---

# 24. Phase 19 — Dashboard Intelligence

Only after the core workflow works.

Dashboard should aggregate real product state.

## Next Best Action

Derive from:

```text
Profile completeness
Project state
Skill gaps
Tasks
Deadline
Review findings
Submission readiness
```

### Example

If:

```text
Project = Reviewing
Unresolved findings = 4
Deadline = 2 days
```

Then:

```text
Next Best Action:
Resolve submission review findings
```

Do not manually hardcode dozens of dashboard states.

---

# 25. Phase 20 — Notifications

Implement the minimum useful notifications.

## Events

```text
Team invitation
Invitation accepted
Invitation declined
Member joined
Deadline approaching
Review completed
```

Keep notification infrastructure simple.

---

# 26. Phase 21 — Admin Hackathon Management

Create an internal admin page.

### Required

- Create hackathon
- Edit
- Archive
- Add track
- Add rules
- Add requirements

### Important

This is an internal tool, not an organizer SaaS product.

---

# 27. Phase 22 — Analytics

Implement product events.

## Core events

```text
signup_completed
profile_completed
hackathon_viewed
hackathon_saved
project_created
copilot_started
copilot_output_accepted
team_invitation_sent
team_member_joined
task_created
task_completed
submission_review_started
submission_gap_resolved
project_submission_ready
```

## North Star

```text
Submission-ready projects
```

But interpret this alongside user activity and qualitative feedback.

---

# 28. Phase 23 — Testing

Testing should happen throughout development, not at the end.

## Unit tests

Test:

- skill gap calculation
- permissions
- status transitions
- readiness logic
- validation schemas

## Integration tests

Test:

- project creation
- team invitation
- AI request validation
- submission review persistence

## E2E tests

Primary journey:

```text
Signup
 ↓
Profile
 ↓
Explore
 ↓
Hackathon
 ↓
Project
 ↓
Copilot
 ↓
Team
 ↓
Tasks
 ↓
Submission
 ↓
Review
 ↓
Ready
```

---

# 29. Phase 24 — AI Quality Testing

Do not judge AI only by whether the output “sounds good.”

Test:

### Schema validity

Does the output conform to the expected schema?

### Context correctness

Did the agent use the right project/hackathon context?

### Hallucination resistance

Does it avoid inventing rules?

### Missing data handling

Does it say when information is unavailable?

### Permission safety

Can users only invoke agents for projects they can access?

### Persistence safety

Can AI accidentally overwrite accepted project data?

---

# 30. Phase 25 — Visual QA

Use Figma as the visual reference.

Test:

- Desktop
- Tablet
- Mobile
- Loading
- Empty
- Error
- Long text
- Large project names
- Large skill lists
- AI generation states
- Accessibility
- Reduced motion

Use Antigravity for browser-based visual and interaction testing.

---

# 31. Phase 26 — Security Review

Before public testing verify:

## Authentication

- Protected routes
- Session handling
- Logout

## Authorization

- RLS
- Project membership
- Admin permissions

## AI

- API keys server-side
- Rate limits
- Input validation
- Output validation

## Storage

- Private project files
- Correct access policies

## General

- No sensitive data in client logs
- No service keys in frontend
- No unsafe HTML rendering
- No trust in client-side permissions

---

# 32. Phase 27 — Deployment

## Environment

```text
Local
 ↓
GitHub branch
 ↓
Vercel Preview
 ↓
QA
 ↓
main
 ↓
Production
```

## Before production

- Database migrations verified
- Environment variables configured
- RLS enabled
- AI provider configured
- Analytics configured
- Error monitoring configured
- E2E smoke test passed

---

# 33. Phase 28 — Private Alpha

Do NOT launch publicly first.

Recruit approximately:

```text
20–50 hackathon participants
```

### Observe

- Where users stop
- What they misunderstand
- Which AI outputs they edit
- Which recommendations they trust
- Whether team matching produces useful candidates
- Whether reviews help
- Whether users return
- Which features are ignored

### Do not immediately add features.

First understand the friction.

---

# 34. Phase 29 — Product Iteration

After the alpha:

```text
User Feedback
      ↓
Behavior Data
      ↓
Identify Friction
      ↓
Prioritize
      ↓
Design
      ↓
Build
      ↓
Test
```

Classify feedback:

```text
Critical
Important
Useful
Interesting
Not Now
```

Do not turn every user request into a feature.

---

# 35. Suggested Build Timeline

This is a flexible sequence rather than a rigid calendar.

## Sprint 1 — Foundation

```text
Repository
Next.js
Supabase
Auth
Database
RLS
Design system
Application shell
```

Output:

> User can securely enter HackLoop.

---

## Sprint 2 — Discovery

```text
Hackathon data
Explore
Filters
Hackathon details
Save
Project creation
```

Output:

> User can discover an opportunity and start a project.

---

## Sprint 3 — AI Copilot

```text
AI Gateway
Context builder
Structured output
Copilot UI
Accept/edit/reject
```

Output:

> User can turn an idea into a structured project.

---

## Sprint 4 — Team

```text
Skills
Project skills
Skill gaps
Candidate discovery
AI matching
Invitations
```

Output:

> User can build a complementary team.

---

## Sprint 5 — Workspace

```text
Project workspace
Tasks
Files
Links
Progress
Next Best Action
```

Output:

> Team can organize project execution.

---

## Sprint 6 — Submission

```text
Submission
Reviewer
Review findings
Readiness checklist
```

Output:

> Team can identify and resolve submission gaps.

---

## Sprint 7 — Hardening

```text
Analytics
E2E
Security
Accessibility
Performance
Error states
Visual QA
```

Output:

> Product is ready for controlled real-user testing.

---

## Sprint 8 — Alpha

```text
20–50 users
Observe
Interview
Measure
Fix
Repeat
```

Output:

> Evidence for what HackLoop should become next.

---

# 36. What You Should Personally Own

As founder + product designer:

## You own

- Product vision
- User problems
- Product decisions
- UX
- Figma
- Design system
- AI behavior expectations
- User testing
- Product analytics interpretation
- Prioritization

You should NOT spend all your time manually writing boilerplate code if AI tools can handle it.

---

# 37. What Codex Should Own

Codex can handle:

- Repository setup
- Components
- Pages
- Server actions
- Route handlers
- Database migrations
- Supabase queries
- Validation
- Tests
- Refactoring
- Bug fixes

Give Codex small, explicit implementation tasks.

---

# 38. What Claude Should Own

Ask Claude to challenge:

- Architecture
- Database relationships
- Security
- AI schemas
- Edge cases
- Permission logic
- Complex implementation decisions

Example:

> “Review this implementation plan for HackLoop Team Matching. Identify data-model, authorization, scalability, and UX edge cases. Do not rewrite the feature.”

---

# 39. What Antigravity Should Own

After implementation:

```text
Open application
 ↓
Follow user flow
 ↓
Find broken interactions
 ↓
Test responsive states
 ↓
Capture failures
 ↓
Report issues
```

Then Codex fixes them.

---

# 40. What Figma Should Own

Figma is the source of truth for:

- visual hierarchy
- components
- spacing
- typography
- responsive behavior
- interactions
- states

Do not design every possible screen before validating the first flow.

Start with:

```text
Landing
 ↓
Explore
 ↓
Hackathon
 ↓
Create Project
 ↓
Copilot
 ↓
Project
 ↓
Team
 ↓
Review
 ↓
Ready
```

---

# 41. First Prototype Flow

Build this flow first in Figma:

```text
Landing
   ↓
Dashboard
   ↓
Explore Hackathons
   ↓
Hackathon Details
   ↓
Start Project
   ↓
AI Copilot
   ↓
Project Workspace
   ↓
Team Matching
   ↓
Tasks
   ↓
Submission Review
   ↓
Submission Ready
```

Do not design the entire product before this flow feels coherent.

---

# 42. Recommended Git Strategy

Use:

```text
main
```

as the production branch.

Feature branches:

```text
feat/auth
feat/profile
feat/hackathon-discovery
feat/project-creation
feat/ai-copilot
feat/team-matching
feat/workspace
feat/submission-review
```

Keep commits small and meaningful.

Example:

```text
feat: add project creation flow
fix: enforce project membership on task queries
feat: add structured copilot response validation
test: cover submission readiness rules
```

---

# 43. Definition of Done for Every Feature

A feature is not done when the page renders.

It is done when:

```text
✓ UX designed
✓ Responsive behavior defined
✓ Empty state exists
✓ Loading state exists
✓ Error state exists
✓ Validation exists
✓ Authorization exists
✓ Database persistence works
✓ Tests exist
✓ Analytics event exists where relevant
✓ Visual QA passed
✓ Code review passed
```

---

# 44. The Golden Rule for AI Development

Never let AI silently make product decisions.

Bad:

> “Build a team matching system.”

Better:

> “Implement the approved Team Matching specification. Use the existing Profile, Skill, Project Skill, and Project Member models. Do not introduce new user-facing behavior. Return the implementation summary and tests.”

AI writes the implementation.

You own the product decision.

---

# 45. The Golden Rule for Scope

Whenever you think:

> “It would be cool if HackLoop also had…”

Stop.

Ask:

```text
Does this help a participant reach submission-ready?
```

If no:

```text
LATER
```

If maybe:

```text
VALIDATE FIRST
```

If yes:

```text
MVP candidate
```

---

# 46. Final End-to-End Build Map

```text
                         HACKLOOP AI

                              │
                              ▼
                    ┌──────────────────┐
                    │   AUTH / PROFILE │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │ HACKATHON DISCOVERY│
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │  PROJECT CREATION│
                    └────────┬─────────┘
                             │
                             ▼
                  ┌───────────────────────┐
                  │   AI HACKATHON COPILOT│
                  └───────────┬───────────┘
                              │
                              ▼
                    ┌──────────────────┐
                    │ PROJECT WORKSPACE │
                    └───────┬──────────┘
                            │
                 ┌──────────┴──────────┐
                 ▼                     ▼
          ┌──────────────┐      ┌──────────────┐
          │ TEAM MATCHING│      │    TASKS     │
          └──────┬───────┘      └──────┬───────┘
                 │                     │
                 └──────────┬──────────┘
                            ▼
                    ┌──────────────────┐
                    │    SUBMISSION    │
                    └────────┬─────────┘
                             │
                             ▼
                 ┌────────────────────────┐
                 │ AI SUBMISSION REVIEWER │
                 └────────────┬───────────┘
                              │
                              ▼
                    ┌──────────────────┐
                    │ SUBMISSION READY │
                    └──────────────────┘
```

---

# 47. The Real Startup Loop

Once V1 is live, HackLoop becomes:

```text
Users
  ↓
Hackathons
  ↓
Projects
  ↓
AI interactions
  ↓
Team formation
  ↓
Submission reviews
  ↓
Real outcomes
  ↓
Product data
  ↓
Better workflows
  ↓
Better AI context
  ↓
Better user outcomes
```

The long-term advantage should not simply be:

> “We have AI.”

It should become:

> “HackLoop understands the complete lifecycle of a hackathon project.”

That context can eventually power much more sophisticated AI.

---

# 48. Long-Term Expansion Path

Only after the core loop is validated:

## V1

```text
Discover
Ideate
Team
Build
Review
Submit
```

## V2

```text
Project Assistant
Technical Mentor
Pitch Coach
Research Agent
GitHub integrations
Better recommendations
```

## V3

```text
Judge Simulator
Demo Coach
Advanced collaboration
Organizer platform
Community
```

## Potential long-term vision

```text
Hackathon Discovery
        ↓
AI Project Formation
        ↓
AI Team Formation
        ↓
AI Planning
        ↓
Human + AI Building
        ↓
AI Validation
        ↓
AI Submission Preparation
        ↓
Project Showcase
        ↓
Portfolio / Career Opportunities
```

Do not build V3 before V1 proves the underlying behavior.

---

# 49. Final Founder Checklist

Before writing significant code:

- [ ] Product Blueprint approved
- [ ] User Flows approved
- [ ] Requirements approved
- [ ] AI architecture approved
- [ ] Data model approved
- [ ] Technical architecture approved
- [ ] Design system approved
- [ ] MVP scope approved
- [ ] Build plan approved

Before each feature:

- [ ] Requirement defined
- [ ] UX flow defined
- [ ] Figma design ready
- [ ] Acceptance criteria written
- [ ] Data requirements understood
- [ ] AI behavior defined if applicable

Before merging:

- [ ] Implementation works
- [ ] Tests pass
- [ ] Authorization checked
- [ ] Responsive QA passed
- [ ] Accessibility checked
- [ ] Error/loading/empty states checked
- [ ] Code reviewed

Before launch:

- [ ] Core E2E flow works
- [ ] Analytics works
- [ ] Error monitoring works
- [ ] Security review complete
- [ ] Production deployment verified
- [ ] Test users recruited

---

# 50. Final Build Order

If you forget everything else, follow this:

```text
1. Foundation
2. Database
3. Auth
4. Profile
5. Application Shell
6. Hackathon Discovery
7. Project Creation
8. AI Gateway
9. AI Copilot
10. Project Workspace
11. Skills
12. Team Matching
13. Team Invitations
14. Tasks
15. Files & Links
16. Submission
17. AI Submission Review
18. Submission Readiness
19. Dashboard Intelligence
20. Notifications
21. Admin
22. Analytics
23. Testing
24. Security
25. Visual QA
26. Deployment
27. Private Alpha
28. Learn
29. Iterate
```

---

# Final Principle

HackLoop does not need to be huge to be valuable.

It needs to make one difficult thing dramatically easier:

> **Turning a hackathon opportunity and a rough idea into a structured, team-supported, submission-ready project.**

Build that loop exceptionally well first.

Everything else earns its place later.
