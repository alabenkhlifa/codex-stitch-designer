---
name: stitch-designer
description: Use Google Stitch MCP from Codex to create, inspect, refine, and hand off high-quality UI designs. Use when the user asks for Stitch projects, screen generation, design-system work, variants, mockup-to-prompt conversion, or implementation handoffs from Stitch output.
---

# Stitch Designer

This skill turns Codex into a context-aware design partner for Google Stitch MCP. It helps choose the right Stitch project, write concrete design prompts, generate or edit screens, explore variants, critique the result, and prepare implementation handoffs.

## Core Workflow

1. Identify the design surface: mobile app, web app, dashboard/admin, landing page, game/tool, or responsive system.
2. Gather context from the user, local project docs/UI files, screenshots, existing Stitch screens, and design systems.
3. If no Stitch project is specified, ask whether to reuse an existing project, create a new project, or work without Stitch.
4. Inspect existing Stitch state before mutating it.
5. Use the narrowest Stitch MCP operation for the request.
6. Review the generated result for workflow clarity, contrast, hierarchy, platform fit, accessibility, and implementation risk.
7. Report project IDs, screen IDs, design-system assets, and any handoff details.

## Project Selection

When the user asks for Stitch design work without a project ID:

- If the task should match existing design language, list projects and recommend reusing one.
- If the task is a new concept or isolated exploration, ask whether to create a new Stitch project.
- If the user only needs a design spec, critique, or implementation handoff, work without creating a Stitch project.
- Use an interactive select list when available; otherwise ask one concise question.
- Do not create a project unless the user explicitly asks or confirms.

## Tool Use

Use the narrowest Stitch tool:

- `list_projects`: connectivity check and project discovery.
- `create_project`: only after explicit request or confirmation.
- `get_project`: inspect title, project ID, screens, theme, and current assets.
- `list_screens` / `get_screen`: inspect existing screens before editing.
- `list_design_systems`: find reusable design-system assets.
- `generate_screen_from_text`: create a new screen.
- `edit_screens`: targeted refinements to existing screens.
- `generate_variants`: explore alternatives without overwriting a direction.
- `create_design_system`, `update_design_system`, `apply_design_system`: reusable theme work.
- `upload_design_md` then `create_design_system_from_design_md`: when the user provides a DESIGN.md-style spec.

## Stitch ID Rules

- `projectId` parameters usually expect the bare project number.
- `get_project.name` expects `projects/<projectId>`.
- `selectedScreenIds` expects bare screen IDs.
- `get_screen.name` expects `projects/<projectId>/screens/<screenId>` and also requires bare `projectId` and `screenId`.
- `designSystem` parameters often expect `assets/<assetId>`.
- `apply_design_system.assetId` expects the bare asset ID.

Normalize full resource names to the parameter shape required by the active tool.

## Reliability Rules

- Stitch generation/edit calls can take minutes. Do not retry while a request is still running.
- If `generate_screen_from_text` times out, poll `get_screen` every 30 seconds for up to 10 attempts before giving up.
- If generation/edit/variants fail with a connection error, the operation may still complete; inspect the project before retrying.
- If Stitch returns `The service is currently unavailable`, one later retry is acceptable for lightweight create/read calls.
- If a design-system call returns `invalid argument`, simplify the payload or encode the style in the screen prompt.
- Pass relevant `outputComponents` text and suggestions back to the user.

## Context-Aware Design Pass

Before prompting Stitch, decide:

- Purpose: what task does the interface help complete?
- Audience: consumer, operator, admin, developer, executive, creator, buyer, student, or other.
- Surface: mobile, web, dashboard, landing page, game/tool, tablet/kiosk, or responsive system.
- Tone: refined luxury, brutalist utility, playful, editorial, industrial, clinical, retro-futuristic, command center, natural, art deco, dense operational, or another deliberate direction.
- Differentiator: the memorable idea, such as layout rhythm, navigation model, material language, type treatment, icon system, or motion cue.
- Constraints: accessibility, locale, density, performance, brand consistency, platform conventions.

Do not force one default style across projects. Reuse an existing design direction only when the project clearly establishes it or the user asks for it.

## Prompt Standards

A strong Stitch prompt includes:

- Product context and target user.
- Screen goal and primary workflow.
- Device/surface target.
- Layout hierarchy and expected states.
- Design direction and why it fits.
- Color roles, typography, surfaces, spacing, shape, elevation, background, and motion cues.
- Exact labels/copy when known.
- Interaction semantics: actual actions vs informational elements.
- Constraints: touch targets, contrast, no overlap, one primary path, locale support.
- Negative constraints: no generic AI aesthetics, no duplicate CTAs, no unreadable inactive controls, no static poster when the user asked for an app/tool.

When the user provides a screenshot/mockup, translate it into explicit design instructions unless the active Stitch tool accepts image input.

## Surface Blueprints

### Mobile App Screen

- Product and audience.
- Screen job in one sentence.
- Safe areas, thumb reach, 44px+ targets, readable type.
- Navigation model: back, tabs, bottom nav, stepper, modal, or task flow.
- Top-to-bottom content hierarchy.
- Visual direction, type pairing, color roles, material/elevation, icon style.
- Primary, secondary, disabled, selected, and pressed states.
- No marketing hero, competing CTAs, cramped cards, or unreadable inactive nav.

### Web App Or SaaS Tool

- User role and repeated workflow.
- Information architecture: sidebar/topbar, work area, detail panel, filters, command actions.
- States: empty, loading, error, selected, saved/unsaved, permission-limited.
- Density target: compact operational, balanced productivity, or spacious executive.
- Tables/forms/charts with columns, controls, labels, and status chips.
- Responsive behavior.

### Dashboard Or Admin Console

- Operational question the dashboard answers.
- Metrics, status severity, filters, time range, owners, and drill-down path.
- Metrics row, chart grid, table/log area, side filters, alerts.
- Normal, warning, critical, stale-data, and no-data states.
- No oversized hero or decorative cards that reduce scan speed.

### Landing Page

- Brand/product/place/person as the first-viewport signal.
- Literal offer or category headline.
- Primary and secondary CTA hierarchy.
- Hero media direction: real image, generated bitmap, product media, or immersive scene.
- Visible hint of below-fold proof/content.
- No generic split-card hero, abstract SVG filler, or gradient-only hero.

### Game Or Interactive Tool

- Immediate playable state.
- Core loop: objective, controls, feedback, score/progress, success/failure, restart/next.
- Large controls and resilient text sizing.
- Visual identity tied to rules/theme.
- Motion feedback for state transitions, timer, correct/incorrect, drag/drop, hover/pressed.
- No hidden main action or instruction wall.

## Variant Strategy

Generate variants when the user asks for options, the direction is underdetermined, or a high-impact screen needs exploration.

Use clear intent:

- Conservative: closest to existing product/brand, lowest implementation risk.
- Distinctive: stronger identity while preserving workflow.
- Experimental: bolder layout/material/motion idea that may need refinement.

Ask for variants with the same functional requirements and different design strategies, not random reskins. Compare variants by workflow clarity, memorability, accessibility, implementation cost, and brand fit.

## Post-Generation Critique

Critique every result against:

- Workflow clarity.
- Visual hierarchy.
- Platform fit.
- Typography.
- Contrast and inactive-state readability.
- Density.
- Expected states.
- Accessibility.
- Implementation risk.

If the result is directionally right but flawed, use a targeted edit. If the concept is wrong, generate a new screen or variants instead of repeatedly patching details.

## Implementation Handoff

When the user wants code implementation, produce a handoff:

- Screen IDs and screenshot/design-system asset IDs.
- Design intent and selected variant rationale.
- Design tokens: colors, typography, spacing, radius, borders, shadows/elevation, motion.
- Component inventory and states.
- Exact content and localization notes.
- Responsive rules and safe areas.
- Assets and whether they are real, generated, or placeholders.
- Implementation risks and open product questions.

Do not claim a Stitch design is implemented in code until a separate implementation step is complete.
