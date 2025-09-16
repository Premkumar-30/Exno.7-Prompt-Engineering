# Exno.7 – Prompt Engineering

## Name :PREM KUMAR K

## Register no:212223060209

# Aim

Development of Python Code to Optimize Daily Schedule Dynamically Using AI.

# Algorithm: Write and implement Python code that prompts an AI tool to review the current agenda and reorganize the schedule when unexpected cancellations occur.

1. Accept input of remaining tasks and canceled tasks.
2. Prompt the AI with the updated agenda.
3. Ask AI to reorganize tasks for efficiency, considering:

   * Task urgency and deadlines
   * Opportunities for breaks/rest
   * Adding new productive activities in freed-up time
4. Generate a new optimized time-blocked schedule.
5. Present the updated schedule in a clear format.

## Aim

To help in dynamically rescheduling and prioritizing daily activities when changes occur in real-time.

## Procedure / Algorithm:

### Step 1: Define the Use Case

Use Case: **Daily Agenda Optimization**.
Whenever scheduled tasks are canceled, AI should reorganize the agenda and suggest:

* New task order for efficiency
* Urgent priorities
* Opportunities for rest or productive fillers

### Step 2: Set Up AI API Access

```python
import os
import openai

OPENAI_API_KEY = os.getenv("OPENAI_API_KEY")
```

### Step 3: Write a Function to Prompt the AI

```python
def optimize_schedule(remaining_tasks, canceled_tasks):
    openai.api_key = OPENAI_API_KEY
    
    prompt = f"""
    I had a couple of scheduled tasks canceled today. 
    Here are my remaining tasks: {remaining_tasks}. 
    The following tasks were canceled: {canceled_tasks}. 
    
    Please reorganize my day to optimize time and energy. Consider:
    1. Adjusting task order for efficiency
    2. Highlighting urgent priorities
    3. Suggesting breaks/rest
    4. Recommending new productive tasks if possible
    Return the updated schedule in a clear, time-blocked format.
    """
    
    response = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[{"role": "user", "content": prompt}]
    )
    return response['choices'][0]['message']['content']
```

### Step 4: Provide Sample Input

```python
remaining = [
    "Finish SQL assignment (due tomorrow, ~2 hrs)",
    "Team call (3:00–3:30 PM)",
    "Gym workout (~1 hr)",
    "Revise notes for exam (~1.5 hrs)"
]

canceled = [
    "12:00–1:00 PM client meeting",
    "5:00–6:00 PM project review"
]

print(optimize_schedule(remaining, canceled))
```

### Step 5: Sample Output (AI Response)

```
Updated Agenda:  
12:00–12:30 → Quick lunch + relaxation  
12:30–2:30 → SQL assignment (priority: deadline tomorrow)  
3:00–3:30 → Team call (fixed)  
3:30–4:30 → Exam revision (fresh focus after call)  
4:30–5:30 → Gym workout (energy boost)  
5:30–6:00 → Review SQL briefly / check emails
```

## Result

The Python code successfully:

1. Accepted input of remaining and canceled tasks.
2. Connected with AI to reorganize the schedule.
3. Generated an optimized, time-blocked daily agenda.
4. Suggested both productive use of time and opportunities for rest.

