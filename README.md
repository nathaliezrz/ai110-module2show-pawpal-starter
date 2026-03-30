# PawPal+ (Module 2 Project)

You are building **PawPal+**, a Streamlit app that helps a pet owner plan care tasks for their pet.

## Scenario

A busy pet owner needs help staying consistent with pet care. They want an assistant that can:

- Track pet care tasks (walks, feeding, meds, enrichment, grooming, etc.)
- Consider constraints (time available, priority, owner preferences)
- Produce a daily plan and explain why it chose that plan

Your job is to design the system first (UML), then implement the logic in Python, then connect it to the Streamlit UI.

## What you will build

Your final app should:

- Let a user enter basic owner + pet info
- Let a user add/edit tasks (duration + priority at minimum)
- Generate a daily schedule/plan based on constraints and priorities
- Display the plan clearly (and ideally explain the reasoning)
- Include tests for the most important scheduling behaviors

## Getting started

### Setup

```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

### Suggested workflow

1. Read the scenario carefully and identify requirements and edge cases.
2. Draft a UML diagram (classes, attributes, methods, relationships).
3. Convert UML into Python class stubs (no logic yet).
4. Implement scheduling logic in small increments.
5. Add tests to verify key behaviors.
6. Connect your logic to the Streamlit UI in `app.py`.
7. Refine UML so it matches what you actually built.

### Smarter Scheduling
1. Added a method to sort all tasks by hour, ascending or descending
2. Added a method to filter tasks by pet name, completion status, or both
3. Added a recurrence field to Task to support daily and weekly repeating tasks
4. Added a due_date field to Task to track which calendar date a task belongs to
5. Updated mark_complete() to automatically schedule the next occurrence for recurring tasks
6. Added a method to detect scheduling conflicts and return warning messages for same-time collisions

### Testing PawPal+
To run tests: python -m pytest
Confidence Level: 4 Stars

The tests verify that tasks sort correctly by hour regardless of the order they were added, and that the sort can be reversed. They also confirm that completing a recurring task automatically schedules the next occurrence on the right date, while one off tasks do not. They also check that the scheduler correctly identifies when two or more tasks are booked at the same time, whether for the same pet or different pets, and that tasks on different dates or hours are never flagged as conflicts.

### Features

1. Sort by time — Tasks can be sorted chronologically by their scheduled hour, ascending or descending, regardless of the order they were added.

2. Filter by pet or status — The scheduler can return a targeted subset of tasks filtered by pet name, completion status, or both at once.

3. Daily and weekly recurrence — Tasks marked with a recurrence type automatically schedule their next occurrence when completed — one day later for daily tasks, seven days later for weekly tasks.

4. Conflict detection — The scheduler scans all tasks grouped by date and hour, and returns warnings when two or more tasks are booked at the same time slot, distinguishing between same-pet and cross-pet overlaps.

5. Structured conflict data for the UI — Alongside plain-text warnings, the scheduler exposes conflict details as structured records so the interface can render them as interactive cards with a table of clashing tasks and a resolution tip.

6. Due date tracking — Every task carries a calendar date so recurring tasks, filters, and conflict checks are all scoped to the correct day rather than treating all tasks as belonging to one undated pool.

7. Back-reference from task to pet — Each task holds a reference to the pet it belongs to, enabling the scheduler to identify ownership without traversing the full owner-pet-task hierarchy on every lookup.

### Demo
<a href="/course_images/ai110/pawpal_final.png" target="_blank"><img src='/course_images/ai110>