# HackLoop --- AI Agents Architecture

Version: 1.0\
Status: Product Definition\
Scope: HackLoop V1

------------------------------------------------------------------------

## 1. Purpose

This document defines HackLoop's AI layer.

The goal is not to create many AI features.

The goal is to create a small number of highly contextual AI
capabilities that work together across the user's hackathon journey.

V1 should begin with four core AI capabilities:

1.  Hackathon Copilot
2.  Team Matcher
3.  Project Assistant
4.  Submission Reviewer

The AI layer should behave as one connected intelligence system rather
than four unrelated chatbots.

------------------------------------------------------------------------

# 2. Core AI Principle

HackLoop should not be:

> A collection of AI chat windows.

HackLoop should be:

> A structured hackathon workflow with AI intelligence embedded at the
> right moments.

The AI should understand the user's:

-   Hackathon
-   Project
-   Team
-   Skills
-   Tasks
-   Requirements
-   Submission

The project context is the central source of truth.

------------------------------------------------------------------------

# 3. AI Context Model

All agents should operate from structured context.

``` text
User Profile
    ↓
Hackathon Context
    ↓
Project Context
    ↓
Team Context
    ↓
Build Context
    ↓
Submission Context
```

The AI should not rely only on previous chat messages.

------------------------------------------------------------------------

# 4. Agent Overview

  -----------------------------------------------------------------------
  Agent                   Primary Job             V1
  ----------------------- ----------------------- -----------------------
  Hackathon Copilot       Turn rough ideas into   Yes
                          structured projects     

  Team Matcher            Find people who fill    Yes
                          project skill gaps      

  Project Assistant       Help teams plan and     Yes
                          execute                 

  Submission Reviewer     Check project against   Yes
                          hackathon requirements  

  Project Manager         Autonomous planning and Later
                          coordination            

  Technical Mentor        Technical guidance      Later

  Judge Simulator         Simulated judging       Later

  Demo Coach              Demo preparation        Later

  Research Agent          Deep research           Later

  Architecture Reviewer   Technical architecture  Later
                          review                  

  Pitch Coach             Pitch refinement        Later
  -----------------------------------------------------------------------

V1 intentionally limits the number of agents.

------------------------------------------------------------------------

# 5. AI-001 --- Hackathon Copilot

## Purpose

Turn a rough idea into a structured, editable project definition.

------------------------------------------------------------------------

## Inputs

The Copilot can receive:

### User input

-   Free-form idea
-   Problem statement
-   Notes
-   Existing solution
-   User questions

### Hackathon context

-   Name
-   Description
-   Theme
-   Tracks
-   Rules
-   Eligibility
-   Submission requirements

### User context

-   Skills
-   Interests
-   Technologies
-   Experience

------------------------------------------------------------------------

## Output

The Copilot should generate structured project information:

``` text
Problem
Target Users
Solution
Core Features
Differentiator
Technical Approach
Technology Stack
MVP
Future Scope
Pitch
```

------------------------------------------------------------------------

## Behavior

The Copilot should:

-   Ask clarifying questions when useful.
-   Identify ambiguous assumptions.
-   Suggest alternatives.
-   Reduce unnecessarily large MVPs.
-   Connect ideas to hackathon requirements.
-   Explain important recommendations.
-   Keep output editable.

------------------------------------------------------------------------

## Example

User:

> I want to build an AI system that helps farmers detect crop disease.

Copilot should not immediately dump a 2,000-word proposal.

It should first determine important missing information.

Example:

> Who is the primary user: individual farmers, agricultural officers, or
> farm-management companies?

After clarification, it can build the structured project.

------------------------------------------------------------------------

## Permissions

The Copilot may:

-   Generate suggestions
-   Propose project content
-   Update fields after user approval

The Copilot must not:

-   Delete user content silently
-   Submit a project
-   Invite users
-   Change permissions
-   Claim requirements are satisfied without evidence

------------------------------------------------------------------------

# 6. AI-002 --- Team Matcher

## Purpose

Identify the skills a project needs and help find suitable teammates.

------------------------------------------------------------------------

## Inputs

### Project

-   Problem
-   Solution
-   Features
-   Technical approach
-   Technology stack
-   MVP

### Existing team

-   Skills
-   Experience
-   Responsibilities

### Candidate profiles

-   Skills
-   Interests
-   Experience
-   Technologies
-   Availability

------------------------------------------------------------------------

## Processing

The Team Matcher should determine:

``` text
Required Skills
      ↓
Current Team Skills
      ↓
Skill Gaps
      ↓
Candidate Profiles
      ↓
Potential Matches
```

------------------------------------------------------------------------

## Output

The matcher should provide:

-   Required project skills
-   Current team coverage
-   Skill gaps
-   Recommended candidates
-   Reason for each recommendation

------------------------------------------------------------------------

## Example

``` text
Project requires:

Python
Computer Vision
Backend
Frontend

Current team:

UI/UX
Frontend

Gaps:

Python
Computer Vision
Backend
```

Potential recommendation:

> Candidate A matches Python + Computer Vision and has weekend
> availability.

------------------------------------------------------------------------

## Matching Philosophy

The matcher should not simply find the person with the largest number of
matching skills.

It should consider:

1.  Skill relevance
2.  Skill gaps
3.  Interest alignment
4.  Technology compatibility
5.  Availability
6.  Experience

The matching system should be explainable.

------------------------------------------------------------------------

## Permissions

The matcher may:

-   Analyze profiles
-   Recommend candidates
-   Identify skill gaps

It must not:

-   Automatically invite users
-   Automatically add members
-   Expose private profile information beyond allowed fields

------------------------------------------------------------------------

# 7. AI-003 --- Project Assistant

## Purpose

Help a team move from project definition to a functioning MVP.

This is not an autonomous coding agent.

It is a project intelligence layer.

------------------------------------------------------------------------

## Inputs

The assistant can access:

-   Hackathon
-   Project definition
-   Team
-   Skills
-   Tasks
-   Project state
-   Links
-   Documents
-   Relevant project notes

------------------------------------------------------------------------

## Primary Jobs

### Planning

> What should we build first?

### Task generation

> Turn our MVP into tasks.

### Prioritization

> Which tasks are critical?

### Dependency analysis

> What is blocking the frontend?

### Scope control

> Which features should we remove from the MVP?

### Progress analysis

> What remains before submission?

------------------------------------------------------------------------

## Example

User:

> We only have two days left. What should we do?

The assistant should inspect:

-   Deadline
-   Remaining tasks
-   Task priorities
-   Dependencies
-   Team capacity

Then provide an actionable plan.

It should not pretend to know information that isn't available.

------------------------------------------------------------------------

# 8. Project Assistant --- Task Generation

When asked to generate tasks, the AI should produce structured tasks.

Example:

``` text
Task:
Build image upload interface

Priority:
High

Owner:
Frontend

Dependencies:
Authentication

Reason:
Required before model testing can be integrated into the user flow.
```

Users should be able to accept or edit generated tasks.

------------------------------------------------------------------------

# 9. Project Assistant --- Scope Control

Hackathons have limited time.

The assistant should actively identify scope risks.

Example:

``` text
MVP

Required:
✓ Login
✓ Image upload
✓ Prediction
✓ Result screen

Potentially unnecessary:
○ Social feed
○ Advanced analytics dashboard
○ Gamification
○ Multi-language support
```

The AI should explain why a feature may be unnecessary rather than
simply deleting it.

------------------------------------------------------------------------

# 10. Project Assistant Permissions

The assistant may:

-   Generate tasks
-   Suggest priorities
-   Identify risks
-   Recommend scope changes
-   Analyze project progress

The assistant should require user confirmation before:

-   Deleting tasks
-   Reassigning important work
-   Changing project scope
-   Changing project state
-   Sending team communications

------------------------------------------------------------------------

# 11. AI-004 --- Submission Reviewer

## Purpose

Determine whether a project adequately addresses known hackathon
requirements.

The reviewer is an evidence-based checker, not a judge.

------------------------------------------------------------------------

## Inputs

### Hackathon

-   Rules
-   Tracks
-   Requirements
-   Submission format
-   Evaluation criteria when officially available

### Project

-   Problem
-   Solution
-   Features
-   Technical approach
-   Tech stack
-   Differentiator
-   MVP
-   Future scope

### Submission

-   Description
-   Demo
-   Repository
-   Documentation
-   Files

------------------------------------------------------------------------

## Output

Each finding should follow:

``` text
Requirement
Evidence
Status
Potential Gap
Recommendation
Suggested Improvement
```

Possible status values:

``` text
Addressed
Partially Addressed
Missing
Unclear
Not Applicable
```

------------------------------------------------------------------------

## Example

``` text
Requirement:
The project must meaningfully use AI.

Evidence:
The project uses an image classification model.

Status:
Partially Addressed

Potential Gap:
The submission does not explain why AI is necessary.

Recommendation:
Explain the model's role and the user-facing benefit.
```

------------------------------------------------------------------------

# 12. Submission Reviewer --- Important Rule

The reviewer must not invent requirements.

If a hackathon requirement is unknown:

> Requirement information unavailable.

It should not hallucinate rules or evaluation criteria.

------------------------------------------------------------------------

# 13. Submission Reviewer --- No Fake Scores

V1 should avoid arbitrary scores such as:

> "Your project has an 87% chance of winning."

That creates false precision.

The reviewer should instead identify concrete strengths, gaps, and
evidence.

------------------------------------------------------------------------

# 14. Shared AI Context

The agents should share a common structured context layer.

Example:

``` text
HackathonContext
├── name
├── description
├── tracks
├── rules
├── requirements
└── deadline

ProjectContext
├── problem
├── users
├── solution
├── features
├── differentiator
├── tech_stack
├── mvp
└── future_scope

TeamContext
├── members
├── skills
├── availability
└── responsibilities

BuildContext
├── tasks
├── status
├── dependencies
└── progress

SubmissionContext
├── description
├── demo
├── repository
├── files
└── checklist
```

------------------------------------------------------------------------

# 15. Agent Context Matrix

  Context              Copilot    Matcher   Assistant   Reviewer
  ----------------- ---------- ---------- ----------- ----------
  User Profile               ✓          ✓           ✓   Optional
  Hackathon                  ✓          ✓           ✓          ✓
  Project                    ✓          ✓           ✓          ✓
  Team                Optional          ✓           ✓          ✓
  Tasks               Optional   Optional           ✓   Optional
  Submission          Optional         No           ✓          ✓
  Hackathon Rules            ✓   Optional           ✓          ✓

------------------------------------------------------------------------

# 16. AI Output Contract

AI should return structured output wherever possible.

Instead of:

``` text
Here are some ideas...
```

Prefer:

``` text
{
  "problem": "...",
  "target_users": ["..."],
  "solution": "...",
  "features": ["..."],
  "differentiator": "...",
  "technology_stack": ["..."]
}
```

The exact schema belongs in the technical implementation.

The product requirement is:

**AI output must be machine-readable when the output maps to product
data.**

------------------------------------------------------------------------

# 17. AI Generation Lifecycle

Every significant AI action should conceptually follow:

``` text
User Request
    ↓
Load Relevant Context
    ↓
Validate Context
    ↓
AI Generation
    ↓
Structured Output
    ↓
Validation
    ↓
User Review
    ↓
Accept / Edit / Reject
    ↓
Persist
```

------------------------------------------------------------------------

# 18. AI Failure Handling

If generation fails:

The user should see:

> We couldn't generate this right now. Your existing project data is
> safe.

The system should:

-   Preserve current data
-   Allow retry
-   Avoid duplicate writes
-   Avoid partially overwriting fields

------------------------------------------------------------------------

# 19. AI Hallucination Controls

HackLoop should treat AI output as suggestions unless supported by known
data.

### For hackathon facts

Prefer verified stored hackathon data.

### For user/project data

Use the actual project database.

### For recommendations

Clearly distinguish:

-   Known information
-   AI suggestion
-   User decision

### For rules

Never invent missing requirements.

------------------------------------------------------------------------

# 20. AI Transparency

The UI should make AI-generated content recognizable.

Possible labels:

-   AI Suggested
-   AI Generated
-   AI Recommendation
-   User Edited
-   Verified Requirement

The exact visual treatment belongs to the design system.

------------------------------------------------------------------------

# 21. Human-in-the-Loop Rules

Users remain responsible for final decisions.

AI should assist with:

-   Generation
-   Analysis
-   Recommendations
-   Organization
-   Review

Users control:

-   Final project definition
-   Team invitations
-   Task ownership
-   Project scope
-   Submission content
-   Final submission

------------------------------------------------------------------------

# 22. AI Memory Strategy

V1 should not create a mysterious long-term AI memory system.

Instead, use explicit structured project context.

The AI can reconstruct its working context from:

``` text
User
+
Hackathon
+
Project
+
Team
+
Tasks
+
Submission
```

This is more predictable and easier to debug.

------------------------------------------------------------------------

# 23. AI Provider Strategy

HackLoop should remain provider-neutral.

Do not design the product around one model vendor.

The architecture should allow different models to be used for different
jobs.

For example:

``` text
AI Gateway
    ↓
Model Provider
    ├── Model A
    ├── Model B
    └── Model C
```

The application should interact with an internal AI service rather than
embedding provider-specific logic throughout the product.

------------------------------------------------------------------------

# 24. Model Selection Philosophy

Do not automatically use the most expensive model for every request.

Use model capability according to task complexity.

### Lightweight tasks

-   Classification
-   Extraction
-   Simple rewriting
-   Skill normalization

### Advanced reasoning

-   Project critique
-   Architecture reasoning
-   Submission analysis
-   Complex planning

The exact model selection should be decided during technical
implementation and validated experimentally.

------------------------------------------------------------------------

# 25. AI Cost Controls

V1 should track:

-   AI requests
-   Model used
-   Token/input usage where available
-   Output usage
-   Estimated cost
-   User/project association

This allows the team to understand AI economics before scaling.

------------------------------------------------------------------------

# 26. AI Observability

For every important AI operation, the system should be able to identify:

-   Agent
-   User
-   Project
-   Request type
-   Model
-   Success/failure
-   Latency
-   Usage
-   Error

Do not expose internal debugging information to normal users.

------------------------------------------------------------------------

# 27. AI Evaluation

AI features need evaluation datasets.

Before launch, create test cases for:

### Copilot

-   Vague idea
-   Strong idea
-   Overly broad idea
-   Impossible idea
-   Hackathon mismatch

### Matcher

-   Exact skill match
-   Partial match
-   No match
-   Overqualified candidate
-   Availability conflict

### Project Assistant

-   Small project
-   Large project
-   Tight deadline
-   Missing task information
-   Blocked dependency

### Reviewer

-   Complete submission
-   Missing requirement
-   Weak evidence
-   Unknown requirement
-   Contradictory project information

------------------------------------------------------------------------

# 28. Agent Success Metrics

Do not measure only AI engagement.

### Copilot

Measure:

-   Projects created
-   Accepted suggestions
-   Project completion
-   User edits after generation

### Matcher

Measure:

-   Recommendations viewed
-   Invitations sent
-   Invitations accepted
-   Teams formed

### Project Assistant

Measure:

-   Generated tasks accepted
-   Task completion
-   Reduced project blockers

### Reviewer

Measure:

-   Reviews completed
-   Identified gaps addressed
-   Submission readiness progression

The final product metric remains:

**Users reaching submission-ready projects.**

------------------------------------------------------------------------

# 29. V1 Agent Boundaries

V1 AI should NOT:

-   Submit projects automatically
-   Invite teammates automatically
-   Delete user content automatically
-   Change permissions
-   Fabricate hackathon rules
-   Fabricate evidence
-   Claim guaranteed success
-   Claim a probability of winning
-   Act as an autonomous coding agent
-   Make irreversible project decisions without confirmation

------------------------------------------------------------------------

# 30. Future AI Agents

These are intentionally deferred.

## AI Project Manager

Could monitor the project continuously and proactively coordinate work.

## Technical Mentor

Could provide deeper technical guidance.

## Judge Simulator

Could simulate evaluation using known judging criteria.

## Demo Coach

Could help improve demonstrations and presentations.

## Research Agent

Could perform deeper external research.

## Architecture Reviewer

Could inspect technical architecture.

## Pitch Coach

Could refine pitch narratives.

These should only be built after V1 establishes a reliable project
context layer.

------------------------------------------------------------------------

# 31. Agent Orchestration

V1 does not require a complex multi-agent autonomous system.

Prefer:

``` text
User
 ↓
HackLoop AI Gateway
 ↓
Selected Agent
 ↓
Structured Context
 ↓
Model
 ↓
Validation
 ↓
User
```

Only introduce multi-agent orchestration when there is a demonstrated
product need.

------------------------------------------------------------------------

# 32. Recommended V1 AI Architecture

``` text
                    ┌────────────────────┐
                    │   HackLoop App     │
                    └─────────┬──────────┘
                              │
                              ↓
                    ┌────────────────────┐
                    │    AI Gateway      │
                    └─────────┬──────────┘
                              │
              ┌───────────────┼───────────────┐
              ↓               ↓               ↓
        ┌──────────┐    ┌──────────┐    ┌────────────┐
        │ Copilot  │    │ Matcher  │    │ Assistant  │
        └──────────┘    └──────────┘    └────────────┘
                              │
                              ↓
                       ┌────────────┐
                       │  Reviewer  │
                       └────────────┘

                              │
                              ↓
                    ┌────────────────────┐
                    │ Structured Context │
                    │ User/Hackathon/    │
                    │ Project/Team/Build │
                    │ Submission         │
                    └────────────────────┘
```

------------------------------------------------------------------------

# 33. The Most Important Architectural Rule

**Do not build four separate AI products.**

Build one AI layer with four specialized capabilities.

That means:

``` text
One context system
+
One AI gateway
+
Specialized agents
+
Structured outputs
+
Human approval
```

This will make HackLoop easier to evolve.

------------------------------------------------------------------------

# 34. Final Principle

HackLoop's competitive value should not be:

> "We have AI."

The differentiator should be:

> **HackLoop understands the entire lifecycle of a hackathon project and
> uses AI at each stage without losing context.**

The AI should help users make progress.

The user remains the decision-maker.

The project remains the source of truth.

The workflow remains the product.
