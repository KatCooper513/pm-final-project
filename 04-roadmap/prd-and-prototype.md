# One-Click Compliance Checklist, Simplified PRD (RouteLogic)

**Author:** Me · **Status:** Draft · **Target:** High-Fidelity Prototype · **Persona:** Driver

## 1. The Big Picture
- **Vision:** To eliminate workarounds, by adding Driver Alert Notifications.
- **Press release:** Today, RouteLogic launched Driver Alert Notifications in their app which will replace the texts/calls dispatchers currently use to reach drivers. This will route drivers back into the app for route/schedule-change alerts and keep them on the correct route, not losing valuable time on stale routes. 

This change will make the process streamline the process and it will be more efficient for the driver, dispatchers and customers. Retaining customers and employees.
- **Success metric:** Drivers are no longer using manual workarounds because the app is successfully working.
- **Guardrail:** Accounts citing complexity as churn reason, currently 4 of 5 accounts vs the previous 1 of 8 accounts two years prior.

## 2. The Details
### User stories
- As a Driver, I want to get push notifications on route/schedule-changes, so that I am on the correct, active route.
### Screens to build
- 1. Entry Point (Lock Screen / Notification Banner)
- 2. Feature Core (In-App Alerts / Schedule View)
- 3. Success / Confirmation
### Functional requirements
- The system must,
- 1. A push notification is generated for 100% of route/schedule-change events, with no manual trigger required.
- 2. Notifications deliver identically across foreground, background, and closed-app states (no degraded path for closed app).
- 3. Every notification includes a non-empty "what changed" field.
- 4. Every notification includes a non-empty "effective time" field.
- 5. A delivery log entry (sent/delivered status) is created for every alert and is queryable by dispatch.
- Alerts fire only for the 3 pilot accounts — no cross-account delivery in this build.
### Smart behaviors (Situation → Outcome)
- Driver's device is offline when the change occurs -> Alert queues and delivers on reconnect
- Multiple changes fire in quick succession -> Each alert delivers independently (no batching/dedup in this pilot) — content must stay specific enough that two alerts never look like duplicates
- Driver has quiet hours enabled and change occurs during them -> Alert is suppressed until quiet hours end (Should Have)
- Dispatch checks the delivery log before the driver acknowledges -> Log shows "Sent," not "Confirmed" — read/ack state is tracked separately so dispatch is never shown false confidence
- Driver has disabled OS-level push permissions -> App shows the pending alert as an in-app banner the next time it's opened — it is not silently dropped
### Technical constraints
- • No external push service integration — simulate delivery with an in-app triggered banner/toast for the prototype.
- • No login or auth flow — a single hardcoded driver identity for the demo.
- • No backend or persistence layer — route/schedule-change events are triggered by a mock action in the prototype, not a real event source.
- State managed with React useState only — no external state libraries, no API calls.

## 3. The Logistics
### Features out
- • Two-way reply or chat from inside the notification. That's a messaging feature, not an alert feature — real scope creep risk given the team size.
- • SMS/email fallback channel. Building a fallback that mimics the exact workaround you're trying to eliminate defeats the point; if push delivery is unreliable, that's a Must Have bug, not a feature to build around.
- • Coordinator-side custom alert-routing rules. Different persona, different pilot — same reasoning that cut B4/B8/B10 from this pilot applies here.
- • Any AI-generated or summarized alert copy. Same complexity-guardrail line drawn for B1 — keep the trigger-to-content mapping deterministic for the pilot.
- • Cross-account/fleet-wide br
### Edge cases & safety guard
- • Driver denies push permission at the OS level → alert must still surface as an in-app banner on next open, never silently disappear.
- • A route is reverted before the driver opens the app → the in-app alerts/schedule view must reflect the current, reverted state — not the original alert description.
- • A system retry fires the same event twice → dedupe by event ID so the driver never sees the same change reported as two separate alerts.
- Safety/hallucination guard: alert copy is assembled only from structured event fields (what changed, effective time) — never free-text or model-generated. There is no summarization step, which removes the hallucination surface by construction rather than by review.
### Decision log
- 1. Rejected SMS/email fallback, even though it would reduce delivery risk, because a fallback channel would quietly recreate the exact text/call workaround this feature exists to eliminate.
- Rejected AI-generated alert copy, despite lower authoring effort, to keep the pipeline deterministic and avoid the same complexity/churn-guardrail risk already flagged and cut on the Smart Daily Report Auto-Fill feature.
### Evals
- 1. Content completeness: % of alerts where both "what changed" and "effective time" fields are populated — target 100% (any blank field is a hard fail).
- 2. Time-on-task: time from notification tap to the driver being able to identify the changed detail in-app — target under 5 seconds without additional navigation beyond the alerts/schedule view.
- 3. Safety trigger: 0 instances, across QA passes, of the in-app alerts/schedule view showing stale/reverted route data — tracked as a binary pass/fail gate, not a percentage.

## MoSCoW scope
- **Must:** Core Requirement 1 -  Push notification triggered on route/schedule change events. Remove this and there's no alternative to the text/call — the feature doesn't exist.; Core Requirement 2 -  Delivery even when the app is backgrounded or closed. Remove this and it only works for drivers already in the app — exactly the drivers who don't need it. It has to reach the ones currently relying on a phone call.; Core Requirement 3 -  Content specific enough to act on without calling dispatch to confirm (what changed, effective when). Remove this and every alert generates a follow-up call anyway — the old workaround survives inside the new feature.; Core Requirement 4 -  Delivery confirmation/logging visible to dispatch that the alert was sent. Remove this and dispatchers won't trust the channel under pressure — they'll fall back to calling "just in case," which quietly kills adoption from the other side.
- **Should:** Valuable addition 1 - Basic notification-type opt-out (e.g. mute non-urgent alerts) — protects against alert fatigue becoming its own churn risk.; Valuable addition 2 - Quiet-hours suppression during logged rest periods — a guardrail-adjacent protection, cheap to add, avoids the feature itself becoming a driver complaint.; Valuable addition 3 -  Lightweight in-app acknowledgment ("Got it") that closes the loop back to dispatch without a call — extends the same win B1 relies on.; COULD HAVE (V2)
- **Could:** Nice to have 1 -  Adaptive pre-fill that learns from a driver's past manual corrections.; Nice to have 2 - Historical view of previously submitted checklists.; Nice to have 3 - Completion streak/indicator.; Multi-language field labels.
- **Won't (now):** Out of scope 1 - Full audit-trail PDF export — that's B9's job, and B9 is explicitly deprioritized this pilot. Don't let it creep in here.; Out of scope 2 -Manager/Coordinator-facing visibility into completion status — different persona (B4/B8 territory), already cut from this pilot on purpose.; Out of scope 3 -AI-generated or AI-summarized field population beyond simple record lookup — this is exactly the "does everything" complexity you flagged as a churn-guardrail risk on B2. Keep B1's auto-fill dumb and deterministic.; Out of scope 4 -A configurable compliance rules engine — ship against the existing rule set as-is; rule authoring is a different, much bigger project.; Out of scope 5 -Full native offline mode — the retry queue (Should Have) covers the pilot's realistic failure case; don't over-build for 3 accounts.

---
**Builder hook:** Build a working prototype based on this PRD. Use the User Story as the core flow, Functional Requirements as build constraints, and prioritize speed and clarity over visual complexity.
