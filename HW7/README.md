# Let's create (a corpus for) Chatbots!

In this homework, you will form a team of 4-5 people (this will be the team for your project) and create a corpus for training your chatbot. Note: this assignment is worth 5 points in additional to the other 7 assignment (HW0-HW6). Thus, in total assignments are worth 40 points.

## Choose your destiny
One way to categorize chatbots is by the purpose of the conversation. 

1. **Task-specific chatbots** are designed with a particular task in mind, such as ordering a pizza, or doing bank transactions. 
2. **Open domain chatbots** are designed for handling any kind of dialogues. An application would be a conversational agent such as *woebot.io*

Decide within your team which type would you prefer, and what kind of domain/application would you build your chatbot for. **Your bot must be in Thai**

To get ideas, https://botlist.co/ is a collection of bots. You can also consult these two awesome list of Chatbot related resources and tutorials. [awesome-list1](https://github.com/fendouai/Awesome-Chatbot) [awesome-list2](https://github.com/JStumpp/awesome-chatbots). Of note, [neural-chatbot-assignment-by-stanford](https://github.com/chiphuyen/stanford-tensorflow-tutorials/tree/master/assignments/chatbot) might be a good start for open domain chatbots.

## Make your corpora
After selecting the domain, list 100xN questions/utterances that can be given to the chatbot (where N is the number of people in your group). 

If your bot is a task-specific one, you must include a `intent tag` or `frame tag`. Examples of intent tagging are already provided in the intent classification assignment. `Frame tags` refer to tags that is related to the task at hand. For example, if you are making a bot for ordering pizza. You know that a complete order would have 1. the type of pizza 2. the amount of pizza 3. the address to deliver the pizza.

You might have the conversation do something like this

You: `I want to order <quantity>one<\quantity> <type>hawaiian pizza<\type>.`

Knowing that it is missing only the location the bot will ask

Bot: `Where do you want this delivered?`

You: `At <location>19th floor Building number 4 Chula Engineering<\location>`

This task can now be considered as PoS tagging and can be solved with any PoSTagger you like. The above example count as two utterances. 

If your bot is an open domain one, list 100xN question+answer pairs.

**Note that you might need more than 100xN utterances for your chatbot. Try to pick something simple.**

## Deliverables
Form a team on mycourseville, and submit your example sentences in an appropriate file. (5 points)
Be creative in creating your sentences as this will serve as a starting point for your project. 
