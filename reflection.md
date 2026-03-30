# PawPal+ Project Reflection

## 1. System Design

**a. Initial design**

- Briefly describe your initial UML design.
- What classes did you include, and what responsibilities did you assign to each?

UML Design / Core User Actions:
- Add a pet
    - Pet holds name, breed, and a list of Task objects
    - Methods: add_pet, remove_pet (on Owner), add_task, remove_task (on Pet)
- Insert pet tasks
    - Task represents a single activity with a description, time, frequency, and completion status
    - Task owns its own state and behavior: mark_complete, reset
    - Task management methods (add, remove) belong to Pet, since Pet owns its task list
- View and manage tasks across pets
    - Owner provides get_all_tasks() to aggregate tasks across all pets
    - Scheduler is the central "brain" that retrieves, organizes, and manages tasks
    - Scheduler references Owner and exposes: get_tasks (per pet), organize_tasks, mark_complete, get_pending_tasks

**b. Design changes**

- Did your design change during implementation?
- If yes, describe at least one change and why you made it.

When asking Claude for missing relationships or logical bottlenecks, it mentioned that Task had no reference to pet, which is integral to the way pawpal+ works. Furthermore, it pointed out that was no validation when the get_task() method, in which pet is a parameter, that pet belonged to the owner. Since I agreed that these were unintentional issues, I fixed them before begining to code the logic.

---

## 2. Scheduling Logic and Tradeoffs

**a. Constraints and priorities**

- What constraints does your scheduler consider (for example: time, priority, preferences)?

The scheduler considers time (each task has a scheduled hour and due date), recurrence (daily or weekly repetition), and completion status (whether a task is still pending). It uses these to sort tasks chronologically, filter, and detect when two tasks compete for the same time slot.

- How did you decide which constraints mattered most?

Time came first because a pet owner's primary need is knowing when to act on a task. A schedule without any ordering would just be a list.

**b. Tradeoffs**

- Describe one tradeoff your scheduler makes.

One tradeoff my scheduler makes is having an algorithm with a longer runtime O(nlogn) instead of O(n) in order to keep the warnings sorted by the time of confliction.

- Why is that tradeoff reasonable for this scenario?

I believe this tradeoff is reasonable as users of pawpal+ would typically not have a very large input size of tasks (generally less than 100), so keeping the UI clean is more important that saving a bit of running time.

---

## 3. AI Collaboration

**a. How you used AI**

- How did you use AI tools during this project (for example: design brainstorming, debugging, refactoring)?

AI tools helped with brainstorming the class design, drafting and refining methods like detect_conflicts() and sort_by_time(), generating the test suite, and connecting the backend logic to the Streamlit UI. I used them as a coding partner throughout!

- What kinds of prompts or questions were most helpful?

Specific, direct prompts worked best. The less the AI had to guess, the more useful its output was.

**b. Judgment and verification**

- Describe one moment where you did not accept an AI suggestion as-is.

When initially looking at main.py, I asked claude a clarifying question, and it attempted to rewrite methods. However, I wanted to look at the skeleton code first, so I did not accept this suggestion.

- How did you evaluate or verify what the AI suggested?

I verified what the AI would sugguest based on my own questions. If I asked for something specific related to one class, but the AI attempted to alter another, then I would investigate and see if it was necessary and acceptable.

---

## 4. Testing and Verification

**a. What you tested**

- What behaviors did you test?

The tests cover task sorting by hour, daily and weekly recurrence creating the correct next occurrence, conflict detection for same-pet and cross-pet time clashes, and edge cases like empty schedules and tasks at the same hour on different dates.

- Why were these tests important?

These tests matter because the core value of a scheduler is its correctness.

**b. Confidence**

- How confident are you that your scheduler works correctly?

I would say that my confidence is a 4/5 because although I performed a lot of tests, I may have missed some edge case.

- What edge cases would you test next if you had more time?

I tested all the edge cases I thought of. However, if I had more time, I would definately dedicate it to testing out the app more and attempting to find bugs.

---

## 5. Reflection

**a. What went well**

- What part of this project are you most satisfied with?

I would say the conflict detection. Its able to  handle both same pet and cross pet clashes, which is a feature that was not too easy to implement!

**b. What you would improve**

- If you had another iteration, what would you improve or redesign?

I'd spend more time improving the UI. The backend logic is solid but the Streamlit interface is still mostly bare.

**c. Key takeaway**

- What is one important thing you learned about designing systems or working with AI on this project?

I learned that its very important to have a detailed map of what you want, especially when using AI. If you are not clear, AI will fill the gaps, and that's what often leads to bugs.
