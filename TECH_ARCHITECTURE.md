# HackLoop --- Technical Architecture

Version: 1.0\
Status: Technical Architecture\
Scope: HackLoop V1

------------------------------------------------------------------------

## 1. Purpose

This document defines the recommended technical architecture for
HackLoop V1.

It translates the product requirements and data model into an
implementation structure that can be handed to engineering AI tools such
as Claude and Codex.

The architecture prioritizes:

-   Fast iteration
-   Low infrastructure complexity
-   Strong developer experience
-   Secure user/project isolation
-   AI provider flexibility
-   Structured AI outputs
-   Easy Vercel deployment
-   Clear separation between product logic and AI logic

------------------------------------------------------------------------

# 2. Architecture Summary

Recommended V1 stack:

``` text
Frontend
Next.js
TypeScript
Tailwind CSS
shadcn/ui
Framer Motion

Backend
Next.js Server Components
Server Actions / Route Handlers

Database
Supabase PostgreSQL

Authentication
Supabase Auth

Storage
Supabase Storage

Realtime
Supabase Realtime where useful

AI
AI Gateway / Provider abstraction
Vercel AI SDK or equivalent abstraction

Hosting
Vercel

Source Control
GitHub

Testing
Playwright
Unit/integration testing

Analytics
PostHog or equivalent

Error Monitoring
Sentry or equivalent
```

The exact libraries can change if engineering validation identifies a
better option.

------------------------------------------------------------------------

# 3. High-Level System

``` text
                         USER
                           │
                           ↓
                  ┌─────────────────┐
                  │   Next.js App   │
                  │ UI + Routing    │
                  └────────┬────────┘
                           │
             ┌─────────────┼─────────────┐
             ↓             ↓             ↓
        Server Logic    AI Gateway    External APIs
             │             │
             ↓             ↓
        ┌─────────┐   ┌──────────────┐
        │Supabase │   │ AI Providers │
        │Postgres │   │ Model A/B/C  │
        │Auth     │   └──────────────┘
        │Storage  │
        └─────────┘
```

The frontend should not directly own sensitive business logic.

------------------------------------------------------------------------

# 4. Frontend Architecture

## Recommended

``` text
Next.js
+
TypeScript
+
App Router
```

Use the App Router to organize:

-   Public pages
-   Authenticated pages
-   Project routes
-   API/server boundaries

------------------------------------------------------------------------

# 5. Frontend Route Structure

Recommended route structure:

``` text
/
├── explore/
├── hackathons/
│   └── [hackathonId]/
├── login/
├── signup/
├── dashboard/
├── projects/
│   ├── new/
│   └── [projectId]/
│       ├── page
│       ├── copilot/
│       ├── team/
│       ├── workspace/
│       ├── review/
│       └── submission/
├── profile/
└── settings/
```

Exact routing syntax should be finalized during implementation.

------------------------------------------------------------------------

# 6. Application Layers

The application should have clear boundaries.

``` text
UI Layer
   ↓
Application Layer
   ↓
Domain Logic
   ↓
Data Access
   ↓
Infrastructure
```

Avoid putting database logic directly into UI components.

------------------------------------------------------------------------

# 7. Recommended Repository Structure

``` text
hackloop/
│
├── app/
│   ├── (public)/
│   ├── (auth)/
│   ├── dashboard/
│   ├── explore/
│   ├── hackathons/
│   ├── projects/
│   ├── profile/
│   └── settings/
│
├── components/
│   ├── ui/
│   ├── layout/
│   ├── hackathons/
│   ├── projects/
│   ├── team/
│   ├── tasks/
│   ├── ai/
│   └── submission/
│
├── lib/
│   ├── supabase/
│   ├── ai/
│   ├── auth/
│   ├── validations/
│   ├── permissions/
│   └── utils/
│
├── services/
│   ├── hackathons/
│   ├── projects/
│   ├── teams/
│   ├── tasks/
│   ├── submissions/
│   └── ai/
│
├── types/
│
├── tests/
│   ├── unit/
│   ├── integration/
│   └── e2e/
│
├── public/
│
├── docs/
│
└── configuration files
```

The final structure can be simplified if the implementation remains
small.

------------------------------------------------------------------------

# 8. Authentication Architecture

Use Supabase Auth for V1.

Conceptually:

``` text
User
 ↓
Supabase Auth
 ↓
Authenticated Session
 ↓
Application User/Profile
```

The application database should reference the authenticated user ID.

------------------------------------------------------------------------

# 9. Authentication Rules

Protected routes must verify authentication.

Examples:

``` text
/dashboard
/projects
/profile
/settings
```

Public routes:

``` text
/
/explore
/hackathons/[id]
/login
/signup
```

A project route must additionally verify project membership or
ownership.

------------------------------------------------------------------------

# 10. Authorization

Authentication answers:

> Who are you?

Authorization answers:

> What are you allowed to do?

HackLoop needs both.

Examples:

### User

Can edit own profile.

### Project Owner

Can manage project membership.

### Team Member

Can access the project according to project permissions.

### Admin

Can manage platform-level resources.

------------------------------------------------------------------------

# 11. Row-Level Security

Supabase Row-Level Security should protect user and project data.

Core principle:

**Never trust the frontend to enforce permissions.**

Examples:

A user should only access:

-   Their own profile
-   Projects they belong to
-   Data they are authorized to see

Project ownership/member relationships should be enforced at the
database/security layer.

------------------------------------------------------------------------

# 12. Database Architecture

Use PostgreSQL through Supabase.

Core tables:

``` text
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

Additional tables should only be added when justified.

------------------------------------------------------------------------

# 13. Database Migration Strategy

Database changes must be version controlled.

Do not manually modify production schema without migrations.

Recommended process:

``` text
Local schema change
      ↓
Migration
      ↓
Test
      ↓
Review
      ↓
Deploy
```

Codex should never make destructive schema changes without explicit
approval.

------------------------------------------------------------------------

# 14. Data Validation

Use a schema validation layer.

Recommended approach:

``` text
Zod
```

Use validation for:

-   API inputs
-   Server actions
-   AI structured outputs
-   Forms
-   Database-facing operations

------------------------------------------------------------------------

# 15. Server Actions vs Route Handlers

Use server actions where they make sense for application mutations.

Examples:

-   Create project
-   Update project
-   Create task
-   Invite teammate
-   Save hackathon

Use route handlers/API endpoints for cases such as:

-   AI streaming
-   External integrations
-   Webhooks
-   Public API endpoints

The exact split should remain pragmatic.

------------------------------------------------------------------------

# 16. AI Architecture

HackLoop should have a central AI gateway.

``` text
UI
 ↓
AI Request
 ↓
AI Gateway
 ↓
Context Builder
 ↓
Agent
 ↓
Model Provider
 ↓
Structured Output
 ↓
Validation
 ↓
UI / Database
```

------------------------------------------------------------------------

# 17. AI Gateway

The AI gateway is responsible for:

-   Agent selection
-   Authentication
-   Context loading
-   Model selection
-   Prompt construction
-   Structured output
-   Validation
-   Error handling
-   Usage tracking

The UI should not contain provider-specific model calls.

------------------------------------------------------------------------

# 18. AI Agent Registry

Agents should have explicit definitions.

Conceptually:

``` text
hackathon_copilot
team_matcher
project_assistant
submission_reviewer
```

Each agent defines:

``` text
Agent name
Purpose
Allowed context
Input schema
Output schema
Model strategy
Permission level
Tools available
```

------------------------------------------------------------------------

# 19. AI Context Builder

Before an AI request is executed:

``` text
User Request
      ↓
Determine Agent
      ↓
Load Required Context
      ↓
Build Context Object
      ↓
Validate Context
      ↓
Run Agent
```

Example:

Submission Reviewer receives:

``` text
Hackathon
Rules
Project
Team
Submission
```

It should not automatically receive every piece of user data.

------------------------------------------------------------------------

# 20. Structured AI Output

Where AI output maps to product data, require structured output.

Example:

``` text
CopilotOutput

problem
target_users
solution
features[]
differentiator
technical_approach
technology_stack[]
mvp[]
future_scope[]
pitch
```

The exact implementation schema should be validated before persistence.

------------------------------------------------------------------------

# 21. AI Output Validation

AI output must pass validation before becoming application data.

``` text
AI
 ↓
Structured Output
 ↓
Schema Validation
 ↓
Business Validation
 ↓
User Confirmation
 ↓
Database
```

Never blindly insert model output into the database.

------------------------------------------------------------------------

# 22. AI Streaming

Streaming can be used for conversational experiences where useful.

Good candidates:

-   Hackathon Copilot
-   Project Assistant

For structured generation, the final validated result should remain the
authoritative output.

------------------------------------------------------------------------

# 23. AI Cost Tracking

Every important AI request should record:

``` text
agent
user_id
project_id
model_provider
model_name
input_tokens
output_tokens
latency
estimated_cost
status
created_at
```

This allows HackLoop to understand AI economics.

------------------------------------------------------------------------

# 24. AI Provider Abstraction

Do not hardcode the application to one provider.

Conceptually:

``` text
HackLoop AI Gateway
        ↓
Provider Adapter
   ┌────┼────┐
   ↓    ↓    ↓
Model A B    C
```

This allows model changes without rewriting product logic.

------------------------------------------------------------------------

# 25. AI Security

Never expose:

-   API keys
-   Provider credentials
-   Server secrets

to the browser.

AI calls requiring secrets must execute server-side.

------------------------------------------------------------------------

# 26. External Hackathon Data

V1 should avoid building a giant universal hackathon crawler.

Start with a controlled data source.

Potential approaches:

1.  Admin-created hackathons
2.  Curated imports
3.  Limited integrations
4.  Carefully validated external ingestion

Every stored hackathon should have a source/reference.

------------------------------------------------------------------------

# 27. Hackathon Data Trust

Hackathon facts should be treated differently from AI-generated
suggestions.

``` text
Official/source data
        ↓
Hackathon database
        ↓
AI context
```

The AI should not invent missing rules.

If data is uncertain:

``` text
Unknown / Not Available
```

rather than hallucinating.

------------------------------------------------------------------------

# 28. File Storage

Use Supabase Storage for V1 project files.

Conceptually:

``` text
Project
 ↓
Storage Bucket
 ↓
Project-specific path
```

Access should be protected using authenticated/project-aware policies.

------------------------------------------------------------------------

# 29. GitHub Integration

V1 should not attempt full GitHub automation.

Initial scope:

-   Store GitHub repository URL
-   Display repository link
-   Optionally verify basic URL validity

Future:

-   OAuth
-   Repository metadata
-   Commit activity
-   Issue synchronization
-   Pull request integration

These are deferred.

------------------------------------------------------------------------

# 30. Realtime

Supabase Realtime can be introduced where it improves collaboration.

Potential V1 uses:

-   Team invitation updates
-   Task updates
-   Project activity

Do not make every UI component realtime by default.

Start with standard data fetching and introduce realtime where users
benefit from immediate updates.

------------------------------------------------------------------------

# 31. Search

V1 search can use PostgreSQL search capabilities.

Search targets:

-   Hackathon name
-   Description
-   Theme
-   Technology
-   Category

A dedicated search engine is unnecessary initially.

------------------------------------------------------------------------

# 32. Vector Search

Do not introduce a vector database just because the product contains AI.

Potential future uses:

-   Semantic hackathon discovery
-   Project knowledge retrieval
-   Document retrieval
-   Similar project discovery

V1 can operate without vector search unless validation proves it
necessary.

Supabase pgvector can be considered later if semantic retrieval becomes
valuable.

------------------------------------------------------------------------

# 33. Caching

Cache relatively stable data where useful.

Examples:

-   Hackathon details
-   Skill taxonomy

Do not aggressively cache highly dynamic project data initially.

Correctness is more important than premature optimization.

------------------------------------------------------------------------

# 34. Analytics

Use product analytics to understand the core journey.

Track events such as:

``` text
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

The event taxonomy should be version controlled.

------------------------------------------------------------------------

# 35. Product Funnel

Core funnel:

``` text
Signup
 ↓
Profile Complete
 ↓
Hackathon Selected
 ↓
Project Created
 ↓
Copilot Used
 ↓
Team Formed
 ↓
Tasks Created
 ↓
Project Built
 ↓
Submission Reviewed
 ↓
Submission Ready
```

This funnel is more meaningful than raw pageviews.

------------------------------------------------------------------------

# 36. Error Monitoring

Use an error monitoring service such as Sentry or an equivalent.

Track:

-   Client errors
-   Server errors
-   Failed AI requests
-   Database errors
-   Integration failures

Do not log secrets or sensitive user information.

------------------------------------------------------------------------

# 37. Logging

Logs should help answer:

-   What failed?
-   Which user/project was affected?
-   Which operation failed?
-   When did it fail?
-   Can it be reproduced?

Avoid logging:

-   Passwords
-   API keys
-   Full sensitive user data
-   Unnecessary private AI context

------------------------------------------------------------------------

# 38. Environment Variables

Sensitive configuration belongs in environment variables.

Examples:

``` text
NEXT_PUBLIC_SUPABASE_URL
NEXT_PUBLIC_SUPABASE_ANON_KEY

SUPABASE_SERVICE_ROLE_KEY

AI_PROVIDER_KEY
AI_MODEL_CONFIGURATION

SENTRY_DSN
POSTHOG_KEY
```

Exact variables depend on chosen providers.

Secrets must never be committed to Git.

------------------------------------------------------------------------

# 39. Environment Strategy

Use at least:

``` text
Local
Preview
Production
```

Recommended flow:

``` text
Developer branch
     ↓
Pull Request
     ↓
Preview deployment
     ↓
Testing
     ↓
Main
     ↓
Production
```

------------------------------------------------------------------------

# 40. Git Strategy

Recommended:

``` text
main
  ↓
feature/*
```

Feature branches should represent focused changes.

Examples:

``` text
feature/auth
feature/hackathon-discovery
feature/project-workspace
feature/ai-copilot
feature/team-matching
feature/submission-review
```

Avoid giant branches containing unrelated features.

------------------------------------------------------------------------

# 41. AI Development Workflow

HackLoop's AI development workflow should follow:

``` text
Product Decision
      ↓
Specification
      ↓
Architecture Review
      ↓
Design
      ↓
Implementation
      ↓
Automated Tests
      ↓
Browser QA
      ↓
Code Review
      ↓
Deploy
      ↓
Real User Validation
```

------------------------------------------------------------------------

# 42. AI Tool Responsibilities

## ChatGPT

Use for:

-   Product strategy
-   Requirements
-   Product architecture
-   Prioritization
-   UX reasoning
-   Research
-   Decision support

## Claude

Use for:

-   Architecture critique
-   Specification review
-   Complex reasoning
-   Code review
-   Edge cases
-   Engineering planning

## Codex

Use for:

-   Repository implementation
-   Feature coding
-   Refactoring
-   Tests
-   Migrations
-   Debugging

## Antigravity

Use for:

-   Autonomous implementation tasks
-   Browser testing
-   End-to-end validation
-   Visual QA
-   Repetitive engineering workflows

## Figma

Use for:

-   UI design
-   Design system
-   Responsive layouts
-   Prototypes
-   Developer handoff

No AI tool should be allowed to redefine product scope without an
explicit product decision.

------------------------------------------------------------------------

# 43. Recommended Build Loop

For every major feature:

``` text
1. Define requirement
2. Define acceptance criteria
3. Design in Figma
4. Review architecture
5. Implement with Codex
6. Test
7. Run browser QA
8. Review implementation
9. Fix issues
10. Merge
```

Do not ask an AI:

> "Build the whole startup."

Break the product into vertical slices.

------------------------------------------------------------------------

# 44. Vertical Slice Example

Instead of:

``` text
Build authentication.
```

Build:

``` text
Signup
 ↓
Profile creation
 ↓
Database persistence
 ↓
Dashboard
 ↓
Logout
 ↓
Protected route
```

Then test the complete slice.

------------------------------------------------------------------------

# 45. Testing Strategy

## Unit Tests

Use for:

-   Validation
-   Utility functions
-   Matching calculations
-   State transitions

## Integration Tests

Use for:

-   Database operations
-   Server actions
-   AI gateway
-   Permissions

## E2E Tests

Use for:

-   Signup
-   Create project
-   Copilot
-   Team invitation
-   Task flow
-   Submission review

------------------------------------------------------------------------

# 46. AI Testing

AI features require deterministic validation around nondeterministic
model behavior.

Test:

-   Output schema
-   Required fields
-   Safety constraints
-   Permission boundaries
-   Hallucination-sensitive cases
-   Failure handling

Do not test AI only by checking whether the prose "sounds good."

------------------------------------------------------------------------

# 47. Security Priorities

V1 must protect:

-   Authentication
-   Project isolation
-   Team permissions
-   API secrets
-   Uploaded files
-   AI provider credentials
-   User data

Priority:

``` text
Database RLS
+
Server-side authorization
+
Input validation
+
Secret management
+
Safe file access
```

------------------------------------------------------------------------

# 48. Performance Priorities

Prioritize:

1.  Fast navigation
2.  Fast project loading
3.  Responsive interactions
4.  Clear AI loading states
5.  Efficient database queries

AI generation latency should be communicated clearly rather than hidden
behind an unresponsive interface.

------------------------------------------------------------------------

# 49. Deployment Architecture

Recommended:

``` text
GitHub
   ↓
Vercel
   ↓
Next.js Application
   │
   ├── Supabase
   │     ├── PostgreSQL
   │     ├── Auth
   │     └── Storage
   │
   └── AI Provider(s)
```

Preview deployments should be used for feature validation.

------------------------------------------------------------------------

# 50. Production Readiness Checklist

Before public V1:

### Product

-   [ ] Core journey works
-   [ ] Empty states exist
-   [ ] Error states exist
-   [ ] Responsive layouts work

### Database

-   [ ] Migrations versioned
-   [ ] RLS enabled
-   [ ] Relationships validated
-   [ ] Backups/recovery strategy understood

### Authentication

-   [ ] Signup works
-   [ ] Login works
-   [ ] Logout works
-   [ ] Protected routes work

### AI

-   [ ] Structured outputs validated
-   [ ] Provider keys secured
-   [ ] Cost tracking enabled
-   [ ] Failure handling implemented
-   [ ] AI permissions tested

### Testing

-   [ ] Unit tests
-   [ ] Integration tests
-   [ ] E2E critical-path tests
-   [ ] Browser QA

### Monitoring

-   [ ] Error monitoring
-   [ ] Analytics
-   [ ] AI usage tracking

------------------------------------------------------------------------

# 51. What Not to Build Yet

Do not add infrastructure merely because it sounds scalable.

Avoid initially:

-   Kubernetes
-   Microservices
-   Dedicated AI orchestration platform
-   Separate search cluster
-   Dedicated vector database
-   Event-driven distributed architecture
-   Custom model hosting
-   Native mobile backend
-   Complex message queues

A modular monolith is sufficient for V1.

------------------------------------------------------------------------

# 52. Recommended Architecture Style

HackLoop V1 should use a:

**Modular monolith**

Meaning:

``` text
One application
+
Clear internal modules
+
One primary database
+
External services where useful
```

This gives startup-level speed without creating unnecessary
distributed-system complexity.

------------------------------------------------------------------------

# 53. Module Boundaries

Suggested modules:

``` text
auth
profiles
hackathons
projects
teams
tasks
submissions
ai
notifications
analytics
```

Each module should have clear responsibilities.

------------------------------------------------------------------------

# 54. AI as a Separate Module

The AI module should own:

``` text
agents
context
prompts
schemas
provider adapters
generation logging
AI validation
```

Product modules should request AI capabilities without knowing
model-provider details.

Example:

``` text
projects module
      ↓
ai.generateProjectDefinition()
      ↓
AI module
      ↓
selected provider
```

------------------------------------------------------------------------

# 55. External Service Principle

Use external services for infrastructure that does not create HackLoop's
unique product value.

Examples:

-   Authentication
-   Database
-   Hosting
-   Monitoring
-   Analytics
-   AI model inference

HackLoop's product value should remain in:

-   Workflow
-   Context
-   Project intelligence
-   Team formation
-   Submission readiness

------------------------------------------------------------------------

# 56. Architecture Decision Records

For important technical decisions, maintain lightweight ADRs.

Examples:

``` text
docs/adr/
├── 001-nextjs.md
├── 002-supabase.md
├── 003-ai-provider-abstraction.md
├── 004-modular-monolith.md
└── 005-project-context.md
```

Do not create ADRs for trivial decisions.

------------------------------------------------------------------------

# 57. Technical Decision Principles

When choosing technology:

1.  Prefer boring technology that works.
2.  Prefer managed infrastructure for V1.
3.  Minimize operational overhead.
4.  Keep providers replaceable.
5.  Keep product logic independent of AI models.
6.  Optimize for iteration speed.
7.  Avoid premature scaling.
8.  Protect user/project data by default.

------------------------------------------------------------------------

# 58. Definition of Technical Success

HackLoop's V1 architecture is successful if:

-   A small team can develop quickly.
-   AI features can evolve without rewriting the app.
-   Project data remains structured and reliable.
-   User/project permissions are secure.
-   New AI agents can be added without major architectural changes.
-   The application can deploy through a simple GitHub → Vercel
    workflow.
-   The architecture can support real users before requiring major
    infrastructure changes.

------------------------------------------------------------------------

# 59. Final Architecture

The intended V1 system is:

``` text
                         HACKLOOP
                            │
                    ┌───────┴───────┐
                    │   Next.js     │
                    │  Application  │
                    └───────┬───────┘
                            │
          ┌─────────────────┼─────────────────┐
          ↓                 ↓                 ↓
     Product Modules     AI Module       Analytics
          │                 │
          ↓                 ↓
     ┌──────────┐      ┌────────────┐
     │ Supabase │      │ AI Gateway │
     │          │      └─────┬──────┘
     │ Postgres │            │
     │ Auth     │       ┌────┴────┐
     │ Storage  │       ↓         ↓
     └──────────┘    Provider A Provider B
```

------------------------------------------------------------------------

# 60. Final Technical Principle

**Keep HackLoop technically simple, but make its product context
sophisticated.**

Do not build a complicated infrastructure system to compensate for an
unclear product.

V1 should be:

``` text
Next.js
+
Supabase
+
AI Gateway
+
External AI Models
+
Vercel
+
GitHub
```

with strong:

``` text
Product workflow
+
Structured data
+
AI context
+
Permissions
+
Validation
```

That is enough to build and validate the first real version of HackLoop.
