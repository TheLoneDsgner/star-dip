# StarDIP Website — Agentic PDR

> **Purpose:** A concise source of truth for AI agents and developers
> building the Star Development Impact Partners (StarDIP) website.
> Follow this document unless the project owner provides updated
> direction.

## 1. Project Overview

**Organization:** STAR DEVELOPMENT IMPACT PARTNERS (StarDIP)
**Location context:** Nigerian development organization
**Brand message:** *Building Capacity. Driving Impact. Transforming Communities.*

StarDIP works with communities, institutions, and partners to address
interconnected challenges across health, livelihoods, agriculture,
gender, youth development, and environmental sustainability.

**Core positioning:** Present StarDIP as a credible, locally rooted
development organization — not simply a collection of unrelated charity
projects. Communicate how its work contributes to healthier, empowered,
and resilient communities.

## 2. Product Goals

- Explain StarDIP's purpose, work, approach, and values clearly.
- Build trust with communities, institutional partners, funders, and collaborators.
- Make programmes, initiatives, resources, and stories easy to discover.
- Encourage relevant actions: partner, support programmes, volunteer, or make an enquiry.
- Provide a responsive, accessible, maintainable website that can grow with the organization.

## 3. Primary Audiences

- Communities and programme participants
- Government and civil-society organizations
- Development partners, funders, and potential collaborators
- Researchers, institutions, and technical experts
- Volunteers and people interested in supporting the work

## 4. Information Architecture

Recommended main navigation:

1. Home
2. About Us
3. What We Do
4. Our Approach
5. Our Impact
6. Projects & Initiatives
7. Resources
8. Get Involved
9. Contact

**Primary navigation CTA:** Partner With Us
**Secondary CTA, where appropriate:** Support Our Work

Supporting pages may include:

- About StarDIP
- Mission, Vision & Values
- One Health
- Health
- Reproductive Health
- Pad Without Price
- Agriculture & Livelihoods
- Youth Development
- Women & Girls
- Climate & Environment
- Capacity Building
- Project / initiative detail pages
- Impact and stories
- Governance & Accountability
- Safeguarding
- Privacy Policy and other required legal pages

Do not create empty or fabricated pages simply to fill the sitemap. Use
"coming soon" only when approved by the project owner.

## 5. Homepage Content Direction

Recommended section order:

1. **Hero:** "Building Capacity. Driving Impact. Transforming Communities." Brief introduction and clear CTAs.
2. **Who We Are:** Concise introduction to StarDIP.
3. **Areas of Focus:** Visual cards for key programme areas.
4. **Our Approach:** Four steps — Listen & Understand; Co-create & Build Capacity; Implement & Measure; Adapt & Sustain.
5. **Featured Initiative:** For example, Pad Without Price, only with accurate programme status.
6. **Impact:** Publish only verified metrics and outcomes.
7. **Stories:** Human experiences, learning, and documented progress.
8. **Partners:** Show logos only when real partnerships are confirmed.
9. **Closing CTA:** "Let's Create Impact Together."

## 6. About Page Direction

Keep the copy concise and scannable. Recommended sections:

- Hero and short introduction
- Who We Are
- Mission and Vision
- Core Values
- Areas of Focus
- Our Approach
- Partnerships
- Accountability & Safeguarding
- Closing CTA

Core values in the current content direction: **People First, Locally Led, Evidence-Informed, Partnership-Driven, Sustainability-Focused, Results-Oriented.**

## 7. UX, Content & Visual Principles

- Use clear, professional, people-centred, hopeful, inclusive language.
- Prefer short headings, concise paragraphs, descriptive links, and meaningful CTAs.
- Prioritize mobile-first responsive layouts and obvious navigation.
- Use authentic, respectful imagery that reflects communities and the work.
- Design for readability, sufficient contrast, keyboard access, visible focus states, and semantic page structure.
- Use reusable components for cards, buttons, section headers, breadcrumbs, and calls to action.
- Maintain consistent spacing, typography, colour, iconography, and interaction patterns.
- Avoid visual clichés, excessive animation, clutter, and unsupported impact claims.

## 8. Content Integrity & Trust

**Never invent or imply as fact:**
- Impact statistics, programme outcomes, testimonials, participant stories, partners, funders, staff, leadership, awards, or project dates.
- Official contact details, registration information, or policy documents.

Use clear placeholders for missing approved information and flag it for
the project owner. Label dummy stories and sample data as illustrative
during development; do not publish them as real evidence. Confirm
programme names, current status, and official wording before launch.

Governance and safeguarding copy must reflect StarDIP's actual approved
policies and operating practices. Do not claim a policy or mechanism
exists until confirmed.

## 9. Development Requirements

- Build reusable, maintainable components and keep content separate from presentation where practical.
- Ensure layouts work on mobile, tablet, and desktop.
- Optimize image sizes, loading performance, metadata, and page titles.
- Use semantic HTML, accessible form labels, useful validation, and clear success/error states.
- Include descriptive alt text for meaningful images; decorative images should not add redundant screen-reader content.
- Provide sensible empty, loading, and error states for dynamic content.
- Protect contact forms against spam and handle submitted personal data responsibly.
- Do not add donation/payment processing, analytics, third-party integrations, or complex CMS functionality without project-owner approval.
- Keep secrets and credentials out of source control.

**Technology stack:** Not specified yet. Inspect the existing repository
and follow its established framework and conventions. If starting from
scratch, propose the stack and explain the trade-offs before introducing
substantial dependencies.

## 10. Agentic Development Workflow

Before making changes:
1. Inspect the repository, existing routes, components, assets, and project instructions.
2. Identify what already exists; do not rebuild working features without reason.
3. Break work into small, testable tasks and state assumptions where requirements are missing.
4. Reuse established patterns and keep changes scoped to the requested task.

While implementing:
1. Build the smallest complete increment.
2. Keep components readable and avoid unnecessary abstractions or dependencies.
3. Use approved content; flag missing facts rather than guessing.
4. Test responsive behaviour, keyboard interaction, links, forms, and relevant error states.

Before marking work complete:
1. Run available lint, type-check, build, and test commands.
2. Fix issues caused by the change and report any checks that could not be run.
3. Summarize files changed, key decisions, remaining questions, and any placeholder content.
4. Do not claim a task is complete unless it has been verified to the extent possible.

## 11. Definition of Done

A page or feature is ready when:

- It meets the requested scope and uses approved content.
- It is responsive across common viewport sizes.
- Navigation, links, CTAs, and forms behave as expected.
- Accessibility basics and semantic structure are in place.
- No fabricated metrics, testimonials, partners, or organizational claims appear.
- Relevant project checks pass, or known failures are clearly reported.
- Any unresolved content, policy, or technical decisions are documented.

## 12. Open Decisions

Confirm with the project owner before final launch:

- Framework, hosting, CMS, and deployment workflow
- Official logo, brand colours, typography, and final design tokens
- Approved contact details and social links
- Verified programme status, impact data, stories, and partner permissions
- Approved governance and safeguarding policies
- Whether donations, newsletter signup, analytics, or a content-management interface are in scope

---

**Working rule for AI agents:** Preserve StarDIP's people-centred,
locally led, evidence-informed positioning. Make reasonable
implementation decisions when low-risk, document assumptions, and ask
before inventing facts or making consequential product, content,
privacy, or infrastructure decisions.
