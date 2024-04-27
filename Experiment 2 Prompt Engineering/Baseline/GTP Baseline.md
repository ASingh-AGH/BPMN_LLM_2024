# GTP Baseline
## Prompt 

    I want you to create a Business Process Model and Notation (BPMN) model for the process described below. Return the model in the following format: task nodes as words, parallel gateways as 
    AND, exclusive gateways as XOR, and arcs as>. You should number the gateways. You may also label the outgoing arcs of an exclusive gateway to denote the decision criterion, like XOR 
    Gateway-> (condition 1) Task. Additionally, provide a mapping of actors to activities, in the format actor: [activity1, ...]

    Process description: A small company manufactures customized bicycles. Whenever the sales department receives an order, a new process instance is created. A member of the sales 
    department can then reject or accept the order for a customized bike. In the former case, the process instance is nished. In the latter case, the storehouse and the engineering department are 
    informed. The storehouse immediately processes the part list of the order and checks the required quantity of each part. If the part is available in- hause, it is reserved. If it is not available, it is 
    back-ordered. This procedure is repeated for each item on the part list. In the meantime, the engineering department prepares everything for the assembling of the ordered bicycle. If the 
    storehouse successfully reserved or back-ordered every item of the part list and the preparation activity has nished, the engineering department assembles the bicycle. Afterwards, the sales 
    department ships the bicycle to the customer and nishes the process instance

## Response
Here's the BPMN model for the described process:

```
Sales Department (Task) -> XOR Gateway (1) -> (reject) End Event
                                     \
                                      -> Accept Order (Task) -> AND Gateway (2) -> Storehouse (Task) -> XOR Gateway (3) -> (all parts available) Engineering Department (Task) -> Assemble Bicycle (Task) -> Ship Bicycle (Task) -> End Event
                                                                               \
                                                                                -> (some parts not available) Storehouse (Task) -> XOR Gateway (4) -> (parts back-ordered) Engineering Department (Task) -> Assemble Bicycle (Task) -> Ship Bicycle (Task) -> End Event
```

Actor mapping:
- Sales Department: [Accept Order, Reject Order]
- Storehouse: [Process Part List]
- Engineering Department: [Prepare Assembly, Assemble Bicycle]
- Sales Department: [Ship Bicycle]
