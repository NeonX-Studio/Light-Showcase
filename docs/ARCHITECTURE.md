# Light architecture

Light is designed around a separation between authoritative simulation rules and an AI reasoning layer.

## Core loop

1. The player interacts with an NPC, object, quest, or environment system.
2. Gameplay systems read and update structured world state.
3. A context builder selects only the information relevant to the current interaction.
4. The AI layer proposes dialogue, a task, or a possible world event in a structured response format.
5. Runtime validation checks the proposal against permissions, available entities, quest state, and system constraints.
6. Accepted state changes are written back to the simulation and become available to future interactions.

## Bounded AI principles

The AI is given a role and a limited information scope. An NPC should know what its role, memories, environment, and authority allow it to know. The runtime remains responsible for entity identity, quest lifecycle, state transitions, and persistence.

This boundary supports three goals:

- **Consistency:** generated content remains anchored to the current simulation.
- **Testability:** state changes can be validated independently of generated language.
- **Safety:** the model cannot directly invent authoritative entities or bypass game rules.

## Main system areas

| Area | Responsibility |
| --- | --- |
| World state | Resources, regional conditions, global flags, event history |
| NPC systems | Memory, attitude, emotion, knowledge scope, interaction state |
| Quest systems | Generation proposals, objectives, lifecycle, completion and failure |
| Interaction systems | Interactable objects, containers, terminals, and contextual actions |
| Network subsystem | Asynchronous communication with the configured AI provider |
| Persistence | Save and restore of world, NPC, quest, and object state |
| UI layer | Dialogue, quest feedback, state feedback, and debug presentation |

## Data-driven direction

NPC and quest behavior is configured through structured data and validated schemas. The public repository does not include the private JSON datasets, prompt libraries, RAG material, or runtime service configuration used by the development project.

## Future multiplayer boundary

The project roadmap includes a server-authoritative boundary for shared world state and AI arbitration. The public direction is to keep simulation authority, validation, and persistence on the trusted side of that boundary while clients receive only the state and presentation data needed for play.
