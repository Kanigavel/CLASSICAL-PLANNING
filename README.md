# ExpNo:10 Implementation of Classical Planning Algorithm
<h3>Name: Kanigavel M <h3>
  
<h3> Register Number: 212224240070 <h3>
  
# Algorithm or Steps Involved:
<ol>
  <li>Define the initial state</li>
  <li>Define the goal state</li>
  <li>Define the actions</li>
  <li>Find a <b>plan</b> to reach the goal state</li>
  <li>Print the plan</li>
</ol>

# Example - 1
```
initial_state = {'A': 'Table', 'B': 'Table'}
goal_state = {'A': 'B', 'B': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_Table': {'precondition': {'A': 'Table', 'B': 'B'}, 'effect': {'B': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
```
# Output:
```
['move_A_to_B']
```
# Example - 2
```
initial_state = {'A': 'Table', 'B': 'Table', 'C': 'Table'}
goal_state = {'A': 'B', 'B': 'C', 'C': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_C': {'precondition': {'A': 'B', 'B': 'Table', 'C': 'Table'}, 'effect': {'B': 'C'}},
    'move_C_to_Table': {'precondition': {'A': 'B', 'B': 'C', 'C': 'C'}, 'effect': {'C': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
```
# Output:
```
['move_A_to_B', 'move_B_to_C']
```

# Please Prepare Solution or Definition For the method find_plan(initial_state, goal_state, actions)
<h3>You Can use any of the searching Strategies for planning and executing a sequence of actions.<br> You can also look in to the Code given in the Repository.</h3>

<h3>PROGRAM </h3>
<hr>
 
```
        def is_goal_reached(state, goal_state):
            """Check if the goal is reached"""
            for key, value in goal_state.items():
                if key not in state or state[key] != value:
                    return False
            return True
        
        
        def preconditions_satisfied(state, preconditions):
            """Check if all preconditions are satisfied"""
            for key, value in preconditions.items():
                if key not in state or state[key] != value:
                    return False
            return True
        
        
        def apply_effects(state, effects):
            """Apply action effects to the current state"""
            new_state = state.copy()
            for key, value in effects.items():
                new_state[key] = value
            return new_state
        
        
        def find_plan(initial_state, goal_state, actions):
            """Find a plan using simple forward search"""
            state = initial_state.copy()
            plan = []
            visited = set()
        
            while not is_goal_reached(state, goal_state):
                for action, details in actions.items():
                    preconditions = details['precondition']
                    effects = details['effect']
        
                    if preconditions_satisfied(state, preconditions):
                        # Apply the action
                        state = apply_effects(state, effects)
                        plan.append(action)
                        # Avoid infinite loops
                        state_tuple = tuple(sorted(state.items()))
                        if state_tuple in visited:
                            return plan
                        visited.add(state_tuple)
                        break
                else:
                    # No valid action found — stop
                    print("No further actions can be applied.")
                    break
        
            return plan
        
        
        # ----------------------------
        # Example 1
        # ----------------------------
        print("Example 1 Output:")
        initial_state = {'A': 'Table', 'B': 'Table'}
        goal_state = {'A': 'B', 'B': 'Table'}
        
        actions = {
            'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
            'move_B_to_Table': {'precondition': {'A': 'Table', 'B': 'B'}, 'effect': {'B': 'Table'}}
        }
        
        plan = find_plan(initial_state, goal_state, actions)
        print(plan)
        
        # ----------------------------
        # Example 2
        # ----------------------------
        print("\nExample 2 Output:")
        initial_state = {'A': 'Table', 'B': 'Table', 'C': 'Table'}
        goal_state = {'A': 'B', 'B': 'C', 'C': 'Table'}
        
        actions = {
            'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
            'move_B_to_C': {'precondition': {'A': 'B', 'B': 'Table', 'C': 'Table'}, 'effect': {'B': 'C'}},
            'move_C_to_Table': {'precondition': {'A': 'B', 'B': 'C', 'C': 'C'}, 'effect': {'C': 'Table'}}
        }
        
        plan = find_plan(initial_state, goal_state, actions)
        print(plan)
        
         
 ```
  <hr>
<h3> OUTPUT <h3>
<img width="570" height="171" alt="image" src="https://github.com/user-attachments/assets/1fc15b52-603b-4d3c-be06-c0ae6d71285c" />

<h3>RESULT</h3>
Thus, the Classical Planning Algorithm was successfully implemented using Python.
