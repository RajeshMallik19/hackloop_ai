# HackLoop --- Product Requirements Document

Version: 1.0\
Status: Product Definition\
Scope: HackLoop V1

------------------------------------------------------------------------

## 1. Purpose

This document converts the HackLoop product vision and user flows into
concrete product requirements.

It defines:

-   What V1 must do
-   What each major feature is responsible for
-   Inputs and outputs
-   User states
-   Permissions
-   Acceptance criteria
-   Important edge cases
-   Explicit V1 exclusions

This is a product specification, not an implementation guide.

Engineering decisions should be made later using this document together
with `TECH_ARCHITECTURE.md`.

------------------------------------------------------------------------

# 2. Product Objective

HackLoop helps hackathon participants move from:

**Hackathon opportunity → idea → team → project → build →
submission-ready work**

The V1 product must make this journey possible without requiring users
to assemble several disconnected tools themselves.

------------------------------------------------------------------------

# 3. V1 User Roles

## 3.1 Participant

A registered HackLoop user.

Can:

-   Create and edit their profile
-   Discover hackathons
-   Save hackathons
-   Create projects
-   Use AI Copilot
-   Invite teammates
-   Join projects
-   Manage project tasks
-   Use AI project assistance
-   Run submission reviews
-   Manage their own account

------------------------------------------------------------------------

## 3.2 Team Member

A participant who belongs to a project.

Can:

-   View permitted project information
-   Manage assigned tasks
-   Contribute project content
-   View team members
-   Participate in project AI interactions where permitted

A team member should not automatically have permission to change
sensitive project settings.

------------------------------------------------------------------------

## 3.3 Project Owner

The participant who creates the project.

Can additionally:

-   Edit project settings
-   Manage team invitations
-   Remove members
-   Configure project information
-   Manage submission information
-   Run final submission preparation

------------------------------------------------------------------------

## 3.4 Admin

Platform-level role.

Can:

-   Manage hackathon data
-   Moderate content
-   Manage users where necessary
-   Review platform activity
-   Maintain platform configuration

Admin functionality is intentionally limited in V1.

------------------------------------------------------------------------

# 4. Authentication Requirements

## AUTH-001 --- Registration

Users must be able to create an account using:

-   Name
-   Email
-   Password

### Acceptance criteria

-   Valid users can create an account.
-   Duplicate email registration is prevented.
-   Invalid credentials produce understandable errors.
-   Successful registration leads to profile setup.

------------------------------------------------------------------------

## AUTH-002 --- Login

Users must be able to log in with their account credentials.

### Acceptance criteria

-   Valid credentials open the authenticated experience.
-   Invalid credentials show an understandable error.
-   Existing projects remain accessible after login.

------------------------------------------------------------------------

## AUTH-003 --- Session Persistence

Authenticated users should remain logged in across normal navigation and
browser refreshes.

------------------------------------------------------------------------

# 5. Profile Requirements

## PROFILE-001 --- Profile Creation

Users must be able to create a basic profile.

Required:

-   Name
-   Skills
-   Interests

Optional:

-   Bio
-   Technologies
-   Experience
-   Availability
-   GitHub
-   Portfolio
-   LinkedIn
-   Profile image

------------------------------------------------------------------------

## PROFILE-002 --- Skills

Users must be able to add and remove skills.

Skills should use standardized values where possible so that matching
does not depend entirely on free-text variations.

Example:

Instead of:

-   React.js
-   React JS
-   ReactJS

The system should normalize these into a common skill representation.

------------------------------------------------------------------------

## PROFILE-003 --- Availability

Users can specify when they are generally available for hackathons.

Example values:

-   Weekdays
-   Weekends
-   Evenings
-   Full-time

------------------------------------------------------------------------

## PROFILE-004 --- Profile Editing

Users must be able to edit their profile after onboarding.

------------------------------------------------------------------------

# 6. Hackathon Discovery Requirements

## HACK-001 --- Browse Hackathons

Users must be able to browse available hackathons.

Each hackathon should expose at minimum:

-   Name
-   Organizer
-   Description
-   Deadline
-   Format
-   Location where applicable
-   Prize information where available
-   Eligibility
-   Technologies/themes
-   Submission requirements

------------------------------------------------------------------------

## HACK-002 --- Search

Users must be able to search hackathons using text.

Search should consider relevant fields such as:

-   Hackathon name
-   Organizer
-   Theme
-   Technology
-   Category

------------------------------------------------------------------------

## HACK-003 --- Filters

V1 should support filters for:

-   Category
-   Technology
-   Online/offline
-   Location
-   Deadline
-   Eligibility

Additional filters can be added later.

------------------------------------------------------------------------

## HACK-004 --- Save Hackathon

Users can save a hackathon for later.

Saved hackathons should appear in an appropriate dashboard area.

------------------------------------------------------------------------

## HACK-005 --- Hackathon Details

Users must be able to open a complete hackathon details page.

The page should clearly expose:

-   Overview
-   Theme/problem
-   Tracks
-   Rules
-   Eligibility
-   Timeline
-   Prizes
-   Submission requirements

Primary CTA:

**Start Project**

------------------------------------------------------------------------

# 7. Project Requirements

## PROJECT-001 --- Create Project

Users must be able to create a project associated with a hackathon.

Minimum project fields:

-   Project name
-   Hackathon
-   Description/status

The project can begin as a draft.

------------------------------------------------------------------------

## PROJECT-002 --- Idea Source

When creating a project, users should choose:

-   I already have an idea
-   Help me develop an idea

Both paths must eventually create the same structured project object.

------------------------------------------------------------------------

## PROJECT-003 --- Project Structure

A project should support:

-   Problem
-   Target users
-   Solution
-   Features
-   Differentiator
-   Technical approach
-   Technology stack
-   MVP
-   Future scope
-   Pitch
-   Team
-   Tasks
-   Links
-   Files
-   Submission information

------------------------------------------------------------------------

## PROJECT-004 --- Project Editing

Users must be able to edit AI-generated or manually created project
content.

AI output must never lock the user into an AI-generated answer.

------------------------------------------------------------------------

# 8. AI Hackathon Copilot Requirements

## AI-001 --- Idea Input

The user can provide an idea in natural language.

Example:

> "I want to build an AI tool for helping small farmers detect crop
> diseases."

------------------------------------------------------------------------

## AI-002 --- Structured Generation

The Copilot should help produce:

-   Problem
-   Target users
-   Solution
-   Core features
-   Differentiator
-   Technical approach
-   Technology stack
-   MVP
-   Future scope
-   Pitch

------------------------------------------------------------------------

## AI-003 --- Clarifying Questions

The Copilot may ask questions when required to improve the project
definition.

Questions should be relevant to the current project.

------------------------------------------------------------------------

## AI-004 --- Project Context

The Copilot should have access to relevant structured context such as:

-   Selected hackathon
-   Rules
-   Tracks
-   User's profile
-   Existing project information

------------------------------------------------------------------------

## AI-005 --- Save AI Output

Accepted AI output must be convertible into editable project fields.

The product must not require the user to manually copy information from
a chat into the project.

------------------------------------------------------------------------

## AI-006 --- Regeneration

Users should be able to request another version of an AI-generated
section.

Examples:

-   Make the solution simpler
-   Give me a more technically ambitious approach
-   Reduce the MVP
-   Suggest alternative differentiators

------------------------------------------------------------------------

## AI-007 --- User Control

Users must be able to:

-   Accept
-   Edit
-   Reject
-   Regenerate

AI-generated suggestions.

------------------------------------------------------------------------

# 9. Team Matching Requirements

## TEAM-001 --- Skill Requirement Detection

HackLoop should identify likely skills required by the project.

Example:

``` text
Project:
AI crop disease detection

Potential requirements:
- Python
- Machine Learning
- Computer Vision
- Backend
- Frontend
```

The system should allow users to edit these requirements.

------------------------------------------------------------------------

## TEAM-002 --- Skill Gap Detection

The system compares:

**Required project skills**

against

**Current team skills**

and identifies gaps.

------------------------------------------------------------------------

## TEAM-003 --- Candidate Matching

The system should identify potentially relevant participants based on
available profile information.

Matching signals may include:

-   Skills
-   Interests
-   Technologies
-   Experience
-   Availability

------------------------------------------------------------------------

## TEAM-004 --- Explainable Matching

Every recommendation should have a reason.

Example:

> Recommended because this participant has Python and Computer Vision
> experience, which match two current project requirements.

------------------------------------------------------------------------

## TEAM-005 --- Invitation

Project owners can invite participants.

Invitation states:

``` text
Pending
Accepted
Declined
Cancelled
```

------------------------------------------------------------------------

## TEAM-006 --- Membership

When an invitation is accepted, the participant becomes a project
member.

------------------------------------------------------------------------

# 10. Project Workspace Requirements

## WORKSPACE-001 --- Project Overview

The workspace must show:

-   Project name
-   Hackathon
-   Current project state
-   Problem
-   Solution
-   Team
-   Progress
-   Next action

------------------------------------------------------------------------

## WORKSPACE-002 --- Project Navigation

V1 navigation should include:

``` text
Overview
Team
Problem
Solution
Features
Tasks
Research
Files
Links
GitHub
Submission
AI
```

Not every section needs to be equally complex in V1.

------------------------------------------------------------------------

## WORKSPACE-003 --- Tasks

Users can create tasks.

Task fields:

-   Title
-   Description
-   Owner
-   Status
-   Priority
-   Due date

Suggested statuses:

``` text
Todo
In Progress
Blocked
Done
```

------------------------------------------------------------------------

## WORKSPACE-004 --- Task Assignment

Project members can be assigned tasks according to their permissions.

------------------------------------------------------------------------

## WORKSPACE-005 --- Project Progress

Project progress should be calculated from meaningful project activity
rather than arbitrary page completion.

V1 may use task completion as the primary measurable progress signal.

------------------------------------------------------------------------

# 11. AI Project Assistance Requirements

## AI-010 --- Workspace Context

AI assistance inside a project must understand:

-   Project definition
-   Hackathon
-   Team
-   Tasks
-   Current state
-   Relevant project documents

------------------------------------------------------------------------

## AI-011 --- Planning Assistance

Users may ask:

-   What should we build next?
-   What tasks are missing?
-   What should the MVP contain?
-   Which task is blocking us?

------------------------------------------------------------------------

## AI-012 --- Project Critique

Users may ask the AI to identify:

-   Unnecessary features
-   Missing functionality
-   Weak assumptions
-   Technical risks
-   Unclear problem statements

AI suggestions should remain editable recommendations.

------------------------------------------------------------------------

# 12. Submission Requirements

## SUB-001 --- Submission Information

Projects must support:

-   Final project description
-   Demo link
-   Repository link
-   Documentation links
-   Required files
-   Team information

------------------------------------------------------------------------

## SUB-002 --- Submission Checklist

HackLoop should generate a checklist based on known hackathon
requirements.

------------------------------------------------------------------------

## SUB-003 --- Deadline Awareness

The project should clearly communicate the relevant submission deadline
when known.

------------------------------------------------------------------------

# 13. AI Submission Reviewer Requirements

## REVIEW-001 --- Requirement Comparison

The reviewer compares:

**Hackathon requirements**

against

**Project/submission information**

------------------------------------------------------------------------

## REVIEW-002 --- Structured Review

Each finding should contain:

``` text
Requirement
Evidence
Gap
Recommendation
Suggested Improvement
```

------------------------------------------------------------------------

## REVIEW-003 --- No Unsupported Scoring

V1 should not present an arbitrary numerical "chance of winning" score.

The reviewer should focus on evidence and actionable gaps.

------------------------------------------------------------------------

## REVIEW-004 --- Review History

Previous reviews should be retained where practical so users can
understand what changed.

------------------------------------------------------------------------

## REVIEW-005 --- Regeneration

Users can run another review after making changes.

------------------------------------------------------------------------

# 14. Next Best Action Requirements

## NBA-001 --- Contextual Action

The product should surface the most relevant next action for the
project.

Examples:

``` text
No project
→ Find a hackathon

Project has no definition
→ Define your idea

Project missing skills
→ Find teammates

No tasks
→ Create MVP tasks

Project building
→ Continue assigned tasks

Submission approaching
→ Run submission review

Review has gaps
→ Fix identified gaps
```

------------------------------------------------------------------------

## NBA-002 --- Avoid Generic Recommendations

Recommendations should be based on actual project state.

The system should not repeatedly show generic AI suggestions.

------------------------------------------------------------------------

# 15. Dashboard Requirements

The dashboard should prioritize active work.

Required sections:

1.  Continue Project
2.  Recommended Hackathons
3.  Teams
4.  Next Best Action
5.  Relevant notifications

Optional V1 elements:

-   Recently saved hackathons
-   Recent AI activity

------------------------------------------------------------------------

# 16. Notifications Requirements

V1 notifications should cover meaningful events.

Examples:

-   Team invitation
-   Invitation accepted
-   Task assignment
-   Task deadline
-   Hackathon deadline approaching
-   Submission review completed

Users should not receive excessive notifications.

------------------------------------------------------------------------

# 17. Permissions

## Participant

Can:

-   Manage own profile
-   Create projects
-   Join projects
-   Work on permitted projects

## Project Owner

Can additionally:

-   Manage project settings
-   Invite/remove members
-   Manage submission information
-   Control project-level configuration

## Team Member

Can:

-   View project
-   Work on assigned/permitted content
-   Manage tasks they are allowed to edit

## Admin

Can manage platform-level content and operations.

------------------------------------------------------------------------

# 18. Important Project States

A project should support:

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

State transitions should be intentional.

Example:

``` text
draft
→ defined
→ team_forming
→ planning
→ building
→ reviewing
→ submission_ready
→ submitted
```

Users may need to move backward when they discover problems.

For example:

``` text
reviewing
→ building
```

is valid.

------------------------------------------------------------------------

# 19. Error States

Every important operation needs understandable failure handling.

Examples:

### AI unavailable

> AI assistance is temporarily unavailable. Your existing project data
> is safe.

### Invitation failed

> We couldn't send this invitation. Try again.

### Hackathon data unavailable

> Hackathon information could not be loaded. Try again later.

### Unauthorized action

> You don't have permission to perform this action.

Errors should explain what happened and what the user can do next.

------------------------------------------------------------------------

# 20. Data Safety Principles

AI should not silently modify important user data.

For significant changes:

-   Show generated content
-   Require user acceptance where appropriate
-   Preserve user-edited content
-   Avoid destructive overwrites
-   Keep important history where useful

------------------------------------------------------------------------

# 21. V1 Acceptance Criteria

HackLoop V1 is functionally viable when a test participant can complete
this sequence:

``` text
Create Account
    ↓
Create Profile
    ↓
Find Hackathon
    ↓
Create Project
    ↓
Use AI Copilot
    ↓
Save Project Definition
    ↓
Identify Skill Gaps
    ↓
Invite Teammate
    ↓
Create Tasks
    ↓
Track Build Progress
    ↓
Run Submission Review
    ↓
Fix Identified Gaps
    ↓
Reach Submission Ready
```

A broken step in this critical path is a V1 blocker.

------------------------------------------------------------------------

# 22. V1 Quality Bar

A feature should not be considered complete merely because it
technically works.

For each major workflow:

### Functional

The action works.

### Usable

A first-time user can understand what to do.

### Recoverable

Errors do not destroy progress.

### Consistent

The feature follows HackLoop's interaction patterns.

### AI-aware

AI suggestions are contextual rather than generic.

### User-controlled

The user can edit or reject AI output.

------------------------------------------------------------------------

# 23. V1 Non-Functional Product Requirements

HackLoop should aim for:

-   Responsive web experience
-   Mobile-friendly layouts
-   Accessible core interactions
-   Fast initial navigation
-   Clear loading states
-   Clear AI generation states
-   Reliable data persistence
-   Secure authentication
-   Permission-aware project access

Exact technical targets belong in the technical architecture document.

------------------------------------------------------------------------

# 24. Explicit V1 Non-Requirements

Do not expand V1 into:

-   Native mobile apps
-   Social media feed
-   Full Discord replacement
-   Full project-management replacement
-   Custom foundation model
-   AI coding agent
-   Judge marketplace
-   Organizer marketplace
-   Advanced gamification
-   Complex leaderboard system
-   Full GitHub automation
-   AI Judge Simulator
-   AI Demo Coach
-   AI Mentor
-   Large external hackathon integration network
-   Enterprise analytics suite

These can be evaluated after V1 validation.

------------------------------------------------------------------------

# 25. Product Decision Rules

When deciding whether to add a feature, ask:

### Rule 1

Does it help a participant reach a submission-ready project?

### Rule 2

Does it strengthen the core workflow?

### Rule 3

Can the feature be validated with real users?

### Rule 4

Does it create unnecessary complexity?

### Rule 5

Can an existing external service solve the problem instead?

If the answer to the first two is no, the feature should normally remain
outside V1.

------------------------------------------------------------------------

# 26. Definition of Done

A V1 feature is done when:

-   The intended user flow works.
-   The required data is persisted.
-   Permissions are correct.
-   Empty states exist.
-   Loading states exist.
-   Error states exist.
-   AI output is editable where applicable.
-   The feature works responsively.
-   The primary interaction is understandable without explanation.
-   The feature does not break the core project journey.

------------------------------------------------------------------------

# 27. Relationship to Other Product Documents

This document sits between the product vision and implementation.

``` text
PRODUCT_BLUEPRINT.md
        ↓
USER_FLOWS.md
        ↓
PRODUCT_REQUIREMENTS.md
        ↓
AI_AGENTS.md
        ↓
DATA_MODEL.md
        ↓
TECH_ARCHITECTURE.md
        ↓
DESIGN_SYSTEM.md
        ↓
MVP_SCOPE.md
        ↓
BUILD_PLAN.md
```

The next major document should define the AI agents themselves.

That document should answer:

-   What each AI agent receives
-   What it produces
-   What context it can access
-   What it is allowed to change
-   What it must never do
-   When it should be invoked
-   How agents share context
-   Which model/tool should handle each AI responsibility

------------------------------------------------------------------------

# 28. Product Principle

HackLoop should optimize for **progress**, not AI activity.

The product should never measure success by:

-   Number of AI messages
-   Number of prompts
-   Number of generated ideas

The meaningful outcome is:

**How many users move from a hackathon opportunity to a genuinely
submission-ready project?**
