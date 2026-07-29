# TMK Refinement Notes

## Refinement 1: Expanded Knowledge for Case-Based Reasoning

### Summary
Refined the Knowledge model for Lesson 09 to better reflect the case-based reasoning framework described in the lesson, including the core assumptions, retrieval methods, adaptation mechanisms, evaluation strategies, and case storage.

### Changes

#### Core Case-Based Reasoning Concepts
- Added the `caseBasedReasoning` concept.
- Defined it as a problem-solving method that reuses stored cases from memory.
- Included to represent the lesson’s central framing of reasoning through prior experience.

#### Case and Case Memory
- Strengthened the descriptions of `case` and `caseMemory`.
- Clarified that a case is a stored experience that pairs a problem with a solution, and that case memory is the repository of such prior cases.
- This better matches the lesson’s emphasis on memory as a source of reusable experience.

#### Similarity and Heuristics
- Added the `similarity` concept.
- Added the `heuristic` concept.
- These concepts capture the lesson’s assumptions that similar problems often have similar solutions and that adaptation may rely on heuristic rules of thumb.

#### Adaptation Methods
- Expanded the adaptation-related knowledge to distinguish three common methods:
  - `ModelBasedAdaptation`
  - `RecursiveCaseBasedAdaptation`
  - `RuleBasedAdaptation`
- Added supporting concepts for `model` and `subgoal` to represent model-based adaptation and recursive decomposition.

#### Evaluation and Storage
- Added `evaluationMethod` as a concept to represent how candidate solutions are tested or judged.
- Added instances such as `Simulation`, `Execution`, `Prototype`, and `Critique` to reflect the lesson’s discussion of evaluation.
- Added `caseBase` as a concrete case memory instance and updated the workflow to emphasize that successful solutions are stored for future reuse.

### Rationale
The original TMK model captured the general idea of reusing cases, but it did not explicitly represent the lesson’s deeper structure: the assumptions behind case-based reasoning, the different adaptation strategies, the role of evaluation, and the final storage step. This refinement makes the model more faithful to Lesson 09 and better aligned with the instructional content.
