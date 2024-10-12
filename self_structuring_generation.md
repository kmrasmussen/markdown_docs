The simplest way of using an LM to solve some task on an input I is "direct prompting" which would be the case where you give an input string p(I), the direct prompt, and the LM follows the prompt. In this case you are relying on the immediate capability of the model to impose its own executional structure. Direct prompting would include both zero- and k-shot.

For more a more advanced task you might not trust that the model is sufficiently good having the executional structure you try to impose in the prompt. Therefore you would apply a kind of "template prompting" where you have a fixed template like, for example AXBYCZ where A, B, C are fixed parts of the template and the model fills out X, Y, and Z, maybe with some limits on the length of generations. In this way you are guiding the model in a stricter way, keeping it on track.

For an even more advanced task you know that the problem need not be solved completely linearly and the generation might be so long that even with you template your are concerned about context-polution-confusion. You would then maybe use some kind of "recursive template prompting" be the case where you have some kind of template but parts of it would be solved without the rest of the context. For example:

Make a list of at most 10 steps for solving task I: X
*process X into list*
for subtask in list: answer = some_other_semiadvanced_prompt(subtask)

It is clear that with a turing-complete language like Python, we can make prompts of whatever computational complexity we want.

I could be that we should fine-tune language models to allow them to self-apply basic operations that aid them in structuring their generation execution.

Ideally the operations should be simple and powerful, easy to use for the models, easy to understand, make examples and training data for by humans, easy to make some kind of algorithmic analysis on. More than just being easy to use for models, they empower models, and that is probably the hardest part to get working: It should be such that it will be require as little intelligence on the side of the models to make the best choice in applying the operations and the least effort on the side of the human to tailor the hand-tailored parts of a prompt.

The best choice of operations for an LLM in terms of "self-controlling" its control flow is not necessarily the same as the best control flow in general because of the error-proneness and fallibility etc of the models. There is probably still a lot of research to be done on the ability for models to self-check etc, but..

Given the desiderata that we should focus on model empowerment, it might be worth plugging into the existing and evolving increase in coding capabilities (one of the areas where we can be more sure of evolving capabilities, see llama3.1 paper). While models are becoming more proficient in other languages, Python is going to be their main specialty for while I think. I could therefore make sense to train them to use a specific python library. They would then produce python code that is not run in the ordinary sense but is somehow applied to the flow itself.

To start being more concrete about this, I will start coming up with some examples. Here I will just note that the framework is (more) developed, I guess my examples will look quite useless, and ones that could be solved by direct prompting. Hopefully the abstraction will be powerful enough to enable more than this.

"What is the total number of letters in the names of all the scandiavian countries?"
This is not a question that needs self-controlled flow. Tuning the models to know that using Python is the best option to solve such a question and hard-coding a list of the names is good.
    There are however, things to talk about even here: Are there ways in which we can make it easier for models to make the right decisions for how to be super-sure of their answer: A good option in solving this task is to do things you might learn when studying physics etc: To write down a quick quess before hand so that you can compare afterwards, and if it is very different you might consider whether it is wrong. To ask yourself if there are any countries you would tend to forget. To try to come up with two different ways of getting to the answer and compare.

From this example, it seems that Self-control flow SCF is especially useful when we are dealing with problems that will rely on processing of larger chunks of natural text and also using larger chunks in further proccessing. Storing text in variables or registers.

While we could be concerned about parallelization and token-costs, I think the best option is for now to just view all desierata about this purely in terms of capability: Context-pollution confusion is when the model is solving a task and in the process generates so much text that it cannot get an overview both in terms of what knowledge it has gained and executively in terms of what it has been doing relates to what it has to do next. Having a non-polluted context benefits in solving tasks in ways that it does for humans certain forms of context-cleaning are probably more useful than for humans: Given the much lower intelligence, they are not as good at not deceiving themselves as we are. They can easily start believing their own answers. They need to hold themselves more accountable. If an instance A has an easier time making an offshoot B whose only responsibility is to make a certain check and which deliberately does not have some knowledge (already gained or which would be gained by A after making offshoot B) that would bias B in making such a check, then it might be easier to not avoid fooling itself.

I do not know if the following task is a challenge for frontier models, but even if not, I want a framework that also improves lesser models. At least gpt3.5 a year ago a prompt like this would not be successful always: "Fix typos and commas in this text <paragraph>". It would not only fix typos and commas, it would change wording.

"Fix typoes and commas in this text "While we could be concerned about parallelization and token-costs, I think the best option is for now to just view all desierata about this purely in terms of capability: Context-pollution confusion is when the model is solving a task and in the process generates so much text that it cannot get an overview both in terms of what knowledge it has gained and executively in terms of what it has been doing relates to what it has to do next. Having a non-polluted context benefits in solving tasks in ways that it does for humans certain forms of context-cleaning are probably more useful than for humans: Given the much lower intelligence, they are not as good at not deceiving themselves as we are. They can easily start believing their own answers. They need to hold themselves more accountable. If an instance A has an easier time making an offshoot B whose only responsibility is to make a certain check and which deliberately does not have some knowledge (already gained or which would be gained by A after making offshoot B) that would bias B in making such a check, then it might be easier to not avoid fooling itself."

Get list of sentences in paragraph
For each sentence in paragraph
    Write things you think are typos
    Write the things you think might be typos
    Reflect on whether they are not typos
    