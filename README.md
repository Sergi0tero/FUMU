   +------------------+
   |   DataFetcher    |  --> ExcelLogger (cada hora)
   +------------------+
             |
         [Publish]
             ↓
 +---------------------+
 |   Pub/Sub Broker    |
 +---------------------+
        /        \
       /          \
Grupo Trad    Grupo IA
 (2 agentes)   (2 agentes)
    ↓              ↓
Average Consensus Average Consensus
    \              /
     \            /
    +-------------+
    | Whiteboard  |
    +-------------+
          |
   +--------------+
   | DecisionMaker|
   +--------------+
