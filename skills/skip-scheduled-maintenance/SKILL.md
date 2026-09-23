---
name: skip-scheduled-maintenance
description: Skip low-priority incidents during scheduled maintenance windows.
  Use this skill to automatically filter MEDIUM and LOW severity alarms that
  fire during planned maintenance for ProductA or ProductB infrastructure updates,
  avoiding unnecessary investigations for expected disruptions.
---

# Skip Scheduled Maintenance

Skip all incidents that meet BOTH criteria:

1. Severity is MEDIUM or LOW
2. The incident arrived during an active maintenance window

## Active Maintenance Windows

Check the maintenance calendar (updated weekly):
- ProductA infrastructure: Sundays 02:00-06:00 UTC
- ProductB infrastructure: Saturdays 22:00-02:00 UTC

## Do NOT skip

- HIGH or CRITICAL severity incidents (investigate regardless)
- Incidents affecting production customer traffic
- Incidents with cascading alarm correlation (3+ related alarms)
