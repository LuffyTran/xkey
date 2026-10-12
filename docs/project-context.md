# Project Context

## Metadata
- Project type: `brownfield`
- Workflow track: `lite`
- Last updated: `2026-10-12T07:09:48+00:00`

## Why This Project Exists
- Problem statement: XKey is a native macOS Vietnamese typing method (Telex, VNI, Simple Telex, auto-detect) that replaces unmaintained or incompatible Vietnamese IMEs on recent macOS (12+). It converts keystrokes into Vietnamese characters in any app. It adds productivity feat...
- Success metrics: Define 2-3 measurable KPIs (business + engineering) and target thresholds before /plan.
- Primary users/personas: Likely end users + internal operators; confirm exact personas and priority order.
- Key user journey: Confirm primary journey from first touch to successful task completion and expected SLA.

## Discovery Decisions (fill before /plan)
- Chosen direction: Xcode project (XKey.xcodeproj, Swift, SwiftUI plus AppKit) with two runtime surfaces. (1) XKey: a menu-bar app that installs a CGEvent tap and injects replacement keystrokes or text into the focused app. It uses the Accessibility API and has special handlin...
- Alternatives considered: Full rewrite vs incremental refactor; prioritize incremental path unless hard blockers emerge.
- Trade-offs accepted: Short-term delivery speed over broad architectural changes; revisit after first stable release.
- Non-goals: No large-scale rewrite or platform migration in this sprint unless explicitly approved.
- Brainstorm confirmed (yes/no): no

## Scope Contract
- In scope this sprint: Finalize discovery context, lock scope, and deliver one testable vertical slice.
- Out of scope this sprint: Cross-cutting refactors and optional optimizations without direct sprint impact.
- Constraints (time/budget/compliance): Work within current stack (unknown stack); keep backward compatibility and auditability.
- Dependencies and owners: Assign owner for backend, frontend, QA, and release sign-off before implementation.

## Architecture Snapshot
- System boundaries: Xcode project (XKey.xcodeproj, Swift, SwiftUI plus AppKit) with two runtime surfaces. (1) XKey: a menu-bar app that installs a CGEvent tap and injects replacement keystrokes or text into the focused app. It uses the Accessibility API and has special handlin...
- Core modules/services: Vietnamese engine (XKey/Core/Engine): Typing-method state machine for Telex/VNI/Simple Telex, tone and diacritic pl...; Event handling / injection (XKey/EventHandling): CGEvent tap interception, backspace and text injection with per-app timing; A...; Input session and app policy (Shared/InputSession): Per-session buffer state and per-app policy runtime shared by both modes (e.g...; App behavior detection (Shared/AppBehaviorDetector.swift): Detects focused app and overlays (Spotlight, Raycast, browsers, terminals) to...; Accessibility helper (Shared/AXHelper.swift): Reads focus, selection and text via the AX API for translation, injection and...
- Data model and storage: Infer from repository modules and migrations; validate authoritative schema and ownership.
- External integrations: No startup command confirmed yet; confirm canonical dev/test command with owner.
- Security and privacy assumptions: Assume least privilege and PII-safe defaults; validate auth, secrets, and logging exposure.

## Execution Inputs For Workflow
- Plan entry criteria: Discovery reviewed, brainstorm answers captured, and readiness gate passed for the scoped work.
- Test strategy: Run targeted automated tests for changed modules plus regression checks on the critical user journey.
- Release strategy: Deliver in small PRs, require passing tests/review, and stage rollout with rollback ready.
- Rollback strategy: Use revert-ready deployment plan and data-safe rollback steps before merge/release.

## Risks and Mitigations
- High risk 1: Fragile CGEvent injection and Accessibility behavior across macOS versions and apps -> Keep a per-app compatibility matrix with regression tests for the policy layer. Prefer the IMKit path where feasible....
- High risk 2: Privacy and security exposure of a keystroke-level tool -> Document that translation sends text off-device. Exclude secure fields and password managers. Audit logging so DebugL...
- Unknowns requiring research: Source code contents: no Swift file bodies were visible, only the file list, so module responsibilities are inferred...; Whether XKeyTests has real tests, what they cover, and whether the XKey scheme runs them.; Whether CI (GitHub Actions) exists, and how releases, notarization and the auto-update feed are produced.

<!-- AUTO-BRAINSTORM-START -->
## Brainstorming Questions (Answer Before /plan)

- 1. Who is the primary user persona, and what pain point must be solved first?
- 2. Which user journey is highest priority for this sprint (from entry to successful outcome)?
- 3. What is the confirmed local startup path (dependencies, env setup, run command) that we should standardize?
- 4. Which modules own business-critical logic among: XKey/UI, XKey/Core, XKey/Assets.xcassets?
- 5. Can you clarify: Source code contents: no Swift file bodies were visible, only the file list, so module responsibilities are inferred from names and the README.?
- 6. Can you clarify: Whether XKeyTests has real tests, what they cover, and whether the XKey scheme runs them.?
- 7. Can you clarify: Whether CI (GitHub Actions) exists, and how releases, notarization and the auto-update feed are produced.?
- 8. How should we mitigate this first critical risk: Fragile CGEvent injection and Accessibility behavior across macOS versions and apps -> Keep a per-app compatibility matrix with regression tests for the policy layer. Prefer the IMKit path where feasible....?
<!-- AUTO-BRAINSTORM-END -->

## Checklist Before /cook
- [ ] Discovery decisions are explicit and conflict-free
- [ ] Scope and non-goals are agreed
- [ ] Acceptance criteria are testable
- [ ] Critical risks have owners

<!-- AUTO-DISCOVERY-START -->
## Auto Discovery Snapshot

- Generated: `2026-10-12T07:10:33+00:00`
- Source: `document-project deep`
- Root: `/Volumes/Projects/github-lufftran/xkey`
- Purpose guess (0.88): **Bộ gõ tiếng Việt hiện đại cho macOS**
- Architecture guess: Architecture appears mixed or monolithic; deeper scan may be required for precise boundaries.

### Top-level Structure

- `Shared`
- `Tools`
- `XKey`
- `XKey.xcodeproj`
- `XKeyIM`
- `XKeyTests`
- `docs`
- `plans`

### Detected Stacks

- Unknown

### Dominant Languages

- Unknown

### Serious Findings

- [medium] No obvious automated test footprint found.

### Next Actions

- Update docs/project-context.md using this scan output before /plan
- Create a targeted plan with /plan referencing this scan

### Startup Hints

- No startup hints detected

### Repository Index

- `XKey/UI`: frontend-or-client-surface (files: 43)
- `XKey/Core`: unknown (files: 28)
- `XKey/Assets.xcassets`: unknown (files: 21)
- `Shared/InputSession`: unknown (files: 12)
- `XKey/Utilities`: unknown (files: 12)
- `XKeyIM/Assets.xcassets`: unknown (files: 10)
- `plans/261012-1409-workflow-init`: unknown (files: 10)
- `XKey/EventHandling`: unknown (files: 7)
- `XKey/App`: frontend-or-client-surface (files: 6)
- `docs/superpowers`: unknown (files: 4)
- `XKey.xcodeproj/xcshareddata`: unknown (files: 3)
- `XKey/InputMethod`: unknown (files: 2)

### AI Synthesis

- overall_confidence: 0.74 (gate_pass=False)
- purpose: XKey is a native macOS Vietnamese typing method (Telex, VNI, Simple Telex, auto-detect) that replaces unmaintained or incompatible Vietnamese IMEs on recent macOS (12+). It converts keystrokes into Vietnamese characters in any app. It adds productivity features: macros, quick typing, spell-check with personal dictionary, per-app smart switch, text conversion tools (case, code table, strip diacritics), and hotkey translation. It runs locally and collects no user data. This repo looks like a fork or personal checkout (git user LuffyTran) of the upstream xmannv/xkey project.
- architecture: Xcode project (XKey.xcodeproj, Swift, SwiftUI plus AppKit) with two runtime surfaces. (1) XKey: a menu-bar app that installs a CGEvent tap and injects replacement keystrokes or text into the focused app. It uses the Accessibility API and has special handling for app quirks (Spotlight, Raycast, terminals, browsers). (2) XKeyIM: an experimental Input Method Kit (IMKInputController) bundle installed in ~/Library/Input Methods, with a different bundle id (com.codetay.inputmethod.XKey). It gives flicker-free composition and shares the engine code. A third layer, Shared/, is compiled into both targets. It holds the input session and app-policy runtime (Shared/InputSession), AX helpers, app behavior detection, tap environment/event source, debug logging and translation languages. XKey/Core/Engine holds the Vietnamese engine (VNEngine, spell checker, ConvertTool, code tables). XKey/EventHandling holds the injection strategies. XKey/UI holds the SwiftUI settings, convert-tool and debug windows. XKey/Utilities and XKey/App (AppDelegate) cover lifecycle and helpers. Integrations: macOS Accessibility, Input Monitoring, Services menu, global hotkeys, App Group shared settings, online translation providers (Google, Tencent, Volcano), auto-update and Homebrew cask distribution, and a bundled GPL Vietnamese dictionary. Versioning lives in Version.xcconfig. build_release.sh packages releases. XKeyTests holds unit tests. The docs, plans and superpowers folders hold workflow and design notes, not runtime code.

### Brainstorm Questions

- 1. Who is the primary user persona, and what pain point must be solved first?
- 2. Which user journey is highest priority for this sprint (from entry to successful outcome)?
- 3. What is the confirmed local startup path (dependencies, env setup, run command) that we should standardize?
- 4. Which modules own business-critical logic among: XKey/UI, XKey/Core, XKey/Assets.xcassets?
- 5. Can you clarify: Source code contents: no Swift file bodies were visible, only the file list, so module responsibilities are inferred from names and the README.?
- 6. Can you clarify: Whether XKeyTests has real tests, what they cover, and whether the XKey scheme runs them.?
- 7. Can you clarify: Whether CI (GitHub Actions) exists, and how releases, notarization and the auto-update feed are produced.?
- 8. How should we mitigate this first critical risk: Fragile CGEvent injection and Accessibility behavior across macOS versions and apps -> Keep a per-app compatibility matrix with regression tests for the policy layer. Prefer the IMKit path where feasible....?

<!-- AUTO-DISCOVERY-END -->
