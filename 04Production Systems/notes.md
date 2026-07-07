# TMK Refinement Notes

## Refinement 1: Added Cognitive Architecture Concepts

### Summary
Expanded the Knowledge model to represent Production Systems as a cognitive architecture, following the lesson's framing of SOAR as an architecture for deliberation, action selection, memory, and learning.

### Changes

#### cognitiveArchitecture
- Added the `cognitiveArchitecture` concept.
- Represents an architecture that combines fixed reasoning mechanisms with knowledge content to produce behavior.
- Included because the lesson introduces Production Systems as a kind of cognitive architecture.

#### SOAR
- Added the `SOAR` concept.
- Represents the specific production-system architecture used in the lesson.
- Includes working memory, long-term memory, decision making, impasse handling, and chunking.

#### behavior
- Added the `behavior` concept.
- Represents the observable result produced by a cognitive architecture operating on knowledge content.

#### architectureContentBehavior
- Added an assertion representing the lesson's equation: architecture plus content equals behavior.

### Rationale
The original model represented production rules and memories, but it did not explicitly capture the architectural framing from the lesson. Adding these concepts connects the TMK model to the lesson's central claim that a fixed cognitive architecture plus different knowledge content can produce different behaviors.

## Refinement 2: Added Production Rule Structure

### Summary
Refined the Knowledge model so production rules are represented as if-then structures with antecedents and consequents.

### Changes

#### antecedent
- Added the `antecedent` concept.
- Represents the if-part of a production rule.
- Used to model matching against the contents of working memory.

#### consequent
- Added the `consequent` concept.
- Represents the then-part of a production rule.
- Used to model updates to working memory, operator suggestions, and action execution.

#### consequentSet
- Added the `consequentSet` concept.
- Represents the collection of consequents produced by fired production rules.

#### Rule Relations
- Added `hasAntecedent` from `productionRule` to `antecedent`.
- Added `hasConsequent` from `productionRule` to `consequent`.
- Added `matches` from `workingMemory` to `antecedent`.
- Added `fires` from `productionRule` to `consequent`.
- Added `updates` from `consequent` to `workingMemory`.

### Rationale
The lesson explicitly describes production rules as having antecedents and consequents. The previous model named `productionRule` but did not represent its internal structure. This refinement makes the if-then form of production rules explicit.

## Refinement 3: Clarified Memory and Knowledge Types

### Summary
Added descriptions and relations for the memory architecture described in the lesson, especially the distinction between working memory and long-term memory.

### Changes

#### workingMemory
- Added a description identifying working memory as short-term, rapidly changing memory.
- Represents current percepts, goals, and rule consequents.

#### longTermMemory
- Added a description identifying long-term memory as relatively stable memory.
- Represents storage for procedural, semantic, and episodic knowledge.

#### proceduralKnowledge
- Added a description identifying procedural knowledge as how-to knowledge represented as production rules.
- Added `representsAsRule` from `proceduralKnowledge` to `productionRule`.

#### semanticKnowledge
- Added a description identifying semantic knowledge as general conceptual knowledge and world models.
- Added `generalizesAs` from `semanticKnowledge` to `knowledgeContent`.

#### episodicKnowledge
- Added a description identifying episodic knowledge as specific remembered events.
- Added `records` from `episodicKnowledge` to `episode`.

#### Long-Term Memory Relations
- Added `containsProceduralKnowledge`.
- Added `containsSemanticKnowledge`.
- Added `containsEpisodicKnowledge`.

### Rationale
The original model listed the three kinds of knowledge but did not explain them or connect them to the architecture. This refinement aligns the Knowledge model with the lesson's account of SOAR's long-term memory.

## Refinement 4: Added Percept-to-Action Concepts

### Summary
Expanded the model to represent the lesson's definition of a cognitive agent as mapping perceptual history into action.

### Changes

#### perceptHistory
- Added the `perceptHistory` concept.
- Represents the history of percepts used by a cognitive agent during action selection.

#### action
- Added the `action` concept.
- Represents an executable behavior selected by the production system.

#### motorSystem
- Added the `motorSystem` concept.
- Represents the component that receives selected operators or actions for execution.

#### Operator and Action Relations
- Added `mapsTo` from `perceptHistory` to `action`.
- Added `sendsTo` from `operator` to `motorSystem`.
- Added `realizesAction` from `operator` to `action`.

### Rationale
The previous model used `operator`, but the lesson distinguishes suggested operators from actions sent to the motor system. Adding these concepts makes the action-selection endpoint clearer.

## Refinement 5: Added Rule Firing and Working Memory Update Tasks

### Summary
Expanded the Task model to represent the production-system cycle more explicitly.

### Changes

#### FireActivatedRules
- Added the `FireActivatedRules` task.
- Represents firing activated production rules and collecting their consequents.

#### UpdateWorkingMemory
- Added the `UpdateWorkingMemory` task.
- Represents writing rule consequents back into working memory.

#### SendActionToMotorSystem
- Added the `SendActionToMotorSystem` task.
- Represents sending the selected operator or action to the motor system.

### Rationale
The lesson emphasizes that activated rules fire, their consequents update working memory, and updated working memory may activate additional rules. The original task model skipped over this intermediate cycle and moved too directly from matching rules to selecting an operator.

## Refinement 6: Corrected the Production System Method Loop

### Summary
Refined the Method model so the production system repeatedly matches, fires, and updates working memory until it is ready to select an operator or encounters an impasse.

### Changes

#### Match-Fire-Update Cycle
- Added a `FireActivatedRules` state.
- Added an `UpdateWorkingMemory` state.
- Added a loop from working-memory update back to rule matching when working memory changes and no operator is ready to select.

#### Action Selection
- Added a state for sending a single selected operator to the motor system.
- Completion now depends on `goodActionSelection(finalConfiguration)`.

#### Method Mechanisms
- Added `RuleFiringMechanism`.
- Added `WorkingMemoryUpdateMechanism`.
- Added `MotorActionMechanism`.

### Rationale
The lesson describes production systems as an interaction between working memory and long-term memory. Rule consequents can update working memory, which can then activate additional rules. This refinement makes that iterative interaction explicit instead of modeling production systems as a single-pass match-and-select procedure.

## Refinement 7: Added Impasse and Chunking Flow

### Summary
Refined the model so impasses trigger chunking, and chunking can add a learned production rule back into procedural knowledge.

### Changes

#### impasse
- Added the `impasse` concept.
- Represents a state where the agent cannot decide because knowledge is insufficient or multiple operators are suggested.

#### chunking
- Added the `chunking` concept.
- Represents learning a new production rule from episodic knowledge to resolve an impasse.

#### episode
- Added the `episode` concept.
- Represents a specific remembered event used as the source for chunking.

#### Chunking Relations
- Added `usesEpisode` from `chunking` to `episode`.
- Added `resolves` from `chunking` to `impasse`.
- Preserved `learns` from `episodicKnowledge` to `productionRule`.

#### Method Flow
- Added a `PS_Chunk` state.
- Routed missing rules, empty consequents, and multiple suggested operators to chunking.
- Added a transition from chunking back to rule matching when a new rule is learned.

### Rationale
The lesson treats chunking as the learning mechanism that is triggered by an impasse. The original model had chunking, but it treated the impasse path as a failure state rather than as a recoverable learning path. This refinement models chunking as part of the production-system cycle.

## Refinement 8: Added State-Space Representation Concepts

### Summary
Expanded the Knowledge model to explicitly represent the state-space vocabulary introduced before the lesson moves into production rules.

### Changes

#### state
- Added the `state` concept.
- Represents a configuration in the production-system decision space.

#### stateSpace
- Added the `stateSpace` concept.
- Represents the set of states reachable by applying operators from an initial state.

#### initialState
- Added the `initialState` concept.
- Represents the starting state of the decision problem before operators are applied.

#### goalState
- Added the `goalState` concept.
- Represents the desired state in which the agent's goal has been accomplished.

#### feature
- Added the `feature` concept.
- Represents an attribute used to describe a state or configuration.

#### featureValue
- Added the `featureValue` concept.
- Represents a value assigned to a feature in a feature-value representation.

#### State-Space Relations
- Added `describedBy` from `state` to `feature`.
- Added `hasValue` from `feature` to `featureValue`.
- Added `belongsTo` from `state` to `stateSpace`.
- Added `hasInitialState` from `stateSpace` to `initialState`.
- Added `hasGoalState` from `stateSpace` to `goalState`.

### Rationale
The previous model used `configuration` to cover the idea of feature-value states, but the lesson explicitly introduces states, state spaces, initial states, goal states, features, and feature values before discussing production rules. Adding these concepts makes the model align more directly with the lesson's setup for action selection.
