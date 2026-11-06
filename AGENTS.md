# Innocitto Bricks Agents

Agent instructions for WordPress projects built with Bricks Builder and the Bricks Native Framework (BNF). Load the referenced docs in `agent-docs/` at the workflow steps listed below.

## Overview

This is the standard operating system for building WordPress sites with Bricks Builder and the Bricks Native Framework. One source of truth, any harness.

## Workflow

1. Business/Brand Discovery
2. Copywriting Discovery
3. Home Page Wireframing & Copy
4. Home Page UI Design
5. Remaining Wireframes
6. Remaining UI Screens
7. Development
8. SEO Optimization
9. Performance Optimization
10. Deployment

## Getting started: Discovery

Every project begins with a guided discovery interview. When the user says `start discovery`, `/discovery`, "begin discovery", or asks to kick off a new project, load and follow [agent-docs/discovery.md](agent-docs/discovery.md) and run the interview to completion.

Do not skip ahead to copywriting, wireframing, or design until the discovery brief at `discovery/brief.md` is complete and the user has approved it. If a brief already exists, resume it rather than starting over.

## Project Environment & Stack

- **Paper or Figma**: wireframing and design
- **WordPress**: platform
- **Bricks Builder 2.2+ (https://academy.bricksbuilder.io)**: page builder and theme
- **Bricks Native Framework (Bricksmaven)**: design system built on the Bricks Style Manager (variables, color palette, theme style). No ACSS, Core Framework, or Advanced Themer.
- **Root font size is 10px.** On these sites, `1rem` = 10px.

## Discovery Conventions (step 1)

Load and follow [agent-docs/discovery.md](agent-docs/discovery.md) to run the guided interview and produce the project brief that drives every later step.

## Copy Conventions (steps 2–3)

Load and follow [agent-docs/copywriting.md](agent-docs/copywriting.md) during copywriting and any page copy review before wireframing.

## Design Conventions (steps 3–6)

Load and follow [agent-docs/design.md](agent-docs/design.md) for wireframing, UI design, and any visual review pass. Design within the BNF token scales ([agent-docs/bnf.md](agent-docs/bnf.md)).

## Build Conventions (step 7)

Load and follow, during development and any layout, class, or CSS review:

- [agent-docs/bricks.md](agent-docs/bricks.md): structure, global classes and BEM, templates, components, query loops, JSON delivery
- [agent-docs/bnf.md](agent-docs/bnf.md) plus the relevant files in [agent-docs/bnf/](agent-docs/bnf/): design tokens and what the theme style already handles
- [agent-docs/html.md](agent-docs/html.md): semantics and accessibility
- [agent-docs/css.md](agent-docs/css.md): custom CSS, only when settings and tokens aren't enough

Before styling a new site, check [agent-docs/bnf/known-issues.md](agent-docs/bnf/known-issues.md) and confirm with the user which fixes are applied.

## Steps 8–10

SEO, performance, and deployment don't have dedicated docs yet. Ask the user for their process before starting these steps.
