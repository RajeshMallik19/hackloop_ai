# HackLoop --- User Flow Architecture

Version: 1.0\
Status: Product Definition\
Scope: HackLoop V1

------------------------------------------------------------------------

## 1. Purpose

This document defines the complete user journey for HackLoop V1.

HackLoop should guide a participant through one continuous workflow:

**Discover → Understand → Ideate → Form Team → Plan → Build → Validate →
Submit**

The product should not feel like a collection of unrelated AI tools.
Every step should build on the structured context created in the
previous step.

------------------------------------------------------------------------

## 2. Core User Journey

``` text
Landing Page
    ↓
Sign Up / Login
    ↓
Create Profile
    ↓
Dashboard
    ↓
Explore Hackathons
    ↓
Hackathon Details
    ↓
Start Project
    ↓
AI Hackathon Copilot
    ↓
Project Definition
    ↓
Team Formation
    ↓
Project Workspace
    ↓
Build & Track
    ↓
AI Submission Review
    ↓
Improve Project
    ↓
Submission
```

### Product principle

A user should never need to restart context when moving between stages.

For example:

-   Hackathon requirements should be available to the Copilot.
-   Copilot output should become project data.
-   Project requirements should inform team matching.
-   Team skills should inform project planning.
-   Project information should inform the submission reviewer.

------------------------------------------------------------------------

# 3. Entry Points

Users can enter HackLoop through several paths.

## 3.1 New participant

``` text
Landing
→ Sign Up
→ Profile Setup
→ Dashboard
```

## 3.2 Returning participant

``` text
Landing
→ Login
→ Dashboard
→ Continue Existing Project
```

## 3.3 User discovers a hackathon first

``` text
Landing
→ Explore Hackathons
→ Hackathon Details
→ Start Project
→ Login / Sign Up if required
→ Project Creation
```

## 3.4 User already has an idea

``` text
Dashboard
→ Create Project
→ Select Hackathon
→ AI Copilot
→ Define Project
```

The system should support both:

**Hackathon-first**

and

**Idea-first**

workflows.

------------------------------------------------------------------------

# 4. Authentication Flow

## 4.1 Sign Up

Required:

-   Name
-   Email
-   Password

Optional during initial setup:

-   GitHub
-   Portfolio
-   LinkedIn

After account creation:

``` text
Sign Up
→ Profile Setup
→ Dashboard
```

## 4.2 Login

``` text
Login
→ Dashboard
```

## 4.3 Authentication principle

Do not make profile setup unnecessarily long.

The user should be able to reach the product quickly and complete
missing profile information progressively.

------------------------------------------------------------------------

# 5. Profile Setup Flow

The profile is the foundation for team matching and personalization.

## Required profile information

### Identity

-   Name
-   Profile photo
-   Short bio

### Skills

-   UI/UX
-   Frontend
-   Backend
-   AI/ML
-   Data
-   Cloud
-   Hardware
-   Blockchain
-   Other relevant skills

### Technologies

Examples:

-   React
-   Next.js
-   Python
-   Java
-   Flutter
-   Firebase
-   Supabase
-   AWS

### Experience

-   Beginner
-   Intermediate
-   Advanced

### Interests

Examples:

-   AI
-   Sustainability
-   FinTech
-   HealthTech
-   EdTech
-   Cybersecurity
-   Social impact

### Availability

Useful for team matching.

Examples:

-   Weekends
-   Evenings
-   Full-time during hackathon

### Links

-   GitHub
-   Portfolio
-   LinkedIn

------------------------------------------------------------------------

# 6. Dashboard Flow

The dashboard should answer one question:

**"What should I do next?"**

## Dashboard sections

### Continue Project

Shows active projects.

Example:

``` text
EcoVision
AI Hackathon 2026

Progress: 62%

Next:
Complete submission review
```

### Recommended Hackathons

Personalized based on:

-   Skills
-   Interests
-   Technology
-   Eligibility
-   Deadline

### Your Teams

Active teams and invitations.

### AI Suggestions

Examples:

-   "Your project needs a backend developer."
-   "This hackathon closes in 3 days."
-   "Your submission is missing evidence for one requirement."

The dashboard should prioritize actions over statistics.

------------------------------------------------------------------------

# 7. Hackathon Discovery Flow

## Explore

Users can:

-   Search
-   Filter
-   Sort
-   Save
-   Open details

### Filters

-   Technology
-   Category
-   Online / Offline
-   Location
-   Deadline
-   Prize
-   Eligibility
-   Beginner-friendly

## Hackathon Card

Each card should communicate:

-   Name
-   Organizer
-   Deadline
-   Prize
-   Format
-   Theme
-   Technologies
-   Eligibility

Primary action:

**View Hackathon**

Secondary action:

**Save**

------------------------------------------------------------------------

# 8. Hackathon Details Flow

The details page should make the hackathon understandable before the
user commits.

## Sections

### Overview

What is the hackathon?

### Problem / Theme

What are participants expected to build?

### Tracks

Available challenge tracks.

### Rules

Important restrictions.

### Eligibility

Who can participate?

### Timeline

Registration → Submission → Judging → Results

### Prizes

Prize information.

### Submission Requirements

What must be submitted?

### Actions

Primary:

**Start Project**

Secondary:

**Save Hackathon**

------------------------------------------------------------------------

# 9. Start Project Flow

When the user clicks **Start Project**:

``` text
Hackathon
    ↓
Create Project
    ↓
Choose:
    • I have an idea
    • Help me generate an idea
```

This prevents the product from assuming every participant starts from
the same place.

------------------------------------------------------------------------

# 10. AI Hackathon Copilot Flow

The Copilot is not simply a chatbot.

It is a structured project-building assistant.

## Input

User can provide:

-   Rough idea
-   Problem statement
-   Existing concept
-   Random notes
-   Voice/text in future versions

Example:

> "I want to build an AI system that helps small farmers predict crop
> disease."

## Copilot processing

The AI should help transform the rough idea into:

``` text
Problem
↓
Target Users
↓
Solution
↓
Core Features
↓
Differentiator
↓
Technical Approach
↓
Technology Stack
↓
MVP
↓
Future Scope
↓
Pitch
```

## Important interaction

The AI should ask clarifying questions when necessary.

Example:

> Who is the primary user?

User:

> Small-scale farmers.

Copilot:

> What should happen when disease is detected?

User:

> The system should recommend treatment.

The project becomes progressively more defined.

------------------------------------------------------------------------

# 11. Project Creation

When the user accepts the Copilot output:

**Create Project**

The AI output becomes structured project data.

Example:

``` text
Project
├── Problem
├── Target Users
├── Solution
├── Features
├── Differentiator
├── Tech Stack
├── MVP
└── Future Scope
```

This is critical.

The AI response should NOT remain trapped inside a chat window.

------------------------------------------------------------------------

# 12. Team Formation Flow

Once the project has been defined:

``` text
Project
→ Identify Required Skills
→ Compare Current Team
→ Identify Skill Gaps
→ Find Potential Members
```

Example:

``` text
Current Team

Rajesh
UI/UX + Product

Required Skills

AI/ML
Backend
Frontend

Missing

AI/ML
Backend
```

HackLoop can then suggest potential teammates.

------------------------------------------------------------------------

# 13. Team Matching

Matching should consider multiple signals.

### Required

-   Skills
-   Skill gaps
-   Interests

### Useful

-   Technology
-   Experience
-   Availability
-   Previous hackathon experience

### Important

The system should explain **why** someone is being recommended.

Example:

> Recommended because your project needs Python + ML, and this
> participant has both skills and is available during the hackathon.

Avoid opaque recommendations.

------------------------------------------------------------------------

# 14. Team Invitation Flow

``` text
Suggested Member
    ↓
View Profile
    ↓
Invite
    ↓
Pending
    ↓
Accept / Decline
```

If accepted:

``` text
Project Team
+
Member Profile
```

The project workspace updates automatically.

------------------------------------------------------------------------

# 15. Project Workspace

The workspace becomes the project's central operating system.

## Main sections

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
AI Tools
```

## Overview

Shows:

-   Project name
-   Hackathon
-   Problem
-   Solution
-   Team
-   Progress
-   Important deadlines

------------------------------------------------------------------------

# 16. Task Planning Flow

The project can begin with an MVP task list.

Example:

``` text
MVP

□ Build landing page
□ Create authentication
□ Build prediction API
□ Connect frontend
□ Test model
□ Prepare demo
□ Write README
□ Prepare submission
```

Tasks should have:

-   Title
-   Description
-   Owner
-   Status
-   Priority
-   Due date

------------------------------------------------------------------------

# 17. AI Project Assistance

The Copilot should remain accessible inside the workspace.

The user could ask:

> "What should we build next?"

or:

> "Our backend is delayed. What can the frontend team work on?"

or:

> "Review our current MVP and tell us what is unnecessary."

The AI should use the project's structured context.

It should not behave like a generic chatbot with no knowledge of the
project.

------------------------------------------------------------------------

# 18. Build Progress Flow

Project states:

``` text
Idea
↓
Defined
↓
Team Formed
↓
Planning
↓
Building
↓
Testing
↓
Submission Ready
↓
Submitted
```

These states should be visible throughout the product.

------------------------------------------------------------------------

# 19. AI Submission Reviewer

When the project reaches a reasonable level of completion:

**Review Submission**

The AI evaluates the project against the actual hackathon requirements.

## Review structure

For each criterion:

``` text
Criterion
Evidence Found
Potential Gap
Recommendation
Suggested Improvement
```

Example:

``` text
Criterion:
Use AI meaningfully.

Evidence:
The project uses an image classification model.

Potential Gap:
The submission does not explain why AI is necessary.

Recommendation:
Explain the model's role and measurable benefit.
```

The reviewer should distinguish:

-   Missing information
-   Weak explanation
-   Technical concern
-   Unsupported claim
-   Requirement mismatch

------------------------------------------------------------------------

# 20. Improvement Loop

The submission process is iterative.

``` text
Review
↓
Identify Gaps
↓
Improve Project
↓
Review Again
↓
Submission Ready
```

There should be no artificial requirement to run the reviewer only once.

------------------------------------------------------------------------

# 21. Submission Flow

Before submission, HackLoop should provide a final checklist.

### Submission checklist

-   [ ] Project description complete
-   [ ] Problem explained
-   [ ] Solution explained
-   [ ] Features documented
-   [ ] Technology stack documented
-   [ ] Team members confirmed
-   [ ] Demo link added
-   [ ] Repository link added
-   [ ] Required files attached
-   [ ] Hackathon requirements addressed
-   [ ] Submission deadline checked

Then:

**Submit / Go to Organizer Submission**

For V1, HackLoop does not need to replace the hackathon organizer's
submission system.

It can prepare and validate the submission.

------------------------------------------------------------------------

# 22. Project Lifecycle

The complete project lifecycle is:

``` text
DISCOVER
    ↓
Hackathon selected
    ↓
IDEATE
    ↓
Project created
    ↓
DEFINE
    ↓
Problem + Solution + MVP
    ↓
TEAM
    ↓
Skill gaps + Matching
    ↓
PLAN
    ↓
Tasks + Workspace
    ↓
BUILD
    ↓
Development + Collaboration
    ↓
VALIDATE
    ↓
AI Submission Review
    ↓
IMPROVE
    ↓
Fix gaps
    ↓
SUBMIT
    ↓
Submission-ready project
```

------------------------------------------------------------------------

# 23. State Model

Every project should have a clear state.

Suggested states:

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

These states should drive:

-   Dashboard status
-   Progress indicators
-   Suggested actions
-   Notifications
-   AI recommendations

------------------------------------------------------------------------

# 24. "Next Best Action"

One of HackLoop's most important UX concepts should be:

**Next Best Action**

At any point, HackLoop should identify the most useful next step.

Examples:

### New project

> Define your problem statement with AI Copilot.

### Incomplete team

> Your project needs an AI/ML teammate.

### Planning

> Create your first MVP tasks.

### Building

> 3 high-priority tasks are still unassigned.

### Near submission

> Run an AI Submission Review.

### Review completed

> Resolve 2 identified submission gaps.

This makes HackLoop feel like an active assistant rather than a passive
dashboard.

------------------------------------------------------------------------

# 25. Notifications

V1 notifications should be focused.

Examples:

-   Team invitation received
-   Team invitation accepted
-   Project deadline approaching
-   Task assigned
-   Task deadline approaching
-   Submission review completed
-   Project requirement appears incomplete

Avoid notification overload.

------------------------------------------------------------------------

# 26. Empty States

Every major screen needs a useful empty state.

Examples:

### No projects

> You haven't started a project yet.

CTA:

**Find a Hackathon**

### No team members

> Your project is missing some skills.

CTA:

**Find Teammates**

### No tasks

> Turn your MVP into actionable tasks.

CTA:

**Generate Tasks with AI**

### No review

> Your project is ready for a submission check.

CTA:

**Review Submission**

Empty states should always provide a next action.

------------------------------------------------------------------------

# 27. Error and Recovery Principles

AI output can be wrong.

Therefore:

-   Never silently overwrite user data.
-   Let users edit AI-generated content.
-   Show source/context where relevant.
-   Allow regeneration.
-   Preserve previous versions where useful.
-   Never present AI assumptions as confirmed facts.
-   Allow the user to reject AI suggestions.

AI is an assistant, not the owner of the project.

------------------------------------------------------------------------

# 28. Context Architecture

The same project context should flow through the entire system.

``` text
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

AI agents consume this context.

### Copilot

Hackathon + Project

### Team Matcher

Project + Profiles

### Project Assistant

Project + Team + Tasks

### Submission Reviewer

Hackathon Rules + Project + Submission

This prevents fragmented AI experiences.

------------------------------------------------------------------------

# 29. V1 Critical Path

The critical path is:

``` text
Sign Up
  ↓
Profile
  ↓
Hackathon
  ↓
Project
  ↓
Copilot
  ↓
Team
  ↓
Workspace
  ↓
Submission Review
```

Everything else should support this path.

If a feature does not improve this journey, it should be questioned
before entering V1.

------------------------------------------------------------------------

# 30. V1 UX Rule

HackLoop should always answer three questions:

### Where am I?

Example:

> Building → EcoVision

### What have I completed?

Example:

> 6/10 MVP tasks complete

### What should I do next?

Example:

> Run your first submission review.

This should be reflected across the dashboard, workspace, and project
navigation.

------------------------------------------------------------------------

# 31. Definition of a Successful V1 Journey

A real participant should be able to:

1.  Create an account.
2.  Build a useful profile.
3.  Find a relevant hackathon.
4.  Start a project.
5.  Turn a rough idea into a defined project using AI.
6.  Identify required team skills.
7.  Find and invite teammates.
8.  Create an MVP task plan.
9.  Work inside the project workspace.
10. Review the project against hackathon requirements.
11. Fix identified gaps.
12. Leave HackLoop with a submission-ready project.

That is the V1 journey.

------------------------------------------------------------------------

# 32. Product Principle

HackLoop should not be:

> "ChatGPT for hackathons."

It should be:

> **"The operating system for turning a hackathon opportunity into a
> submission-ready project."**

AI is the intelligence layer.

The workflow is the product.

The project is the persistent context.

The participant remains in control.
