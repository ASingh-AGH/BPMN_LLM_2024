# GTP OneShot

## Prompt 

    I want you to create a Business Process Model and Notation (BPMN) model for the process described below. Return the model in the following format: task nodes as words, parallel gateways as 
    AND, exclusive gateways as XOR, and arcs as>. You should number the gateways. You may also label the outgoing arcs of an exclusive gateway to denote the decision criterion, like XOR 
    Gateway-> (condition 1) Task. Additionally, provide a mapping of actors to activities, in the format actor: [activity1, ...]

    A good example of formatting:
    Order Received-> XOR Gateway 1
    XOR Gateway 1-> (Order Rejected) End Event
    XOR Gateway 1-> (Order Accepted) AND Gateway 1
    AND Gateway 1-> Process Part List
    AND Gateway 1-> Prepare for Assembling

    Process description: A small company manufactures customized bicycles. Whenever the sales department receives an order, a new process instance is created. A member of the sales 
    department can then reject or accept the order for a customized bike. In the former case, the process instance is nished. In the latter case, the storehouse and the engineering department are 
    informed. The storehouse immediately processes the part list of the order and checks the required quantity of each part. If the part is available in- hause, it is reserved. If it is not available, it is 
    back-ordered. This procedure is repeated for each item on the part list. In the meantime, the engineering department prepares everything for the assembling of the ordered bicycle. If the 
    storehouse successfully reserved or back-ordered every item of the part list and the preparation activity has nished, the engineering department assembles the bicycle. Afterwards, the sales 
    department ships the bicycle to the customer and nishes the process instance

## Response
Sales Order Received> XOR Gateway 1

XOR Gateway 1> (Order Rejected) End Event

XOR Gateway 1> (Order Accepted) AND Gateway 1

AND Gateway 1> Inform Storehouse

AND Gateway 1> Inform Engineering Department

Inform Storehouse> AND Gateway 2

Inform Engineering Department> Prepare for Assembling

AND Gateway 2> Process Part List

AND Gateway 2> Check Part Availability

Check Part Availability> XOR Gateway 2

XOR Gateway 2> (Part Available) Reserve Part

XOR Gateway 2> (Part Unavailable) Back-Order Part

Reserve Part> AND Gateway 3

Back-Order Part> AND Gateway 3

AND Gateway 3> Check All Parts Reserved or Back-Ordered

Check All Parts Reserved or Back-Ordered> XOR Gateway 3

XOR Gateway 3> (All Parts Reserved or Back-Ordered) Assemble Bicycle

XOR Gateway 3> (Not All Parts Reserved or Back-Ordered) End Event

Assemble Bicycle> Ship Bicycle

Ship Bicycle> End Event

Actor Mapping:

- Sales Department: [Sales Order Received, Order Rejected, Order Accepted]
- Storehouse: [Inform Storehouse, Process Part List, Check Part Availability, Reserve Part, Back-Order Part, Check - All Parts Reserved or Back-Ordered]
- Engineering Department: [Inform Engineering Department, Prepare for Assembling, Assemble Bicycle]
- Sales Department (for shipping): [Ship Bicycle]