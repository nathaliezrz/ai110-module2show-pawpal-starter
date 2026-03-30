# PawPal+ Project Reflection

## 1. System Design

**a. Initial design**

- Briefly describe your initial UML design.
- What classes did you include, and what responsibilities did you assign to each?

Core User Actions:
- Add a pet
    - Pet should hold name, breed, and a list of assigned tasks
    - Task management lives on Pet, since Pet owns its task list
    - Methods: addPet, deletePet (on Owner), insertTask, removeTask, changeAmount (on Pet)
- Insert their availability schedule
    - Availability should hold a list of blocked hours (hours the owner is unavailable)
    - Availability is owned by Owner, and DailyPlan accesses it through Owner
    - Methods: addHours, removeHours, alterHours
- Insert Pet Tasks
    - Pet tasks have a type (walk, feeding, grooming, playing) and a daily count
    - TaskType is an enumeration to enforce valid task options
    - Task management methods (insert, remove, change amount) belong to Pet, not PetTask
    - PetTask only holds its own data: type and dailyCount
- View a daily plan that accounts for tasks and availability
    - DailyPlan references Owner (for availability) and Pet (for tasks), keeping the ownership chain intact
    - After generation, the plan stores scheduledSlots (the ordered plan) and an explanation (why it was formatted that way)
    - Methods: generate

**b. Design changes**

- Did your design change during implementation?
- If yes, describe at least one change and why you made it.

---

## 2. Scheduling Logic and Tradeoffs

**a. Constraints and priorities**

- What constraints does your scheduler consider (for example: time, priority, preferences)?
- How did you decide which constraints mattered most?

**b. Tradeoffs**

- Describe one tradeoff your scheduler makes.
- Why is that tradeoff reasonable for this scenario?

---

## 3. AI Collaboration

**a. How you used AI**

- How did you use AI tools during this project (for example: design brainstorming, debugging, refactoring)?
- What kinds of prompts or questions were most helpful?

**b. Judgment and verification**

- Describe one moment where you did not accept an AI suggestion as-is.
- How did you evaluate or verify what the AI suggested?

---

## 4. Testing and Verification

**a. What you tested**

- What behaviors did you test?
- Why were these tests important?

**b. Confidence**

- How confident are you that your scheduler works correctly?
- What edge cases would you test next if you had more time?

---

## 5. Reflection

**a. What went well**

- What part of this project are you most satisfied with?

**b. What you would improve**

- If you had another iteration, what would you improve or redesign?

**c. Key takeaway**

- What is one important thing you learned about designing systems or working with AI on this project?
