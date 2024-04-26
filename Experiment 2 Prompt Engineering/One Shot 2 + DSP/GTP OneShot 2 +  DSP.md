# GTP OneShot 2 + DSP

## Prompt 

    I want you to create a Business Process Model and Notation (BPMN) model for the process described below. Return the model in the following format: task nodes as Task [words], parallel gateways as AND, exclusive gateways as XOR, and arcs as ->.
    You should number the gateways. 
    You may also label the outgoing arcs of an exclusive gateway to denote the decision criterion, like XOR Gateway 1 -> Condition (action choice). 
    Additionally, provide a mapping of actors to activities, in the format Actor: [activity1, ...]

    Process description: A small company manufactures customized bicycles. Whenever the sales department receives an order, a new process instance is created. A member of the sales  department can then reject or accept the order for a customized bike. In the former case, the process instance is nished. In the latter case, the storehouse and the engineering department are informed. The storehouse immediately processes the part list of the order and checks the required quantity of each part. If the part is available in- hause, it is reserved. If it is not available, it is back-ordered. This procedure is repeated for each item on the part list. In the meantime, the engineering department prepares everything for the assembling of the ordered bicycle. If the storehouse successfully reserved or back-ordered every item of the part list and the preparation activity has nished, the engineering department assembles the bicycle. Afterwards, the sales department ships the bicycle to the customer and nishes the process instance

    Hint: A good example of formatting is as follows,
    Start Event O -> Task [Receives an Order]
    Task [Receives an Order] -> XOR Gateway 1
    XOR Gateway 1 -> Condition (Order Rejected)
    XOR Gateway 1 -> Condition (Order Accepted)
    Condition (Order Rejected) -> Event End O
    Condition (Order Accepted) -> Task [Inform Storehouse and Engineering Department]


## Response
Start Event O -> Task [Receive Order]
Task [Receive Order] -> XOR Gateway 1
XOR Gateway 1 -> Condition (Order Rejected)
XOR Gateway 1 -> Condition (Order Accepted)
Condition (Order Rejected) -> Event End O
Condition (Order Accepted) -> Task [Inform Storehouse and Engineering Department]
Task [Inform Storehouse and Engineering Department] -> AND Gateway 2
AND Gateway 2 -> Task [Process Part List]
AND Gateway 2 -> Task [Prepare for Assembly]
Task [Process Part List] -> XOR Gateway 3
XOR Gateway 3 -> Condition (All Parts Reserved/Back-ordered)
XOR Gateway 3 -> Task [Repeat Process for Next Part]
Task [Repeat Process for Next Part] -> XOR Gateway 3
Condition (All Parts Reserved/Back-ordered) -> AND Gateway 4
Task [Prepare for Assembly] -> AND Gateway 4
AND Gateway 4 -> XOR Gateway 5
XOR Gateway 5 -> Condition (Parts Reserved)
XOR Gateway 5 -> Condition (Parts Back-ordered)
Condition (Parts Reserved) -> Task [Assemble Bicycle]
Condition (Parts Back-ordered) -> Task [Wait for Parts]
Task [Assemble Bicycle] -> Task [Ship Bicycle]
Task [Wait for Parts] -> Task [Check Part Availability]
Task [Check Part Availability] -> XOR Gateway 6
XOR Gateway 6 -> Condition (Part Available)
XOR Gateway 6 -> Condition (Part Unavailable)
Condition (Part Available) -> Task [Reserve Part]
Condition (Part Unavailable) -> Task [Back-order Part]
Task [Reserve Part] -> XOR Gateway 7
Task [Back-order Part] -> XOR Gateway 7
XOR Gateway 7 -> Condition (All Parts Checked)
Condition (All Parts Checked) -> AND Gateway 4
Task [Ship Bicycle] -> Event End O

Actor: 
- Sales Department: [Receive Order, Inform Storehouse and Engineering Department]
- Storehouse: [Process Part List, Check Part Availability, Reserve Part, Back-order Part, Ship Bicycle]
- Engineering Department: [Prepare for Assembly, Assemble Bicycle]