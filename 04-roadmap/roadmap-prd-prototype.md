# Feature Roadmap, Module 4 · RouteLogic Velocity

**Team:** 2 engineers + 1 designer + 1 CS lead

## Strategic anchors
- **Persona:** Driver
- **Primary metric:** Increase in Drivers using the Scheduling feature
- **Moment of misery:** Drivers and Dispatchers communicating outside the app as a necessary workaround.
- **Guardrail:** accounts citing complexity as churn reason.

## Scoring
| Feature | Value | Effort | Quadrant | Decision | Rationale |
|---|---|---|---|---|---|
| B1 One-Click Compliance Checklist | 4 | 2 | Quick Win | Now | Genuine driver time-save (14.6 min) with mostly plumbing/form work — low complexity risk, so it doesn't threaten the guardrail. Doesn't move the primary metric, but cheap enough to bundle into the pilot. |
| B2 Smart Daily Report Auto-Fill | 3 | 5 | Time Sinker | Cut | AI auto-fill is high engineering lift and higher failure surface — exactly the kind of "does everything" complexity that trips your churn guardrail. Doesn't touch Scheduling adoption or the misery moment. Cut for this pilot. |
| B3 Shift Handoff Wizard | 5 | 3 | Major Project | Next | Handoff is precisely where driver↔dispatcher coordination breaks down into off-app workarounds. 6.8 min/day saved is real driver friction, buildable by a 2-eng/1-designer team inside 4 weeks. |
| B4 Mobile-First Coordinator Dashboard | 1 | 5 | Time Sinker | Cut | Would meaningfully reduce off-app coordination, but it's Coordinator-facing (not the Driver persona), spans three modules, and is not a 4-week/2-engineer scope. Right initiative, wrong pilot. |
| B5 Step Progress Indicator | 2 | 1 | Fill-In | Later | Cosmetic. Ships if there's spare designer bandwidth in week 4; never displaces a Quick Win. |
| B6 Driver Alert Notifications | 5 | 3 | Major Project | Next | Directly attacks the Moment of Misery — push alerts replace the texts/calls dispatchers currently use to reach drivers. If route/schedule-change alerts route drivers back into the app, this is also the most direct lever on the Scheduling adoption metric. |
| B7 Contextual AI ETA Display | 2 | 2 | Fill-In | Later | Already live at 11% adoption — that's a demand signal, not a build problem. Low effort to iterate, but not worth pilot focus until you know why adoption is low. |
| B8 Fleet Analytics Manager View | 1 | 5 | Time Sinker | Cut | Classic Sales/Exec-preference feature — no driver benefit, no tie to the primary metric or misery moment. Ruthlessly deprioritize regardless of who's asking for it. |
| B9 Compliance Audit Trail Export | 2 | 2 | Fill-In | Later | Useful for CS/back-office relationships, cheap to ship, but doesn't touch the driver's daily friction or the metric you're pilot-scoring against. |
| B10 In-App Coordinator Training | 2 | 3 | Time Sinker | Cut | Coordinator-facing, not Driver. Marginal guardrail benefit (could reduce complexity-driven churn) but too indirect to earn scarce eng time this cycle. |

## Roadmap
### NOW, Pilot (4 weeks, 3 accounts)
- **B1 One-Click Compliance Checklist**, Genuine driver time-save (14.6 min) with mostly plumbing/form work — low complexity risk, so it doesn't threaten the guardrail. Doesn't move the primary metric, but cheap enough to bundle into the pilot.

### NEXT, GA Release (weeks 5-8)
- **B3 Shift Handoff Wizard**, Handoff is precisely where driver↔dispatcher coordination breaks down into off-app workarounds. 6.8 min/day saved is real driver friction, buildable by a 2-eng/1-designer team inside 4 weeks.
- **B6 Driver Alert Notifications**, Directly attacks the Moment of Misery — push alerts replace the texts/calls dispatchers currently use to reach drivers. If route/schedule-change alerts route drivers back into the app, this is also the most direct lever on the Scheduling adoption metric.

### LATER, backlog
- **B5 Step Progress Indicator**, Cosmetic. Ships if there's spare designer bandwidth in week 4; never displaces a Quick Win.
- **B7 Contextual AI ETA Display**, Already live at 11% adoption — that's a demand signal, not a build problem. Low effort to iterate, but not worth pilot focus until you know why adoption is low.
- **B9 Compliance Audit Trail Export**, Useful for CS/back-office relationships, cheap to ship, but doesn't touch the driver's daily friction or the metric you're pilot-scoring against.

### ✂ Cut List
- **B2 Smart Daily Report Auto-Fill**, AI auto-fill is high engineering lift and higher failure surface — exactly the kind of "does everything" complexity that trips your churn guardrail. Doesn't touch Scheduling adoption or the misery moment. Cut for this pilot.
- **B4 Mobile-First Coordinator Dashboard**, Would meaningfully reduce off-app coordination, but it's Coordinator-facing (not the Driver persona), spans three modules, and is not a 4-week/2-engineer scope. Right initiative, wrong pilot.
- **B8 Fleet Analytics Manager View**, Classic Sales/Exec-preference feature — no driver benefit, no tie to the primary metric or misery moment. Ruthlessly deprioritize regardless of who's asking for it.
- **B10 In-App Coordinator Training**, Coordinator-facing, not Driver. Marginal guardrail benefit (could reduce complexity-driven churn) but too indirect to earn scarce eng time this cycle.
