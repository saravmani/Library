
### Sample Custm message state  class
```py
from typing import Annotated
from langgraph.graph import MessagesState
from langchain_core.messages import AnyMessage
from langgraph.graph.message import add_messages

# Define a custom TypedDict that includes a list of messages with add_messages reducer
class CustomMessagesState(TypedDict):
    messages: Annotated[list[AnyMessage], add_messages]
    added_key_1: str
    added_key_2: str
    # etc

# Use MessagesState, which includes the messages key with add_messages reducer
class ExtendedMessagesState(MessagesState):
    # Add any keys needed beyond messages, which is pre-built 
    added_key_1: str
    added_key_2: str
    # etc
```

this both are same CustomMessagesState  and ExtendedMessagesState


### To update the messages use **ID**
```py
# Initial state
initial_messages = [AIMessage(content="Hello! How can I assist you?", name="Bot", id="1"),
                    HumanMessage(content="I'm looking for information on marine biology.", name="Sarav", id="2")
                   ]

# New message to add
new_message = HumanMessage(content="I'm looking for information on whales, specifically", name="Lance", id="2")

# Test
add_messages(initial_messages , new_message)
```


### To Remove
```py
from langchain_core.messages import RemoveMessage
delete_messages = [RemoveMessage(id=m.id) for m in initial_messages[:-2]]

```

