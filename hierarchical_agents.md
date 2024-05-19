## Hierarchical agents
There is probably a lot of literature and various github projects on the topic of building agents from LLMs, here I am just trying to think about the hierarchical execution of tasks without looking at what other people have tried and proposed.

```python
class Task:
    def __init__(self, goal, parent):
        self.parent = parent
        self.goal = goal
        self.solved_criterion = self.get_solved_criterion()
        self.subtasks = self.get_subtasks()
        
    def get_solved_criterion(self):
        prompt = "The current goal is: {self.goal}, this is a subgoal
        of a larger goal of {self.parent.goal}. We need to
        specify requirements very precisely what would count as a situation
        where this goal is actually reached. When we think
        we have solved the task we can use the requirement to
        determine if we indeed solved the task. Please
        give a list of appropriate requirements. If the goal
        is one that could be tested computationlly such as
        checking the state of the system such that specific
        tests are passed, add the tag "computational" and sketch
        how this test might be constructed."
        self.solved_criterion = llm.completion(prompt)

    def get_subtasks(self):
        prompt = "The current goal is: {self.goal}, this is a subgoal
        of a larger goal of {self.parent.goal}. We need to determine
        which subgoals/steps need to be solved to reach this state.
        Please give a list of steps to reach this goal. Each item
        in the list should have the following format:
        <item number>: Because <reason> we need to <step description>.
        The goal of the step will be to <step goal>.
        list_string = llm.completion(prompt)
        steps_tuples = [(step desc i, step goal i)]
        for (step_desc, step_goal) in steps_tuples:
```

    