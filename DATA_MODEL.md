# HackLoop --- Data Model

Version: 1.0\
Status: Product Architecture\
Scope: HackLoop V1

------------------------------------------------------------------------

## 1. Purpose

This document defines the core data model for HackLoop V1.

The purpose is to establish:

-   What information HackLoop stores
-   How entities relate to each other
-   What becomes the source of truth
-   What information AI agents consume
-   Which data belongs to users, projects, hackathons, teams, and
    submissions

This is a conceptual data model.

Exact SQL types, indexes, migrations, RLS policies, and implementation
details belong in `TECH_ARCHITECTURE.md`.

------------------------------------------------------------------------

# 2. Core Principle

The **Project** is the central object in HackLoop.

Most product activity eventually connects to a project:

``` text
User
  ↓
Profile
  ↓
Project
  ├── Hackathon
  ├── Team
  ├── Skills
  ├── Tasks
  ├── Documents
  ├── Links
  ├── AI Sessions
  └── Submission
```

The project is also the primary context boundary for AI.

------------------------------------------------------------------------

# 3. Entity Overview

V1 entities:

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

------------------------------------------------------------------------

# 4. User

## Purpose

Represents a HackLoop account.

### Core fields

``` text
id
email
created_at
updated_at
last_login_at
status
```

### Status

Suggested values:

``` text
active
suspended
deleted
```

Authentication credentials should be handled by the authentication
provider rather than stored directly in the application database.

------------------------------------------------------------------------

# 5. Profile

## Purpose

Stores participant information used throughout HackLoop.

### Fields

``` text
id
user_id
display_name
avatar_url
bio
experience_level
availability
github_url
portfolio_url
linkedin_url
created_at
updated_at
```

The profile belongs to exactly one user.

``` text
User 1 ───── 1 Profile
```

------------------------------------------------------------------------

# 6. Skill

## Purpose

Provides standardized skills for matching and project requirements.

### Fields

``` text
id
name
category
normalized_name
created_at
```

Examples:

``` text
React
Python
Machine Learning
UI/UX Design
Backend Development
Computer Vision
Cloud
Data Analytics
```

Skills should be normalized.

For example:

``` text
React.js
ReactJS
React JS
```

should map to one canonical skill where appropriate.

------------------------------------------------------------------------

# 7. Profile Skill

## Purpose

Connects users to their skills.

### Fields

``` text
id
profile_id
skill_id
proficiency
years_experience
created_at
```

### Relationship

``` text
Profile
   │
   ├── Profile Skill
   │        │
   │        └── Skill
   │
   └── Profile Skill
```

This creates a many-to-many relationship:

``` text
Profiles ↔ Skills
```

------------------------------------------------------------------------

# 8. Hackathon

## Purpose

Represents a hackathon available on HackLoop.

### Fields

``` text
id
name
organizer_name
description
theme
format
location
registration_url
submission_url
registration_deadline
submission_deadline
prize_summary
eligibility_summary
status
source
created_at
updated_at
```

### Status

Suggested:

``` text
draft
published
closed
archived
```

------------------------------------------------------------------------

# 9. Hackathon Track

## Purpose

Represents a specific challenge or category within a hackathon.

### Fields

``` text
id
hackathon_id
name
description
requirements
created_at
updated_at
```

Relationship:

``` text
Hackathon 1 ───── N Tracks
```

------------------------------------------------------------------------

# 10. Hackathon Rule

## Purpose

Stores structured or extracted hackathon requirements.

### Fields

``` text
id
hackathon_id
title
description
rule_type
source_reference
is_required
created_at
updated_at
```

Examples:

``` text
Eligibility
Submission Format
Technology Requirement
Team Size
Theme Requirement
Prize Track Requirement
Documentation Requirement
```

------------------------------------------------------------------------

# 11. Project

## Purpose

The central entity in HackLoop.

A project represents a participant's hackathon project from idea through
submission.

### Fields

``` text
id
owner_id
hackathon_id
track_id

name
slug

problem
target_users
solution
differentiator

features
technical_approach
technology_stack

mvp
future_scope
pitch

status
progress

created_at
updated_at
```

------------------------------------------------------------------------

# 12. Project Status

Suggested lifecycle:

``` text
draft
defined
team_forming
planning
building
reviewing
submission_ready
submitted
archived
```

Valid transitions may include:

``` text
draft
  ↓
defined
  ↓
team_forming
  ↓
planning
  ↓
building
  ↓
reviewing
  ↓
submission_ready
  ↓
submitted
```

Backward transitions should also be possible when new problems are
discovered.

Example:

``` text
reviewing → building
```

------------------------------------------------------------------------

# 13. Project Owner

Every project has one primary owner.

``` text
Project.owner_id → User.id
```

The owner has elevated project permissions.

------------------------------------------------------------------------

# 14. Project Member

## Purpose

Connects users to projects.

### Fields

``` text
id
project_id
user_id
role
status
joined_at
created_at
```

### Roles

``` text
owner
member
```

### Membership status

``` text
invited
active
declined
removed
```

Relationship:

``` text
Users ↔ Projects
```

through:

``` text
Project Members
```

------------------------------------------------------------------------

# 15. Project Skill

## Purpose

Represents skills required by a project.

### Fields

``` text
id
project_id
skill_id
importance
required_count
created_at
```

### Importance

Suggested:

``` text
critical
important
nice_to_have
```

Example:

``` text
Project:
CropVision

Required Skills:

Computer Vision → critical
Python → critical
Backend → important
UI/UX → important
```

------------------------------------------------------------------------

# 16. Skill Gap

Skill gaps do not necessarily need their own table in V1.

They can be derived:

``` text
Required Project Skills
-
Current Team Skills
=
Skill Gaps
```

This keeps the data model simpler.

A dedicated table can be introduced later if the matching system
requires historical or manually managed skill-gap data.

------------------------------------------------------------------------

# 17. Project Task

## Purpose

Represents work that must be completed.

### Fields

``` text
id
project_id
title
description
assignee_id
status
priority
due_date
created_by
created_at
updated_at
completed_at
```

### Status

``` text
todo
in_progress
blocked
done
```

### Priority

``` text
low
medium
high
critical
```

------------------------------------------------------------------------

# 18. Task Relationships

A task belongs to one project.

An assignee is a project member.

``` text
Project
   ↓
Task
   ↓
Project Member
   ↓
User
```

This prevents assigning work to unrelated users.

------------------------------------------------------------------------

# 19. Project Document

## Purpose

Represents project-related files or documents.

### Fields

``` text
id
project_id
uploaded_by
name
storage_path
file_type
size
created_at
updated_at
```

Potential future fields:

``` text
version
description
```

------------------------------------------------------------------------

# 20. Project Link

## Purpose

Stores useful external links.

### Fields

``` text
id
project_id
type
title
url
created_by
created_at
updated_at
```

### Types

``` text
github
demo
figma
documentation
deployment
video
other
```

------------------------------------------------------------------------

# 21. AI Session

## Purpose

Represents an AI interaction context.

### Fields

``` text
id
user_id
project_id
agent_type
title
created_at
updated_at
```

### Agent types

``` text
hackathon_copilot
team_matcher
project_assistant
submission_reviewer
```

An AI session can belong to a project.

Some pre-project Copilot sessions may temporarily exist without one.

------------------------------------------------------------------------

# 22. AI Generation

## Purpose

Stores individual AI-generated outputs.

### Fields

``` text
id
session_id
user_id
project_id
agent_type

input_context
output_content
structured_output

model_provider
model_name

status
latency_ms

input_tokens
output_tokens
estimated_cost

created_at
```

### Status

``` text
pending
completed
failed
cancelled
```

------------------------------------------------------------------------

# 23. AI Output Acceptance

AI-generated content should be distinguishable from accepted project
data.

Conceptually:

``` text
AI Generation
     ↓
User Review
     ↓
Accept / Edit / Reject
     ↓
Project Data
```

The AI generation record preserves the generation history.

The project remains the source of truth.

------------------------------------------------------------------------

# 24. Submission

## Purpose

Represents the project's intended hackathon submission.

### Fields

``` text
id
project_id

description
demo_url
repository_url
documentation_url

status
submitted_at

created_at
updated_at
```

### Status

``` text
draft
ready
submitted
```

V1 does not require HackLoop to submit directly to every external
hackathon platform.

------------------------------------------------------------------------

# 25. Submission Review

## Purpose

Stores AI-generated submission review results.

### Fields

``` text
id
submission_id
review_version
overall_status
created_at
```

A review should contain individual findings.

------------------------------------------------------------------------

# 26. Submission Review Finding

Conceptually, each review contains:

``` text
Requirement
Evidence
Status
Potential Gap
Recommendation
Suggested Improvement
```

Suggested status:

``` text
addressed
partially_addressed
missing
unclear
not_applicable
```

This may initially be stored as structured JSON inside the review.

A dedicated relational table can be introduced later if querying
individual findings becomes important.

------------------------------------------------------------------------

# 27. Notification

## Purpose

Represents meaningful user notifications.

### Fields

``` text
id
user_id
type
title
message
related_entity_type
related_entity_id
read_at
created_at
```

### Types

``` text
team_invitation
invitation_accepted
task_assigned
task_deadline
hackathon_deadline
review_completed
project_update
```

------------------------------------------------------------------------

# 28. Saved Hackathons

A user should be able to save hackathons.

Conceptually:

``` text
User ↔ Hackathon
```

through a saved-hackathon relationship.

Suggested entity:

``` text
saved_hackathons

id
user_id
hackathon_id
created_at
```

This should be added to the implementation schema even though it was not
part of the initial entity list.

------------------------------------------------------------------------

# 29. Team Invitation

Team invitations may initially be represented through `project_members`.

For a pending invitation:

``` text
project_members.status = invited
```

If the invitation workflow later requires richer data, create:

``` text
team_invitations

id
project_id
inviter_id
invitee_id
status
message
expires_at
created_at
responded_at
```

V1 can start simpler.

------------------------------------------------------------------------

# 30. Relationships Overview

``` text
USER
 │
 ├── PROFILE
 │     │
 │     └── PROFILE_SKILLS ─── SKILLS
 │
 ├── PROJECTS (owner)
 │
 ├── PROJECT_MEMBERS
 │
 ├── NOTIFICATIONS
 │
 └── AI_SESSIONS
              │
              └── AI_GENERATIONS


HACKATHON
 │
 ├── TRACKS
 ├── RULES
 ├── PROJECTS
 └── SAVED_HACKATHONS


PROJECT
 │
 ├── OWNER → USER
 ├── HACKATHON
 ├── TRACK
 ├── MEMBERS → USERS
 ├── SKILLS
 ├── TASKS
 ├── DOCUMENTS
 ├── LINKS
 ├── AI_SESSIONS
 └── SUBMISSION
              │
              └── REVIEWS
```

------------------------------------------------------------------------

# 31. Core Relationship Map

``` text
User
 │
 ├────────────── Profile
 │                    │
 │                    └──── Skills
 │
 ├────────────── Project Member
 │                    │
 │                    └──── Project
 │                              │
 │                              ├──── Hackathon
 │                              ├──── Track
 │                              ├──── Project Skills
 │                              ├──── Tasks
 │                              ├──── Documents
 │                              ├──── Links
 │                              ├──── AI Sessions
 │                              └──── Submission
 │                                         │
 │                                         └──── Review
 │
 └────────────── Notifications
```

------------------------------------------------------------------------

# 32. AI Context Assembly

When an AI agent runs, HackLoop should assemble only the context
required for that operation.

## Copilot

``` text
User Profile
+
Hackathon
+
Track
+
Rules
+
Existing Project
```

## Team Matcher

``` text
Project
+
Project Skills
+
Current Team
+
Candidate Profiles
```

## Project Assistant

``` text
Project
+
Team
+
Tasks
+
Deadline
+
Relevant Documents
```

## Submission Reviewer

``` text
Hackathon
+
Rules
+
Project
+
Submission
+
Relevant Documents
```

Avoid sending unrelated user data to the model.

------------------------------------------------------------------------

# 33. Source of Truth

Each type of information should have one primary source.

  Information          Source of Truth
  -------------------- -------------------------
  User identity        User/Auth
  Skills               Profile + Skills
  Hackathon rules      Hackathon data
  Project definition   Project
  Team membership      Project Members
  Required skills      Project Skills
  Work                 Project Tasks
  Files                Project Documents
  External resources   Project Links
  AI history           AI Sessions/Generations
  Submission           Submission
  Review               Submission Review

AI output is not the source of truth.

------------------------------------------------------------------------

# 34. Data Ownership

## User-owned

-   Profile
-   Personal links
-   Availability
-   Personal skills

## Project-owned

-   Project definition
-   Team membership
-   Skills required
-   Tasks
-   Documents
-   Links
-   Submission

## Platform-owned

-   Hackathon records
-   Hackathon rules
-   Skills taxonomy
-   System notifications
-   AI telemetry

------------------------------------------------------------------------

# 35. Deletion Principles

Deleting a user or project should be handled carefully.

Potentially destructive operations should not immediately destroy
valuable historical information.

Recommended approach:

-   Soft-delete where useful
-   Preserve submission/review history where required
-   Remove access before permanent deletion
-   Respect privacy requirements

Exact retention rules belong in the technical/security design.

------------------------------------------------------------------------

# 36. Data Validation Principles

The application should validate:

### User

Valid email and account state.

### Profile

Valid skill references.

### Project

Valid owner and hackathon.

### Project Member

User must exist and membership must belong to the project.

### Task

Assignee must belong to the project.

### Submission

Submission must belong to the project.

### Review

Review must belong to a submission.

------------------------------------------------------------------------

# 37. Preventing Orphaned Data

Important relationships should have explicit ownership.

Examples:

A task cannot exist without a project.

A submission cannot exist without a project.

A project member cannot exist without a project and user.

A review cannot exist without a submission.

This keeps the database consistent.

------------------------------------------------------------------------

# 38. Progress Model

V1 should avoid storing too many redundant progress values.

Primary progress can be derived from tasks:

``` text
completed_tasks / total_tasks
```

However, project state should remain explicitly stored because:

``` text
building
reviewing
submission_ready
```

cannot be reliably inferred from task percentage alone.

------------------------------------------------------------------------

# 39. Deadline Model

Hackathon deadlines should be stored explicitly.

At minimum:

``` text
registration_deadline
submission_deadline
```

Projects should reference the hackathon rather than copying the deadline
into the project.

This prevents duplicated deadline data.

------------------------------------------------------------------------

# 40. Future Scalability

The model should allow future expansion into:

-   Multiple hackathon sources
-   Organizer accounts
-   More advanced team matching
-   AI agent history
-   Project versioning
-   Collaboration
-   Project analytics
-   GitHub integrations
-   Advanced submissions
-   Judge feedback

V1 should not implement these simply because the data model could
support them.

------------------------------------------------------------------------

# 41. Recommended Initial Database Boundary

The first database implementation should focus on:

``` text
Users
Profiles
Skills
Hackathons
Tracks
Rules
Projects
Project Members
Project Skills
Tasks
AI Sessions
AI Generations
Submissions
Submission Reviews
Notifications
Saved Hackathons
```

Documents and advanced collaboration can be implemented incrementally.

------------------------------------------------------------------------

# 42. Data Model Design Rule

When deciding whether to create another entity, ask:

1.  Does it represent a distinct business concept?
2.  Does it need independent querying?
3.  Does it have its own lifecycle?
4.  Does it need independent permissions?
5.  Would storing it inside another object make the data difficult to
    maintain?

If the answer is mostly no, avoid creating another table.

------------------------------------------------------------------------

# 43. Final Architecture Principle

The HackLoop data model should make one thing possible:

``` text
One User
    ↓
One Hackathon
    ↓
One Project
    ↓
One Team
    ↓
One Build Context
    ↓
One Submission Context
```

AI should be able to reconstruct the user's current project state from
these connected entities.

That persistent context is one of the foundations of HackLoop's product
value.
