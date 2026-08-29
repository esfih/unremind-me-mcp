# Tools

16 tools, grouped by what an agent is trying to do.

### Getting oriented

| Tool | What it does |
|---|---|
| `orient` | START HERE at the beginning of a working session, and after any long gap. |
| `get_guide` | Fetches detailed guidance for one kind of work — scheduling, delegating, capturing tasks well, setup, or the context-tag vocabulary. |
| `save_progress` | Records what you just did and what should happen next, so a future session (yours or another agent's) can resume instead of starting cold. |

### Reminders (Unreminders)

| Tool | What it does |
|---|---|
| `list_unreminders` | Lists the signed-in user's own Unreminders (tasks), soonest due first. |
| `create_unreminder` | Submits a new Unreminder to the user for approval. |
| `update_unreminder` | Updates fields on one of the signed-in user's own Unreminders. |
| `complete_unreminder` | Marks one of the signed-in user's own Unreminders as completed. |
| `list_context_tags` | Lists every context tag UnRemind understands, grouped (time, energy, type, device, connectivity, movement, people, payment, paymentAmount). |

### Delegated work

| Tool | What it does |
|---|---|
| `list_my_tasks` | Lists Unreminders the user has ASSIGNED TO YOU as an agent to carry out -- your work queue, not the user's own list. |
| `get_task` | Full brief for one task assigned to you: the complete notes, due date, context tags, place, the owner's standing instructions for you, and the…. |
| `update_task_status` | Reports progress on a task assigned to you, with a comment the user will see in the task history. |
| `comment_on_task` | Adds a comment to a task assigned to you without changing its status. |
| `ask_owner` | Hands a task back to the user with a question, when you cannot proceed without a decision or information only they have. |

### Planning

| Tool | What it does |
|---|---|
| `check_conflicts` | Checks whether a proposed time collides with the user's real Google Calendar meetings or with other Unreminders already due around then, and offers…. |
| `review_workload` | The state of the user's commitments: what is overdue, what is due soon, and what has no due date at all. |
| `suggest_next_task` | Suggests what to work on right now, given how much time the user has. |
